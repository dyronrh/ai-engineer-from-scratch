# Phase 3 · Advanced AI

> This is where real engineering begins.

**Estimated duration:** 6–10 weeks  
**Prerequisite:** Phase 2 complete — especially LLM Engineering

---

## What you'll be able to do after this phase

- Design and build RAG systems that actually work (not just tutorials)
- Create stateful AI agents with memory and tools
- Understand when and how to fine-tune a model
- Complete the phase project: a multi-document research agent

---

## Modules

### [01 · RAG Systems](./01-rag-systems/)

Retrieval-Augmented Generation: making LLMs work with your own data.

**Topics:**
- Embeddings: what they are, how to pick the right model
- Vector databases: Chroma, Pinecone, Weaviate, pgvector
- Basic RAG pipeline: chunk → embed → store → retrieve → generate
- Advanced RAG: HyDE, reranking, hybrid search
- RAG evaluation: context relevance, faithfulness, answer relevance

**Resources:**
| Resource | Time |
|---|---|
| [Pinecone Learning Center](https://www.pinecone.io/learn/) | 1 week |
| [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings) | 3 days |
| [LlamaIndex Docs](https://docs.llamaindex.ai/) | 2 weeks |

---

### [02 · AI Agents](./02-ai-agents/)

Agents that plan, use tools, and adapt. Not chatbots with if/else.

**Topics:**
- ReAct pattern: Reason → Act → Observe
- LangGraph: state graphs for complex agents
- Tools: web search, code execution, external APIs
- Memory: short-term (context window), long-term (vector store)
- Multi-agent: coordination, communication, specialization
- MCP — Model Context Protocol: Anthropic's standard for connecting tools

**Resources:**
| Resource | Time |
|---|---|
| [LangGraph Docs](https://langchain-ai.github.io/langgraph/) | 2 weeks |
| [CrewAI Docs](https://docs.crewai.com/) | 1 week |
| [Anthropic MCP Docs](https://modelcontextprotocol.io/) | 1 week |
| [AutoGen GitHub](https://github.com/microsoft/autogen) | 1 week |

---

### [03 · Fine-tuning](./03-fine-tuning/)

When fine-tuning makes sense (less often than you think) and how to do it right.

**Topics:**
- Fine-tuning vs. prompt engineering vs. RAG — when to use each
- LoRA and QLoRA: efficient fine-tuning on modest hardware
- Dataset curation: quality over quantity
- Evaluating fine-tuned models
- Tools: HuggingFace PEFT, Axolotl, Unsloth

**Resources:**
| Resource | Time |
|---|---|
| [HuggingFace PEFT](https://huggingface.co/docs/peft/index) | 2 weeks |
| [Argilla Docs](https://docs.argilla.io/) | 1 week |
| [Eleuther LM Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) | 1 week |

---

## Phase project

**Research agent with RAG**

An agent that takes a question, searches for relevant information across a document collection using RAG, and generates a structured report with sources.

**Stack:** Python · LangGraph · ChromaDB · OpenAI or Claude  
**Demonstrates:** Stateful agents · RAG pipeline · Planning · Source citation

Project folder: [`02-ai-agents/project/`](./02-ai-agents/project/)

---

## Phase checklist

- [ ] Built a RAG pipeline that evaluates faithfulness and relevance
- [ ] Implemented an agent with tools using LangGraph
- [ ] Understand when to use multi-agent and when not to
- [ ] Fine-tuned some model (even a small one)
- [ ] The research agent generates reports with cited sources

Next: [Phase 4 · Production](../phase-4-production/)
