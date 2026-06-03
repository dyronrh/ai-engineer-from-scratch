# 06 - Memory Systems

Stateless LLM calls forget everything. Production agents need memory: what the user said last session, what the agent tried and failed, what facts are true about this user's environment. Without memory, every conversation starts from zero.

Memory is not one thing. It is several different mechanisms, each solving a different problem.

---

## Memory taxonomy

| Type | What it stores | Where | Lifespan |
|---|---|---|---|
| **In-context** | Current conversation turns | Message list | Single session |
| **Working** | Compressed recent history | Summarized message | Single session |
| **External short-term** | Cross-request state | Redis, database | Hours to days |
| **Semantic** | Facts, knowledge, preferences | Vector store | Persistent |
| **Episodic** | Past agent runs and outcomes | Structured logs | Persistent |
| **Procedural** | How to do things | Tool definitions, prompts | Persistent |

Most production agents need in-context + semantic at minimum. Add episodic when the agent needs to learn from its own history.

---

## In-context memory

The simplest form. The message list is the memory. Everything the model knows about the current task is in the `messages` array.

```python
import anthropic

client = anthropic.Anthropic()
messages: list[dict] = []

def chat(user_input: str) -> str:
    messages.append({"role": "user", "content": user_input})

    response = client.messages.create(
        model="claude-opus-4-8",
        max_tokens=1024,
        messages=messages,
    )

    assistant_reply = response.content[0].text
    messages.append({"role": "assistant", "content": assistant_reply})
    return assistant_reply
```

**Limit:** it fills up. At some point the conversation is too long for the context window. Handle this with a sliding window or summarization (see context engineering module).

---

## External short-term memory

For state that must survive between API calls, server restarts, or parallel agent runs. Redis is the standard choice for speed; Postgres for durability.

```python
import json
import redis
import anthropic

r = redis.Redis(host="localhost", port=6379, decode_responses=True)
client = anthropic.Anthropic()

SESSION_TTL = 60 * 60  # 1 hour

def get_session_messages(session_id: str) -> list[dict]:
    raw = r.get(f"session:{session_id}:messages")
    return json.loads(raw) if raw else []

def save_session_messages(session_id: str, messages: list[dict]) -> None:
    r.setex(
        f"session:{session_id}:messages",
        SESSION_TTL,
        json.dumps(messages),
    )

def chat(session_id: str, user_input: str) -> str:
    messages = get_session_messages(session_id)
    messages.append({"role": "user", "content": user_input})

    response = client.messages.create(
        model="claude-opus-4-8",
        max_tokens=1024,
        messages=messages,
    )

    reply = response.content[0].text
    messages.append({"role": "assistant", "content": reply})
    save_session_messages(session_id, messages)
    return reply
```

Use this when you have multiple servers handling the same user session, or when you need conversation state to outlast a single process.

---

## Semantic memory (long-term)

Facts, user preferences, and knowledge that should persist across sessions. Stored as embeddings in a vector database. Retrieved by similarity when relevant to the current query.

```python
import anthropic
import chromadb
from chromadb.utils.embedding_functions import OpenAIEmbeddingFunction

client = anthropic.Anthropic()
chroma = chromadb.Client()
embedding_fn = OpenAIEmbeddingFunction(api_key="...", model_name="text-embedding-3-small")
memory_collection = chroma.get_or_create_collection("agent_memory", embedding_function=embedding_fn)

def remember(fact: str, metadata: dict | None = None) -> None:
    memory_collection.add(
        documents=[fact],
        metadatas=[metadata or {}],
        ids=[f"mem_{hash(fact)}"],
    )

def recall(query: str, n: int = 5) -> list[str]:
    results = memory_collection.query(query_texts=[query], n_results=n)
    return results["documents"][0] if results["documents"] else []

def chat_with_memory(user_input: str) -> str:
    # Retrieve relevant memories before responding
    memories = recall(user_input)
    memory_context = "\n".join(f"- {m}" for m in memories)

    system = "You are a helpful assistant."
    if memory_context:
        system += f"\n\nRelevant context from memory:\n{memory_context}"

    response = client.messages.create(
        model="claude-opus-4-8",
        max_tokens=1024,
        system=system,
        messages=[{"role": "user", "content": user_input}],
    )
    return response.content[0].text

# Example
remember("User prefers concise responses, no more than 3 sentences.")
remember("User is building a FastAPI backend that connects to PostgreSQL.")
remember("User's production environment is AWS ECS with Fargate.")
```

**What to store in semantic memory:**
- User preferences and working style
- Facts established in past conversations
- Decisions the agent made and why
- Domain knowledge that would otherwise need to be re-explained

**What not to store:** raw conversation transcripts (that is episodic memory). Extract the facts from them first.

---

## Episodic memory

A log of what the agent did, what happened, and what the outcome was. Used to avoid repeating mistakes, to summarize past work, and to let agents learn from experience.

```python
import json
from datetime import datetime, UTC
from pathlib import Path

EPISODE_LOG = Path("agent_episodes.jsonl")

def log_episode(
    task: str,
    steps: list[dict],
    outcome: str,
    success: bool,
) -> None:
    episode = {
        "timestamp": datetime.now(UTC).isoformat(),
        "task": task,
        "steps": steps,
        "outcome": outcome,
        "success": success,
    }
    with EPISODE_LOG.open("a") as f:
        f.write(json.dumps(episode) + "\n")

def get_relevant_episodes(task: str, max_episodes: int = 3) -> list[dict]:
    if not EPISODE_LOG.exists():
        return []

    episodes = []
    with EPISODE_LOG.open() as f:
        for line in f:
            ep = json.loads(line)
            # Simple keyword match — use embeddings for production
            if any(word in ep["task"] for word in task.split()):
                episodes.append(ep)

    # Return most recent relevant episodes
    return sorted(episodes, key=lambda e: e["timestamp"], reverse=True)[:max_episodes]

def format_episode_context(episodes: list[dict]) -> str:
    if not episodes:
        return ""

    lines = ["Past attempts at similar tasks:"]
    for ep in episodes:
        status = "succeeded" if ep["success"] else "failed"
        lines.append(f"- [{status}] {ep['task']}: {ep['outcome']}")

    return "\n".join(lines)
```

Episodic memory is what lets an agent say "I tried that approach last time and it failed because X, so this time I will try Y."

---

## LangGraph persistence

LangGraph has built-in checkpointing that saves graph state after every step. This gives you durable, resumable agent runs out of the box.

```python
from langgraph.graph import StateGraph, END
from langgraph.checkpoint.memory import MemorySaver
from langgraph.checkpoint.postgres import PostgresSaver
from typing import TypedDict

class AgentState(TypedDict):
    messages: list[dict]
    memory_context: str
    task: str

def build_agent_with_memory():
    graph = StateGraph(AgentState)
    graph.add_node("think", think_node)
    graph.add_node("act", act_node)
    graph.add_node("observe", observe_node)
    graph.set_entry_point("think")

    # For development: in-memory checkpointing
    checkpointer = MemorySaver()

    # For production: PostgreSQL checkpointing
    # checkpointer = PostgresSaver.from_conn_string("postgresql://...")

    return graph.compile(checkpointer=checkpointer)

agent = build_agent_with_memory()

# thread_id makes this run resumable
config = {"configurable": {"thread_id": "user-123-task-456"}}

# Start or resume the run
result = agent.invoke({"task": "Research competitors"}, config=config)

# If the process dies, invoking with the same thread_id resumes from last checkpoint
result = agent.invoke(None, config=config)  # None = resume
```

---

## Memory frameworks

Building memory from scratch is reasonable for simple use cases. For production systems with multiple users and complex retrieval needs, purpose-built frameworks save significant time.

### Mem0

Open-source memory layer with an API. Handles storage, retrieval, and updating of memories across users and sessions. Supports local and cloud storage.

```python
from mem0 import Memory

memory = Memory()

# Add a memory
memory.add("User prefers TypeScript over JavaScript for new projects.", user_id="user_123")

# Search memories
results = memory.search("what language does this user prefer?", user_id="user_123")
for r in results:
    print(r["memory"])
```

- [Mem0 Docs](https://docs.mem0.ai/)
- Best for: user-level memory that needs to be searchable and updateable

### Zep

Memory layer for LLM applications with automatic summarization, entity extraction, and temporal reasoning. Stores conversation history and extracts structured facts automatically.

```python
from zep_cloud.client import Zep

zep = Zep(api_key="...")

# Add a session message — Zep auto-extracts facts and entities
zep.memory.add(
    session_id="session_123",
    messages=[{"role": "user", "content": "I'm migrating from MySQL to PostgreSQL."}]
)

# Retrieve memory with temporal context
memory = zep.memory.get("session_123")
print(memory.relevant_facts)  # ["User is migrating from MySQL to PostgreSQL"]
```

- [Zep Docs](https://docs.getzep.com/)
- Best for: conversation-level memory with automatic entity extraction

### LangGraph Memory Store

LangGraph's built-in memory store for cross-thread persistent memory. Accessible from any node in the graph.

```python
from langgraph.store.memory import InMemoryStore
from langgraph.store.postgres import PostgresStore

# Development
store = InMemoryStore()

# Production  
store = PostgresStore.from_conn_string("postgresql://...")

# In a graph node: write a memory
async def update_user_preferences(state, config, *, store):
    user_id = config["configurable"]["user_id"]
    await store.aput(
        namespace=("user_preferences", user_id),
        key="language",
        value={"preference": "TypeScript", "updated_at": "2026-01-15"}
    )

# In a graph node: read memories
async def personalize_response(state, config, *, store):
    user_id = config["configurable"]["user_id"]
    prefs = await store.aget(("user_preferences", user_id), "language")
    return {"preference_context": str(prefs.value) if prefs else ""}
```

- [LangGraph Memory Docs](https://langchain-ai.github.io/langgraph/concepts/memory/)

---

## Memory read/write patterns

**When to write:**
- After a user states a preference ("I always want JSON output")
- After a successful task completes (store what worked)
- After a failure (store what failed and why)
- When the user provides factual context ("My stack is Next.js + Supabase")

**When to read:**
- At the start of every agent turn (retrieve relevant memories for the current query)
- Before calling a tool (does memory tell you anything about this tool's quirks for this user?)
- After a failure (has this failed before? what did we try?)

**Conflict resolution:**
```python
def update_or_replace_memory(memory_store, user_id: str, key: str, new_value: str) -> None:
    existing = memory_store.get(user_id, key)

    if not existing:
        memory_store.set(user_id, key, new_value)
        return

    # Decide: update vs. replace vs. append
    # Simple heuristic: newer explicit statement wins
    # For preferences, replace. For facts, append with timestamp.
    memory_store.set(user_id, key, new_value, overwrite=True)
```

**Do not over-remember:** Storing everything creates retrieval noise. Be selective. The goal is relevant context, not a transcript.

---

## Memory in multi-agent systems

Each agent in a multi-agent system can have its own memory, or they can share a memory store. Share selectively.

```
Coordinator agent
    → reads user memory (preferences, history)
    → passes relevant subset to each specialist
    
Researcher agent
    → reads episodic memory of past research runs
    → writes findings to shared working memory

Writer agent
    → reads shared working memory (researcher's findings)
    → reads user preferences (tone, length)
    → writes final output to episodic memory
```

Shared memory creates coupling. Give each agent the memory it needs, not everything.

---

## Quick reference: choosing the right memory type

| Situation | Memory type |
|---|---|
| Remember what was said 3 messages ago | In-context (message list) |
| Resume a conversation next day | External short-term (Redis/DB) |
| Remember a user preference forever | Semantic (vector store or Mem0) |
| Avoid repeating a failed approach | Episodic (structured log) |
| Resume an agent run after a crash | LangGraph checkpointing |
| User-level memory across many sessions | Mem0 or Zep |
| Agent state in a LangGraph graph | LangGraph Memory Store |

---

## Resources

- [LangGraph Memory Docs](https://langchain-ai.github.io/langgraph/concepts/memory/)
- [Mem0](https://mem0.ai/) — open-source memory layer for AI agents
- [Zep](https://www.getzep.com/) — memory and temporal reasoning for LLM apps
- [Lilian Weng - LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/) — memory taxonomy section is essential reading
