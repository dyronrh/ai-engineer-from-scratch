# Phase 3 - Agentic AI

**Duration:** 6-8 weeks  
**Prerequisite:** Phase 2 done — you can call LLM APIs and use tool/function calling

---

## Why this phase matters more than any other

The numbers from real job postings:

- AI Agents: **980% job posting growth** from 2023 to 2024
- LangGraph/LangChain: in **39.9% of all agentic AI engineering roles**
- RAG: **dominant production use case** across every company size
- MCP: the emerging standard that's already showing up in job descriptions
- Agentic AI engineers earn **15-20% more** than standard AI engineers

This is where the market is right now. Companies are not hiring for ML theory — they're hiring for people who can build systems that plan, retrieve, act, and loop until the job is done.

---

## Modules

### [01 - RAG Systems](./01-rag-systems/)

Retrieval-Augmented Generation. The most deployed production pattern for LLM applications. Every company that builds on LLMs and has their own data needs this.

**Topics:**
- Embeddings: picking the right model, understanding similarity
- Vector databases: Chroma (local), Pinecone (managed), pgvector (Postgres)
- Basic RAG pipeline: chunk, embed, store, retrieve, generate
- Advanced RAG: HyDE, reranking with cross-encoders, hybrid search
- Evaluating RAG: faithfulness, context relevance, answer quality with RAGAS

**Resources:**
| Resource | Time |
|---|---|
| [Pinecone Learning Center](https://www.pinecone.io/learn/) | 1 week |
| [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings) | 2 days |
| [LlamaIndex Docs](https://docs.llamaindex.ai/) | 1 week |
| [RAGAS Docs](https://docs.ragas.io/) | 3 days |

---

### [02 - Agentic Patterns](./02-agentic-patterns/)

The design patterns that make agents work. These are recurring solutions to recurring problems. Learn the patterns before learning the frameworks.

**Patterns to know:**
- **ReAct** (Reason + Act): think, then act, then observe, then think again
- **Planning**: break a goal into steps before executing
- **Reflection**: evaluate your own output and try again if it's wrong
- **Tool use**: let the model decide when to call external tools
- **Memory**: short-term (conversation), long-term (vector store), episodic

**Resources:**
| Resource | Time |
|---|---|
| [ReAct paper](https://arxiv.org/abs/2210.03629) | 2 days |
| [LangGraph conceptual guides](https://langchain-ai.github.io/langgraph/concepts/) | 1 week |

---

### [03 - LangGraph](./03-langgraph/)

The framework for building stateful, controllable agents. In 39.9% of agentic AI job postings. Build agents that can branch, loop, retry, and coordinate — not just chain prompts linearly.

**Topics:**
- State graphs: nodes, edges, conditional routing
- Checkpointing and resuming agent runs
- Human-in-the-loop: pause and wait for approval
- Streaming agent outputs
- Subgraphs and modular agent design

**Resources:**
| Resource | Time |
|---|---|
| [LangGraph Docs](https://langchain-ai.github.io/langgraph/) | 2 weeks |
| [LangGraph tutorials](https://langchain-ai.github.io/langgraph/tutorials/) | 1 week |

---

### [04 - Multi-Agent Systems](./04-multi-agent/)

One agent can't do everything well. Multi-agent systems have a coordinator delegate to specialists — each focused, each tool-equipped.

**Topics:**
- Coordinator + specialist pattern
- Parallel agent execution
- Agent communication and shared state
- When multi-agent helps (and when it's overkill)
- CrewAI: higher-level multi-agent orchestration

**Resources:**
| Resource | Time |
|---|---|
| [CrewAI Docs](https://docs.crewai.com/) | 1 week |
| [LangGraph multi-agent docs](https://langchain-ai.github.io/langgraph/concepts/multi_agent/) | 1 week |

---

### [05 - MCP: Model Context Protocol](./05-mcp/)

Anthropic's open standard for connecting LLMs to tools and data sources. Already showing up in job descriptions. Will likely become the standard interface layer for agentic systems.

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

You don't need all of these. Know LangChain/LangGraph deeply - that's where 39.9% of job postings point. Know the others well enough to pick the right tool for a given situation.

### LangChain + LangGraph
The most widely used agentic stack. LangChain provides the building blocks (chains, retrievers, tool wrappers, memory). LangGraph adds stateful agent graphs with branching, looping, checkpointing, and human-in-the-loop.

- [LangChain Docs](https://python.langchain.com/docs/introduction/) - components, integrations, LCEL
- [LangGraph Docs](https://langchain-ai.github.io/langgraph/) - stateful agents, the main framework for production agents
- [LangChain blog](https://blog.langchain.dev/) - agentic patterns as they emerge

### LlamaIndex
Focused on data connectivity - the best choice when the core challenge is getting data into the LLM accurately. Stronger than LangChain for complex document parsing, structured knowledge graphs, and production RAG pipelines.

- [LlamaIndex Docs](https://docs.llamaindex.ai/)

### CrewAI
High-level multi-agent framework. You define agents with roles, tools, and goals, then define tasks and hand them to a crew. Less code for coordinator-specialist patterns than writing raw LangGraph.

- [CrewAI Docs](https://docs.crewai.com/)

### AutoGen (Microsoft)
Multi-agent conversation framework. Agents talk to each other to solve tasks. Good for research and exploration of complex multi-agent interactions. Strong community and Microsoft backing.

- [AutoGen Docs](https://microsoft.github.io/autogen/)

### Pydantic AI
Agent framework built on top of Pydantic. Strongly typed, test-friendly, straightforward for single-agent apps where type safety matters. Newer but growing quickly.

- [Pydantic AI Docs](https://ai.pydantic.dev/)

### Haystack
Production-focused RAG and agent framework by deepset. Strong on pipelines, evaluation, and enterprise features. Good alternative to LlamaIndex when you need built-in evaluation tooling.

- [Haystack Docs](https://docs.haystack.deepset.ai/)

### Semantic Kernel (Microsoft)
Enterprise-focused SDK for .NET, Python, and Java. If you're working in enterprise environments - especially Microsoft stack - this shows up. Plugin architecture aligns well with MCP concepts.

- [Semantic Kernel Docs](https://learn.microsoft.com/en-us/semantic-kernel/)

### Agno (formerly Phidata)
Lightweight agent framework. Good for building agents fast with minimal boilerplate. Memory, storage, and knowledge built in.

- [Agno Docs](https://docs.agno.com/)

### ADK - Agent Development Kit (Google)
Google's open-source framework for building multi-agent systems. Model-agnostic but optimized for Gemini. Strong on agent composition, built-in evaluation, and deployment to Google Cloud (Vertex AI Agent Engine). ADK agents are natively compatible with A2A (Agent-to-Agent protocol), Google's answer to MCP for agent interoperability.

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

An agent that takes a research question, retrieves relevant chunks from a document collection with RAG, uses MCP-connected tools (web search, file system), and generates a structured report with citations.

Stack: LangGraph, ChromaDB, MCP, Claude/OpenAI  
Project folder: [`04-multi-agent/project/`](./04-multi-agent/project/)

---

## Phase checklist

- [ ] Built a RAG pipeline and measured faithfulness > 0.8 with RAGAS
- [ ] Implemented a ReAct agent from scratch (no framework) to understand the pattern
- [ ] Built a stateful LangGraph agent with at least 3 tools and conditional routing
- [ ] Agent can loop, retry on failure, and stop when the goal is met
- [ ] Multi-agent system with coordinator delegating to 2+ specialists
- [ ] Built or connected an MCP server

Next: [Phase 4 - Production](../phase-4-production/)
