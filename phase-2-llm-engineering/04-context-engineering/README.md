# 04 - Context Engineering

Context engineering is the discipline of deciding what goes into the LLM's context window on every call. It is as important as prompt engineering and most engineers learn it late. Context determines quality, cost, and latency. All three.

The context window is finite. You have budget for a system prompt, conversation history, retrieved documents, tool definitions, and the response. Everything competes for the same space.

---

## Token budgeting

Before you write a prompt, know what it costs. Tokens are your currency.

```python
import anthropic
import tiktoken

# Count tokens before sending (OpenAI models)
def count_tokens_openai(text: str, model: str = "gpt-4o") -> int:
    enc = tiktoken.encoding_for_model(model)
    return len(enc.encode(text))

# Count tokens with Anthropic's API
client = anthropic.Anthropic()

def count_tokens_anthropic(messages: list, system: str = "") -> int:
    response = client.messages.count_tokens(
        model="claude-opus-4-8",
        system=system,
        messages=messages,
    )
    return response.input_tokens

# Budget allocation example
CONTEXT_LIMIT = 200_000   # claude-opus-4-8
RESPONSE_BUDGET = 4_000
SYSTEM_BUDGET = 2_000
HISTORY_BUDGET = 50_000
RETRIEVAL_BUDGET = CONTEXT_LIMIT - RESPONSE_BUDGET - SYSTEM_BUDGET - HISTORY_BUDGET
# leaves ~144k for retrieved documents
```

Plan your budget before building. A common failure is discovering at runtime that the conversation history alone fills the window.

---

## Prompt caching

Prompt caching reuses computed context across API calls. When a prefix of your prompt is identical to a prior call, the model skips recomputing it and returns the cached KV state. This cuts latency by up to 85% and cost by up to 90% for the cached portion.

### Anthropic prompt caching

Mark long, stable content with `cache_control`. The cache is keyed on everything before the marker.

```python
import anthropic

client = anthropic.Anthropic()

# The system prompt is the same every call — cache it
response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=1024,
    system=[
        {
            "type": "text",
            "text": LARGE_SYSTEM_PROMPT,           # 10k+ tokens of stable instructions
            "cache_control": {"type": "ephemeral"} # cache this prefix
        }
    ],
    messages=[{"role": "user", "content": user_message}]
)

print(response.usage)
# cache_creation_input_tokens: charged at 1.25x on first call
# cache_read_input_tokens: charged at 0.1x on subsequent calls
```

Cache what is stable. The cache breaks when content before the marker changes.

**What to cache:**
- Long system prompts with static instructions
- Large documents being analyzed across multiple turns
- Tool definitions (rarely change within a session)
- Few-shot examples that stay constant

**What not to cache:**
- Dynamic data (timestamps, user names, search results)
- Content that changes every request

### Organizing prompts for maximum cache hits

Put stable content first, dynamic content last. Cache is prefix-based.

```python
# Good: stable parts first
messages = [
    {
        "role": "user",
        "content": [
            {
                "type": "text",
                "text": STATIC_LONG_DOCUMENT,       # 50k tokens — always the same
                "cache_control": {"type": "ephemeral"}
            },
            {
                "type": "text",
                "text": f"Question: {dynamic_question}"  # changes per call
            }
        ]
    }
]

# Bad: dynamic content before the cache break point
# The cache will miss because the prefix changed
```

---

## Context compression

When conversation history grows too long, compress it. The naive approach — truncating old messages — loses continuity. These patterns preserve the important parts.

### Rolling summary

Summarize old turns into a single message. Keep recent turns verbatim.

```python
import anthropic

client = anthropic.Anthropic()
WINDOW_SIZE = 10     # keep last N turns verbatim
SUMMARY_TRIGGER = 20 # summarize when history exceeds N turns

def compress_history(messages: list[dict]) -> list[dict]:
    if len(messages) <= WINDOW_SIZE:
        return messages

    to_summarize = messages[:-WINDOW_SIZE]
    recent = messages[-WINDOW_SIZE:]

    summary_prompt = (
        "Summarize the following conversation. "
        "Preserve all decisions, facts, and open questions. "
        "Be dense, not conversational.\n\n"
        + "\n".join(f"{m['role']}: {m['content']}" for m in to_summarize)
    )

    summary = client.messages.create(
        model="claude-haiku-4-5-20251001",  # use a fast, cheap model for summarization
        max_tokens=1000,
        messages=[{"role": "user", "content": summary_prompt}]
    ).content[0].text

    return [
        {"role": "user", "content": f"[Conversation summary]\n{summary}"},
        {"role": "assistant", "content": "Understood. I have the context from earlier."},
        *recent,
    ]
```

### Selective retention

Not all messages are equal. Keep messages that contain decisions, facts, or open tasks. Discard filler.

```python
IMPORTANT_KEYWORDS = ["decided", "error", "requirement", "must", "confirmed", "TODO"]

def filter_messages(messages: list[dict], max_tokens: int = 20_000) -> list[dict]:
    scored = []
    for msg in messages:
        content = msg["content"]
        score = sum(1 for kw in IMPORTANT_KEYWORDS if kw.lower() in content.lower())
        scored.append((score, msg))

    # Always keep the last 4 messages (recent context)
    recent = messages[-4:]
    candidates = [m for _, m in sorted(scored, key=lambda x: -x[0])]

    selected = []
    total_tokens = 0
    for msg in candidates:
        tokens = len(msg["content"].split()) * 1.3  # rough estimate
        if total_tokens + tokens > max_tokens:
            break
        if msg not in recent:
            selected.append(msg)
            total_tokens += tokens

    # Reconstruct in original order
    all_kept = set(id(m) for m in selected + recent)
    return [m for m in messages if id(m) in all_kept]
```

---

## Dynamic context selection

When you have more information than fits, choose what to include based on the current query. This is the same idea as RAG but applied to conversation history, tool documentation, and anything else in context.

```python
from anthropic import Anthropic
import numpy as np

client = Anthropic()

def get_embedding(text: str) -> list[float]:
    # Use any embedding model
    # Voyager, OpenAI text-embedding-3-small, etc.
    ...

def select_relevant_context(
    query: str,
    context_pool: list[dict],  # [{"content": "...", "embedding": [...]}]
    max_items: int = 5,
) -> list[str]:
    query_emb = np.array(get_embedding(query))

    scored = []
    for item in context_pool:
        item_emb = np.array(item["embedding"])
        similarity = float(np.dot(query_emb, item_emb) / (
            np.linalg.norm(query_emb) * np.linalg.norm(item_emb)
        ))
        scored.append((similarity, item["content"]))

    scored.sort(key=lambda x: -x[0])
    return [content for _, content in scored[:max_items]]
```

The principle: always ask "is this content relevant to what the model needs to answer right now?" If not, leave it out. Every irrelevant token dilutes the model's attention.

---

## Conversation management at scale

Long conversations need explicit state management. Treat the context window like memory — what to keep, what to compress, what to evict.

```python
from dataclasses import dataclass, field
from typing import Literal

@dataclass
class ConversationManager:
    model: str = "claude-opus-4-8"
    max_context_tokens: int = 150_000  # leave headroom
    messages: list[dict] = field(default_factory=list)
    _client: anthropic.Anthropic = field(default_factory=anthropic.Anthropic)

    def add_user_message(self, content: str) -> None:
        self.messages.append({"role": "user", "content": content})
        self._maybe_compress()

    def chat(self, user_input: str) -> str:
        self.add_user_message(user_input)

        response = self._client.messages.create(
            model=self.model,
            max_tokens=2048,
            messages=self.messages,
        )
        assistant_message = response.content[0].text
        self.messages.append({"role": "assistant", "content": assistant_message})
        return assistant_message

    def _maybe_compress(self) -> None:
        token_count = self._estimate_tokens()
        if token_count > self.max_context_tokens:
            self.messages = compress_history(self.messages)

    def _estimate_tokens(self) -> int:
        # rough estimate: 4 chars per token
        total_chars = sum(len(str(m["content"])) for m in self.messages)
        return total_chars // 4
```

---

## Context window strategies by task

| Task | Strategy |
|---|---|
| Single-turn Q&A | Include only what answers the question, no more |
| Multi-turn chat | Rolling window + summary for history beyond N turns |
| Document analysis | Cache the document, stream questions against it |
| Agent with tools | Cache system prompt + tool defs, keep recent steps only |
| RAG | Retrieve and score chunks, take the top K by relevance |
| Code review | Include only the diff and the relevant file, not the whole repo |

---

## What not to put in context

- The whole codebase (use RAG or file search tools instead)
- Logs that are not relevant to the current task
- Examples the model has already seen and acted on
- Repeated instructions already in the system prompt
- Raw database dumps (process them first)

Every token in context is a token the model reads. Noise in → noise out.

---

## Resources

- [Anthropic Prompt Caching Docs](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching)
- [OpenAI Prompt Caching](https://platform.openai.com/docs/guides/prompt-caching)
- [tiktoken](https://github.com/openai/tiktoken) — token counting for OpenAI models
- [Lilian Weng - The Transformer Family](https://lilianweng.github.io/posts/2023-01-27-the-transformer-family-v2/) — how attention and context actually work
