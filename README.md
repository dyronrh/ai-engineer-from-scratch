# ai-engineer-from-scratch

A practical, market-driven path to becoming an AI Engineer. Built from real job postings, not theory.

This is not another "learn ML from scratch" course. It's the shortest path to the skills companies are actually hiring for right now — based on analysis of thousands of job postings from Amazon, Meta, Google, NVIDIA, and hundreds of startups.

**Estimated time:** 6 to 12 months at 10-15 hours per week  
**Cost:** 100% free resources  
**Outcome:** Ship AI systems in production. Get hired.

---

## What the job market actually wants (2024-2025)

Before starting, look at what appears in real job postings:

| Skill | Frequency in job postings |
|---|---|
| Python | 82% of all AI engineer postings |
| PyTorch or TensorFlow | 37-38% |
| LangChain / LangGraph | 39.9% of agentic AI roles |
| Docker / Kubernetes | 15-17% |
| RAG systems | Dominant production use case |
| AI Agents | 980% growth from 2023 to 2024 |
| FastAPI | 1,700+ active job listings combining it with AI |
| SQL | 17% |

**What about math?** Linear algebra, calculus, and statistics are listed explicitly in fewer than 20% of AI Engineer postings. They matter more for ML Engineers (who train models from scratch). For AI Engineers — who build systems on top of pre-trained models — Python and production skills matter far more. Math is in this roadmap, but compressed and made optional for people targeting pure AI Engineer roles.

**The role split:**

| Role | What they do | Math needed |
|---|---|---|
| **AI Engineer** | Integrates pre-trained models into products | Low to medium |
| **ML Engineer** | Trains models from scratch | High |
| **LLM Engineer** | Builds LLM-powered apps (RAG, agents) | Low |

This roadmap targets **AI Engineer and LLM Engineer** roles, where the market is growing fastest.

---

## The full map

The interactive roadmap diagram is in [`roadmap.excalidraw`](./roadmap.excalidraw).  
Open it with the [Excalidraw VS Code extension](https://marketplace.visualstudio.com/items?itemName=pomdtr.excalidraw-editor) or import it at [excalidraw.com](https://excalidraw.com).

```
Start
   |
   v
Phase 1 - Foundations (4-6 weeks)
  Python for AI · Math basics · ML fundamentals
   |
   v
Phase 2 - AI Core (6-10 weeks)
  Deep Learning · NLP & Transformers · LLM Engineering
   |
   v
Phase 3 - Advanced AI (6-10 weeks)
  RAG Systems · AI Agents · Fine-tuning
   |
   v
Phase 4 - Production (4-6 weeks)
  MLOps · Deployment · Observability
   |
   v
  AI Engineer
```

---

## Who is this for

| Profile | Where to start |
|---|---|
| Complete beginner | Phase 1 from the top |
| Developer switching to AI | Phase 2 - you already have the Python base |
| Data Scientist leveling up | Phase 3 - Agents and RAG are where the jobs are |
| Already using LLM APIs | Phase 4 - learn to ship things that don't break |

---

## Repository structure

```
ai-engineer-from-scratch/
├── README.md
├── roadmap.excalidraw
│
├── phase-1-foundations/
│   ├── README.md
│   ├── 01-python-for-ai/         <- highest priority
│   ├── 02-math-and-stats/        <- useful, not blocking
│   └── 03-ml-fundamentals/
│
├── phase-2-ai-core/
│   ├── README.md
│   ├── 01-deep-learning/
│   ├── 02-nlp-and-transformers/
│   └── 03-llm-engineering/       <- highest priority
│
├── phase-3-advanced-ai/
│   ├── README.md
│   ├── 01-rag-systems/           <- most demanded production skill
│   ├── 02-ai-agents/             <- 980% job growth
│   └── 03-fine-tuning/
│
├── phase-4-production/
│   ├── README.md
│   ├── 01-mlops/
│   ├── 02-deployment/
│   └── 03-observability/
│
└── final-project/
    └── README.md
```

---

## Phase 1 - Foundations

Folder: [`phase-1-foundations/`](./phase-1-foundations/)

### Python for AI (priority: critical)
| Topic | Free resource | Time |
|---|---|---|
| Async/await for APIs | [Real Python - Async IO](https://realpython.com/async-io-python/) | 1 week |
| OOP and type hints | [Python Docs](https://docs.python.org/3/library/typing.html) | 3 days |
| NumPy, Pandas, Matplotlib | [Kaggle Learn](https://www.kaggle.com/learn) | 1 week |

### Math and Statistics (priority: useful, not blocking for AI Engineer roles)
| Topic | Free resource | Time |
|---|---|---|
| Linear Algebra basics | [3Blue1Brown - Essence of LA](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) | 1 week |
| Calculus for backprop | [3Blue1Brown - Calculus](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) | 1 week |
| Probability and Stats | [StatQuest YouTube](https://www.youtube.com/@statquest) | 1 week |

> If your goal is AI Engineer or LLM Engineer, you can move faster through math and come back to it later. If you want to become an ML Engineer who trains models from scratch, invest more time here.

### ML Fundamentals (priority: medium - gives you context)
| Topic | Free resource | Time |
|---|---|---|
| Core ML concepts | [Andrew Ng - ML Specialization](https://www.coursera.org/specializations/machine-learning-introduction) | 3 weeks |
| Scikit-learn hands-on | [Scikit-learn docs](https://scikit-learn.org/stable/tutorial/index.html) | 1 week |

---

## Phase 2 - AI Core

Folder: [`phase-2-ai-core/`](./phase-2-ai-core/)

### Deep Learning (priority: high - understanding beats memorizing)
| Topic | Free resource | Time |
|---|---|---|
| Neural networks from scratch | [fast.ai Practical DL](https://course.fast.ai/) | 3 weeks |
| PyTorch fundamentals | [PyTorch official tutorial](https://pytorch.org/tutorials/) | 1 week |

### NLP and Transformers (priority: high - this is the foundation of everything)
| Topic | Free resource | Time |
|---|---|---|
| Attention mechanism | [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | 2 days |
| HuggingFace Transformers | [HuggingFace Course](https://huggingface.co/learn/nlp-course/chapter1/1) | 2 weeks |
| Building LLMs from scratch | [Andrej Karpathy - makemore](https://github.com/karpathy/makemore) | 1 week |

### LLM Engineering (priority: critical - appears in 80%+ of AI engineer job postings)
| Topic | Free resource | Time |
|---|---|---|
| OpenAI API + function calling | [OpenAI Cookbook](https://cookbook.openai.com/) | 1 week |
| Anthropic Claude API | [Anthropic Docs](https://docs.anthropic.com/) | 3 days |
| Open source LLMs with Ollama | [Ollama docs](https://ollama.com/docs) | 3 days |
| Prompt Engineering | [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) | 1 week |

---

## Phase 3 - Advanced AI

Folder: [`phase-3-advanced-ai/`](./phase-3-advanced-ai/)

### RAG Systems (priority: critical - dominant production use case in 2024-2025)
| Topic | Free resource | Time |
|---|---|---|
| Vector databases | [Pinecone Learning Center](https://www.pinecone.io/learn/) | 1 week |
| Embeddings deep dive | [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings) | 3 days |
| Advanced RAG (HyDE, reranking) | [LlamaIndex Docs](https://docs.llamaindex.ai/) | 2 weeks |

### AI Agents (priority: critical - 980% job growth, 39.9% of postings mention LangGraph/LangChain)
| Topic | Free resource | Time |
|---|---|---|
| LangGraph - stateful agents | [LangGraph Docs](https://langchain-ai.github.io/langgraph/) | 2 weeks |
| Multi-agent systems with CrewAI | [CrewAI Docs](https://docs.crewai.com/) | 1 week |
| MCP - Model Context Protocol | [Anthropic MCP Docs](https://modelcontextprotocol.io/) | 1 week |

### Fine-tuning (priority: medium - useful to understand, rarely needed in practice)
| Topic | Free resource | Time |
|---|---|---|
| LoRA and QLoRA | [HuggingFace PEFT](https://huggingface.co/docs/peft/index) | 2 weeks |
| Dataset curation | [Argilla Docs](https://docs.argilla.io/) | 1 week |

---

## Phase 4 - Production

Folder: [`phase-4-production/`](./phase-4-production/)

### MLOps
| Topic | Free resource | Time |
|---|---|---|
| Experiment tracking with MLflow | [MLflow Docs](https://mlflow.org/docs/latest/index.html) | 1 week |
| Data versioning with DVC | [DVC Docs](https://dvc.org/doc) | 3 days |
| CI/CD with GitHub Actions | [GitHub Actions Docs](https://docs.github.com/en/actions) | 1 week |

### Deployment (priority: high - Docker/Kubernetes in 15-17% of all postings)
| Topic | Free resource | Time |
|---|---|---|
| FastAPI for AI APIs | [FastAPI Docs](https://fastapi.tiangolo.com/) | 1 week |
| Docker + Kubernetes | [Play with Docker](https://labs.play-with-docker.com/) | 2 weeks |
| Cloud deployment (AWS/GCP) | [AWS Free Tier](https://aws.amazon.com/free/) | 2 weeks |

### Observability and Safety
| Topic | Free resource | Time |
|---|---|---|
| LLM monitoring with Langfuse | [Langfuse Docs](https://langfuse.com/docs) | 3 days |
| Guardrails and evals | [RAGAS](https://docs.ragas.io/) and [DeepEval](https://docs.confident-ai.com/) | 1 week |
| AI security basics | [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | 3 days |

---

## Final Project

The capstone. Folder: [`final-project/`](./final-project/)

Build a **multi-agent research assistant** that demonstrates everything: RAG, agents, production API, monitoring. This is what hiring managers at mid-size companies and startups want to see — something real and deployed, not a notebook.

---

## Essential free resources

| Resource | Why it matters |
|---|---|
| [fast.ai](https://fast.ai) | Best practical deep learning course, free |
| [DeepLearning.AI](https://www.deeplearning.ai/courses/) | Short courses on LLMs, RAG and Agents by Andrew Ng |
| [HuggingFace Learn](https://huggingface.co/learn) | Hands-on NLP, diffusion and agents |
| [Andrej Karpathy YouTube](https://www.youtube.com/@AndrejKarpathy) | Build LLMs from scratch |
| [The Batch](https://www.deeplearning.ai/the-batch/) | Weekly AI newsletter |

---

## Contributing

Found a better resource, a missing topic, or a broken link?

1. Fork the repo
2. Create a branch: `git checkout -b add/your-topic`
3. Open a Pull Request

---

MIT License - free to use, share and adapt.
