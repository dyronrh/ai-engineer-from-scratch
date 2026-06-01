# ai-engineer-from-scratch

A practical path to becoming an AI Engineer in the agentic era. Built from what companies are actually hiring for right now.

Not another "learn ML from scratch" repo. The job market shifted. Companies are not hiring people to train models — they hire people who can build systems that use them. Agents, RAG, MCP, production APIs. That's the stack.

**Time:** 6-9 months at 10-15 hours per week  
**Cost:** 100% free resources  
**Target roles:** AI Engineer, LLM Engineer, Agentic AI Engineer

---

## What the market wants (2024-2025 job data)

| Skill | Signal |
|---|---|
| Python | 82% of all AI Engineer postings |
| LangChain / LangGraph | 39.9% of agentic AI roles |
| RAG systems | Dominant production use case across all company sizes |
| AI Agents | 980% job posting growth from 2023 to 2024 |
| FastAPI + Docker | 1,700+ active postings combining AI with these tools |
| MCP (Model Context Protocol) | Emerging standard — already in job descriptions |

**What the market does NOT care about as much:**
- Math (linear algebra, calculus) — explicit in <20% of AI Engineer postings
- Training models from scratch — that's ML Engineer, a different and narrower role
- Deep learning theory — useful context, not a hiring requirement

This roadmap targets AI Engineer and LLM Engineer roles, where demand is growing fastest.

---

## The full map

Interactive diagram: [`roadmap.excalidraw`](./roadmap.excalidraw)  
Open with the [Excalidraw VS Code extension](https://marketplace.visualstudio.com/items?itemName=pomdtr.excalidraw-editor) or at [excalidraw.com](https://excalidraw.com).

```
Start
   |
   v
Phase 1 - Python for AI (2-4 weeks)
  The language everything runs on

   |
   v
Phase 2 - LLM Engineering (4-6 weeks)
  APIs, prompt engineering, tool use

   |
   v
Phase 3 - Agentic AI (6-8 weeks)  <-- where most of the hiring is
  RAG · Agents · Agentic Patterns · MCP

   |
   v
Phase 4 - Production (4-6 weeks)
  FastAPI · Docker · Monitoring

   |
   v
  AI Engineer
```

---

## Who is this for

| Profile | Where to start |
|---|---|
| Complete beginner | Phase 1, work through it fully |
| Developer switching to AI | Phase 2 - you have the Python, skip Phase 1 |
| Already using LLM APIs | Phase 3 - agentic patterns are where the gap usually is |
| Building agents but not shipping them | Phase 4 |

---

## Repository structure

```
ai-engineer-from-scratch/
├── README.md
├── roadmap.excalidraw
│
├── phase-1-python-for-ai/          <- foundation, 2-4 weeks
│   └── README.md
│
├── phase-2-llm-engineering/        <- APIs, prompts, tool use
│   ├── README.md
│   ├── 01-how-llms-work/
│   ├── 02-api-and-tool-use/
│   └── 03-prompt-engineering/
│
├── phase-3-agentic-ai/             <- where the jobs are
│   ├── README.md
│   ├── 01-rag-systems/
│   ├── 02-agentic-patterns/
│   ├── 03-langgraph/
│   ├── 04-multi-agent/
│   └── 05-mcp/
│
├── phase-4-production/
│   ├── README.md
│   ├── 01-fastapi/
│   ├── 02-docker-and-deployment/
│   └── 03-monitoring/
│
└── final-project/
    └── README.md
```

---

## Phase 1 - Python for AI

Folder: [`phase-1-python-for-ai/`](./phase-1-python-for-ai/)

**Duration:** 2-4 weeks  
**What you need to be able to do:** write async, typed Python and call HTTP APIs confidently.

| Topic | Free resource | Time |
|---|---|---|
| Async/await | [Real Python - Async IO](https://realpython.com/async-io-python/) | 1 week |
| OOP and type hints | [Python Docs - typing](https://docs.python.org/3/library/typing.html) | 3 days |
| HTTP APIs with httpx | [HTTPX Docs](https://www.python-httpx.org/) | 2 days |
| JSON, environment variables, .env files | [python-dotenv](https://pypi.org/project/python-dotenv/) | 1 day |
| Pandas basics for data handling | [Kaggle Learn - Pandas](https://www.kaggle.com/learn/pandas) | 3 days |

Skip if: you already write async Python at work.

---

## Phase 2 - LLM Engineering

Folder: [`phase-2-llm-engineering/`](./phase-2-llm-engineering/)

**Duration:** 4-6 weeks  
**What you need to be able to do:** call any LLM API, use tool/function calling, write prompts that work, run models locally.

| Topic | Free resource | Time |
|---|---|---|
| How LLMs work (conceptual) | [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | 2 days |
| HuggingFace for inference | [HuggingFace Course Ch. 1-3](https://huggingface.co/learn/nlp-course/chapter1/1) | 1 week |
| OpenAI API + function calling | [OpenAI Cookbook](https://cookbook.openai.com/) | 1 week |
| Anthropic Claude API + tool use | [Anthropic Docs](https://docs.anthropic.com/) | 3 days |
| Local models with Ollama | [Ollama docs](https://ollama.com/docs) | 2 days |
| Prompt engineering | [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) | 1 week |

---

## Phase 3 - Agentic AI

Folder: [`phase-3-agentic-ai/`](./phase-3-agentic-ai/)

**Duration:** 6-8 weeks  
**This is the core of the roadmap.** RAG and agents are what most companies are building right now. LangGraph appears in 39.9% of agentic job postings. MCP is the emerging standard for tool connectivity.

### RAG Systems
| Topic | Free resource | Time |
|---|---|---|
| Embeddings and vector databases | [Pinecone Learning Center](https://www.pinecone.io/learn/) | 1 week |
| RAG pipeline from scratch | [LlamaIndex Docs](https://docs.llamaindex.ai/) | 1 week |
| Advanced RAG (reranking, HyDE) | [LlamaIndex Advanced RAG](https://docs.llamaindex.ai/en/stable/optimizing/advanced_retrieval/) | 1 week |
| Evaluating RAG with RAGAS | [RAGAS Docs](https://docs.ragas.io/) | 3 days |

### Agentic Patterns
| Topic | Free resource | Time |
|---|---|---|
| ReAct pattern | [Original ReAct paper](https://arxiv.org/abs/2210.03629) | 2 days |
| Planning and reflection patterns | [LangGraph Docs](https://langchain-ai.github.io/langgraph/) | 1 week |
| LangGraph - stateful agents | [LangGraph Tutorials](https://langchain-ai.github.io/langgraph/tutorials/) | 2 weeks |
| Multi-agent systems with CrewAI | [CrewAI Docs](https://docs.crewai.com/) | 1 week |
| MCP - Model Context Protocol | [MCP Docs](https://modelcontextprotocol.io/) | 1 week |

---

## Phase 4 - Production

Folder: [`phase-4-production/`](./phase-4-production/)

**Duration:** 4-6 weeks  
**What you need:** FastAPI + Docker is in 1,700+ active AI engineer job postings. Without this, you can build demos but not ship products.

| Topic | Free resource | Time |
|---|---|---|
| FastAPI for AI APIs | [FastAPI Docs](https://fastapi.tiangolo.com/) | 1 week |
| Docker and Docker Compose | [Play with Docker](https://labs.play-with-docker.com/) | 1 week |
| Deployment to cloud (AWS/GCP) | [AWS Free Tier](https://aws.amazon.com/free/) | 1 week |
| Experiment tracking with MLflow | [MLflow Docs](https://mlflow.org/docs/latest/index.html) | 3 days |
| LLM monitoring with Langfuse | [Langfuse Docs](https://langfuse.com/docs) | 3 days |
| Guardrails and eval pipelines | [RAGAS](https://docs.ragas.io/) + [DeepEval](https://docs.confident-ai.com/) | 1 week |

---

## Final Project

Folder: [`final-project/`](./final-project/)

A **multi-agent research assistant** with RAG, deployed as a FastAPI service with Langfuse monitoring. Every component from the roadmap in one real system.

---

## Essential resources

| Resource | Why |
|---|---|
| [fast.ai](https://fast.ai) | Best practical deep learning course if you want ML depth |
| [DeepLearning.AI short courses](https://www.deeplearning.ai/courses/) | RAG, agents, LLMs by Andrew Ng - free |
| [HuggingFace Learn](https://huggingface.co/learn) | Transformers, pipelines, hands-on |
| [Andrej Karpathy YouTube](https://www.youtube.com/@AndrejKarpathy) | How LLMs actually work under the hood |
| [LangChain blog](https://blog.langchain.dev/) | Agentic patterns as they emerge |
| [The Batch](https://www.deeplearning.ai/the-batch/) | Weekly AI news |

---

## Contributing

Found a better resource or a missing topic? Open a PR.

1. Fork the repo
2. `git checkout -b add/your-topic`
3. Open a Pull Request

---

MIT License
