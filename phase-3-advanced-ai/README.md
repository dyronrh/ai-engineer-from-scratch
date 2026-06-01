# Phase 3 - Advanced AI

**Estimated duration:** 6-10 weeks  
**Prerequisite:** Phase 2 done, especially LLM Engineering

---

## Market context for this phase

This phase covers the two skills with the highest demand growth in the entire AI engineer job market:

**RAG systems** are the dominant production use case in 2024-2025. Nearly every company that builds on LLMs needs RAG. It's not a nice-to-have anymore.

**AI Agents** saw 980% job posting growth from 2023 to 2024. LangGraph and LangChain appear in 39.9% of all agentic AI engineering roles. Agentic AI engineers earn 15-20% more than standard AI engineers on average.

Fine-tuning is useful to understand, but most companies reach for RAG and prompt engineering before fine-tuning. Know how it works, but don't spend 6 weeks on it before you can build a working agent.

---

## Modules

### [01 - RAG Systems](./01-rag-systems/) — highest priority

Retrieval-Augmented Generation: making LLMs work with your own data. This is what most companies actually want when they say they're building an AI product.

**Topics:**
- Embeddings: what they are, how to choose the right model
- Vector databases: Chroma (free, local), Pinecone (managed), pgvector (postgres)
- Basic RAG pipeline: chunk, embed, store, retrieve, generate
- Advanced RAG: HyDE, reranking, hybrid search
- Evaluating RAG: context relevance, faithfulness, answer quality

**Resources:**
| Resource | Time |
|---|---|
| [Pinecone Learning Center](https://www.pinecone.io/learn/) | 1 week |
| [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings) | 3 days |
| [LlamaIndex Docs](https://docs.llamaindex.ai/) | 2 weeks |

---

### [02 - AI Agents](./02-ai-agents/) — highest priority

Agents that plan, use tools, loop until a goal is met, and coordinate with other agents. Not chatbots. Real systems that do things.

**Topics:**
- ReAct pattern: Reason, Act, Observe
- LangGraph: stateful agent workflows with branching and loops
- Tools: web search, code execution, database queries, external APIs
- Memory: short-term (context window), long-term (vector store)
- Multi-agent systems: coordinator and specialist agents
- MCP - Model Context Protocol: Anthropic's open standard for tool connectivity

**Resources:**
| Resource | Time |
|---|---|
| [LangGraph Docs](https://langchain-ai.github.io/langgraph/) | 2 weeks |
| [CrewAI Docs](https://docs.crewai.com/) | 1 week |
| [Anthropic MCP Docs](https://modelcontextprotocol.io/) | 1 week |
| [AutoGen GitHub](https://github.com/microsoft/autogen) | 1 week |

---

### [03 - Fine-tuning](./03-fine-tuning/) — medium priority

When to fine-tune vs when to use RAG vs when to just fix your prompt. This skill differentiates strong candidates, but most production systems never actually need it. Learn it after RAG and Agents.

**Topics:**
- When fine-tuning is the right call (and when it isn't)
- LoRA and QLoRA: fine-tuning on consumer hardware
- Building a training dataset: quality beats quantity
- Evaluating fine-tuned models properly
- HuggingFace PEFT, Axolotl, Unsloth

**Resources:**
| Resource | Time |
|---|---|
| [HuggingFace PEFT](https://huggingface.co/docs/peft/index) | 2 weeks |
| [Argilla Docs](https://docs.argilla.io/) | 1 week |
| [Eleuther LM Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) | 1 week |

---

## Phase project

**Research agent with RAG**

An agent that takes a question, searches a document collection with RAG, and generates a structured report with cited sources. This is the kind of system that gets you interviews.

**Stack:** Python, LangGraph, ChromaDB, OpenAI or Claude  
**Demonstrates:** Stateful agents, RAG pipeline, planning, source attribution

Project folder: [`02-ai-agents/project/`](./02-ai-agents/project/)

---

## Phase checklist

- [ ] Built a RAG pipeline and measured faithfulness and relevance
- [ ] Implemented an agent with at least 3 tools using LangGraph
- [ ] Can explain the tradeoff between RAG, fine-tuning, and prompt engineering
- [ ] Multi-agent setup where one agent delegates to others
- [ ] Research agent produces reports with traceable sources

Next: [Phase 4 - Production](../phase-4-production/)
