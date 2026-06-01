# Phase 3 - Agentic AI

**Duration:** 6-8 weeks  
**Prerequisite:** Phase 2 done, you can call LLM APIs and use tool/function calling

---

## Why this phase matters more than any other

From real job postings:

- AI Agents: **980% job posting growth** from 2023 to 2024
- LangGraph/LangChain: in **39.9% of all agentic AI engineering roles**
- RAG: **dominant production use case** across every company size
- MCP: already showing up in job descriptions
- Agentic AI engineers earn **15-20% more** than standard AI engineers

Companies are not hiring for ML theory. They want people who can build systems that plan, retrieve, act, and loop until a job is done. That is what this phase teaches.

---

## Modules

### [01 - RAG Systems](./01-rag-systems/)

Retrieval-Augmented Generation. The most deployed production pattern for LLM applications. If a company builds on LLMs and has their own data, they almost certainly need RAG.

**Topics:**
- Embeddings: picking the right model, understanding similarity
- Vector databases: Chroma (local), Pinecone (managed), pgvector (Postgres)
- Basic RAG pipeline: chunk, embed, store, retrieve, generate
- Advanced RAG: HyDE, reranking with cross-encoders, hybrid search
- Evaluating RAG with RAGAS: faithfulness, context relevance, answer quality

**Resources:**
| Resource | Time |
|---|---|
| [Pinecone Learning Center](https://www.pinecone.io/learn/) | 1 week |
| [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings) | 2 days |
| [LlamaIndex Docs](https://docs.llamaindex.ai/) | 1 week |
| [RAGAS Docs](https://docs.ragas.io/) | 3 days |

---

### [02 - Agentic Patterns](./02-agentic-patterns/)

The design patterns that make agents actually work. These are recurring solutions to recurring problems. Learn the patterns before learning the frameworks, or the frameworks will feel like magic boxes.

**Patterns to know:**
- **ReAct** (Reason + Act): think, act, observe the result, think again
- **Planning**: break a goal into steps before executing any of them
- **Reflection**: evaluate your own output and retry if it falls short
- **Tool use**: let the model decide when to call external tools
- **Memory**: short-term (conversation), long-term (vector store), episodic

**Resources:**
| Resource | Time |
|---|---|
| [ReAct paper](https://arxiv.org/abs/2210.03629) | 2 days |
| [LangGraph conceptual guides](https://langchain-ai.github.io/langgraph/concepts/) | 1 week |

---

### [03 - LangGraph](./03-langgraph/)

The framework for building stateful, controllable agents. Appears in 39.9% of agentic AI job postings. LangGraph lets you build agents that branch, loop, retry, and coordinate, not just chain prompts together linearly.

**Topics:**
- State graphs: nodes, edges, conditional routing
- Checkpointing and resuming agent runs
- Human-in-the-loop: pause and wait for approval before continuing
- Streaming agent outputs
- Subgraphs and modular agent design

**Resources:**
| Resource | Time |
|---|---|
| [LangGraph Docs](https://langchain-ai.github.io/langgraph/) | 2 weeks |
| [LangGraph tutorials](https://langchain-ai.github.io/langgraph/tutorials/) | 1 week |

---

### [04 - Multi-Agent Systems](./04-multi-agent/)

One agent trying to do everything produces mediocre results. Multi-agent systems use a coordinator to delegate to specialists, each focused on one thing with the right tools for it.

**Topics:**
- Coordinator + specialist pattern
- Parallel agent execution
- Agent communication and shared state
- When multi-agent is worth it (and when it is not)
- CrewAI: higher-level multi-agent orchestration

**Resources:**
| Resource | Time |
|---|---|
| [CrewAI Docs](https://docs.crewai.com/) | 1 week |
| [LangGraph multi-agent docs](https://langchain-ai.github.io/langgraph/concepts/multi_agent/) | 1 week |

---

### [05 - MCP: Model Context Protocol](./05-mcp/)

Anthropic's open standard for connecting LLMs to tools and data sources. Already in job descriptions. The direction the industry is moving for tool connectivity.

**Topics:**
- What MCP is and why it matters
- MCP architecture: hosts, clients, servers
- Building an MCP server that exposes tools
- Connecting an MCP server to Claude
- Available MCP servers: filesystem, databases, GitHub, Slack, web

**Resources:**
| Resource | Time |
|---|---|
| [MCP official docs](https://modelcontextprotocol.io/) | 1 week |
| [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) | 3 days |
| [MCP server examples](https://github.com/modelcontextprotocol/servers) | 3 days |

---

## The agentic ecosystem

You do not need to know all of these. Know LangChain and LangGraph well, that is where 39.9% of job postings point. Know the others well enough to recognize when one fits better than another.

### LangChain + LangGraph
The most widely used agentic stack. LangChain provides the building blocks: chains, retrievers, tool wrappers, memory. LangGraph adds stateful agent graphs with branching, looping, checkpointing, and human-in-the-loop.

- [LangChain Docs](https://python.langchain.com/docs/introduction/) - components, integrations, LCEL
- [LangGraph Docs](https://langchain-ai.github.io/langgraph/) - stateful agents, the main framework for production agents
- [LangChain blog](https://blog.langchain.dev/) - agentic patterns as they emerge

### LlamaIndex
Focused on data connectivity. The better choice when the core challenge is getting data into the LLM accurately. Stronger than LangChain for complex document parsing, structured knowledge graphs, and production RAG pipelines.

- [LlamaIndex Docs](https://docs.llamaindex.ai/)

### CrewAI
High-level multi-agent framework. You define agents with roles, tools, and goals, then hand tasks to a crew. Much less code for coordinator-specialist patterns than writing raw LangGraph.

- [CrewAI Docs](https://docs.crewai.com/)

### AutoGen (Microsoft)
Multi-agent conversation framework where agents talk to each other to solve tasks. Good for research and complex multi-agent interactions. Strong community and Microsoft backing.

- [AutoGen Docs](https://microsoft.github.io/autogen/)

### Pydantic AI
Agent framework built on top of Pydantic. Strongly typed, easy to test, good for single-agent apps where type safety is a priority. Newer but growing quickly.

- [Pydantic AI Docs](https://ai.pydantic.dev/)

### Haystack
Production-focused RAG and agent framework by deepset. Strong on pipelines, evaluation, and enterprise features. A solid alternative to LlamaIndex when built-in evaluation tooling matters.

- [Haystack Docs](https://docs.haystack.deepset.ai/)

### Semantic Kernel (Microsoft)
Enterprise SDK for .NET, Python, and Java. Shows up in Microsoft-heavy environments. Plugin architecture maps well to MCP concepts.

- [Semantic Kernel Docs](https://learn.microsoft.com/en-us/semantic-kernel/)

### Agno (formerly Phidata)
Lightweight agent framework with memory, storage, and knowledge built in. Good for moving fast with minimal boilerplate.

- [Agno Docs](https://docs.agno.com/)

### ADK - Agent Development Kit (Google)
Google's open-source framework for building multi-agent systems. Model-agnostic but optimized for Gemini. Deploys natively to Vertex AI Agent Engine. ADK agents work with A2A (Agent-to-Agent protocol), Google's answer to MCP for agent interoperability.

- [ADK Docs](https://google.github.io/adk-docs/)
- [ADK GitHub](https://github.com/google/adk-python)
- [A2A Protocol](https://google.github.io/A2A/)

### Which one to pick

| Situation | Use |
|---|---|
| Job market signal, general agents | LangGraph |
| Complex document pipelines and RAG | LlamaIndex |
| Multi-agent without writing graph code | CrewAI |
| Strongly typed, testable, single agent | Pydantic AI |
| Microsoft/enterprise environment | Semantic Kernel or AutoGen |
| Google Cloud / Gemini ecosystem | ADK |

---

## Phase project

**Research agent with RAG and MCP**

An agent that takes a research question, retrieves relevant chunks from a document collection with RAG, uses MCP-connected tools (web search, file system), and produces a structured report with citations.

Stack: LangGraph, ChromaDB, MCP, Claude/OpenAI  
Project folder: [`04-multi-agent/project/`](./04-multi-agent/project/)

---

## Phase checklist

- [ ] Built a RAG pipeline and measured faithfulness > 0.8 with RAGAS
- [ ] Implemented a ReAct agent from scratch without a framework
- [ ] Built a stateful LangGraph agent with at least 3 tools and conditional routing
- [ ] Agent loops, retries on failure, and stops when the goal is met
- [ ] Multi-agent system with coordinator delegating to 2+ specialists
- [ ] Built or connected an MCP server

Next: [Phase 4 - Production](../phase-4-production/)
