# ai-engineer-from-scratch

A real, no-nonsense path to becoming an AI Engineer — from zero to production.

This is the guide I wish I had when I started. Each phase has free resources, exercises, and a concrete project. No shortcuts, but a clear order.

**Estimated time:** 6 to 12 months at 10–15 hours per week  
**Cost:** 100% free resources available  
**Outcome:** Able to design, build and deploy AI systems in production

---

## The full map

The interactive roadmap diagram is in [`roadmap.excalidraw`](./roadmap.excalidraw).  
Open it with the [Excalidraw VS Code extension](https://marketplace.visualstudio.com/items?itemName=pomdtr.excalidraw-editor) or at [excalidraw.com](https://excalidraw.com) by importing the file.

```
🚀 Start
   │
   ▼
┌─────────────────────────────────┐
│  Phase 1 · Foundations (4–8 wk) │
│  Python · Math · ML Basics      │
└─────────────────┬───────────────┘
                  │
                  ▼
┌─────────────────────────────────┐
│  Phase 2 · AI Core (6–10 wk)    │
│  Deep Learning · NLP · LLMs     │
└─────────────────┬───────────────┘
                  │
                  ▼
┌─────────────────────────────────┐
│  Phase 3 · Advanced AI (6–10 wk)│
│  RAG · Agents · Fine-tuning     │
└─────────────────┬───────────────┘
                  │
                  ▼
┌─────────────────────────────────┐
│  Phase 4 · Production (4–6 wk)  │
│  MLOps · Deployment · Monitoring│
└─────────────────┬───────────────┘
                  │
                  ▼
        ✅ AI Engineer
```

---

## Who is this for

| Profile | Where to start |
|---|---|
| Complete beginner | Phase 1 from the top — don't skip the math |
| Developer switching to AI | Phase 2, fill Phase 1 gaps as needed |
| Data Scientist leveling up | Phase 3 — Agents + LLMOps |
| Already building with LLMs | Phase 4 — systems that don't break at 3am |

---

## Repository structure

```
ai-engineer-from-scratch/
├── README.md                     ← you are here
├── roadmap.excalidraw            ← full interactive diagram
│
├── phase-1-foundations/
│   ├── README.md
│   ├── 01-python-for-ai/
│   ├── 02-math-and-stats/
│   └── 03-ml-fundamentals/
│
├── phase-2-ai-core/
│   ├── README.md
│   ├── 01-deep-learning/
│   ├── 02-nlp-and-transformers/
│   └── 03-llm-engineering/
│
├── phase-3-advanced-ai/
│   ├── README.md
│   ├── 01-rag-systems/
│   ├── 02-ai-agents/
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

## Phase 1 · Foundations

> The base everything else sits on. No shortcuts here.

Folder: [`phase-1-foundations/`](./phase-1-foundations/)

### Python for AI
| Topic | Free resource | Time |
|---|---|---|
| Async/await for APIs | [Real Python — Async IO](https://realpython.com/async-io-python/) | 1 week |
| OOP & type hints | [Python Docs](https://docs.python.org/3/library/typing.html) | 3 days |
| NumPy, Pandas, Matplotlib | [Kaggle Learn](https://www.kaggle.com/learn) | 1 week |

### Math & Statistics
| Topic | Free resource | Time |
|---|---|---|
| Linear Algebra | [3Blue1Brown — Essence of LA](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) | 1 week |
| Calculus (backprop) | [3Blue1Brown — Calculus](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) | 1 week |
| Probability & Stats | [StatQuest YouTube](https://www.youtube.com/@statquest) | 2 weeks |

### ML Fundamentals
| Topic | Free resource | Time |
|---|---|---|
| Core ML concepts | [Andrew Ng — ML Specialization](https://www.coursera.org/specializations/machine-learning-introduction) | 4 weeks |
| Scikit-learn hands-on | [Scikit-learn docs](https://scikit-learn.org/stable/tutorial/index.html) | 1 week |
| Feature engineering | [Kaggle Feature Engineering](https://www.kaggle.com/learn/feature-engineering) | 3 days |

---

## Phase 2 · AI Core

> The engine room. Master deep learning and LLMs.

Folder: [`phase-2-ai-core/`](./phase-2-ai-core/)

### Deep Learning
| Topic | Free resource | Time |
|---|---|---|
| Neural networks from scratch | [fast.ai Practical DL](https://course.fast.ai/) | 4 weeks |
| CNNs & computer vision | [CS231n Stanford](https://cs231n.github.io/) | 2 weeks |
| PyTorch fundamentals | [PyTorch official tutorial](https://pytorch.org/tutorials/) | 1 week |

### NLP & Transformers
| Topic | Free resource | Time |
|---|---|---|
| Attention mechanism | [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | 2 days |
| HuggingFace Transformers | [HuggingFace Course](https://huggingface.co/learn/nlp-course/chapter1/1) | 2 weeks |
| Building LLMs from scratch | [Andrej Karpathy — makemore](https://github.com/karpathy/makemore) | 1 week |

### LLM Engineering
| Topic | Free resource | Time |
|---|---|---|
| OpenAI API + function calling | [OpenAI Cookbook](https://cookbook.openai.com/) | 1 week |
| Anthropic Claude API | [Anthropic Docs](https://docs.anthropic.com/) | 3 days |
| Open source LLMs (Ollama) | [Ollama docs](https://ollama.com/docs) | 3 days |
| Prompt Engineering | [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) | 1 week |

---

## Phase 3 · Advanced AI

> This is where real engineering begins.

Folder: [`phase-3-advanced-ai/`](./phase-3-advanced-ai/)

### RAG Systems
| Topic | Free resource | Time |
|---|---|---|
| Vector databases | [Pinecone Learning Center](https://www.pinecone.io/learn/) | 1 week |
| Embeddings deep dive | [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings) | 3 days |
| Advanced RAG (HyDE, reranking) | [LlamaIndex Docs](https://docs.llamaindex.ai/) | 2 weeks |

### AI Agents
| Topic | Free resource | Time |
|---|---|---|
| LangGraph (stateful agents) | [LangGraph Docs](https://langchain-ai.github.io/langgraph/) | 2 weeks |
| Multi-agent systems (CrewAI) | [CrewAI Docs](https://docs.crewai.com/) | 1 week |
| MCP — Model Context Protocol | [Anthropic MCP Docs](https://modelcontextprotocol.io/) | 1 week |
| AutoGen | [AutoGen GitHub](https://github.com/microsoft/autogen) | 1 week |

### Fine-tuning
| Topic | Free resource | Time |
|---|---|---|
| LoRA & QLoRA | [HuggingFace PEFT](https://huggingface.co/docs/peft/index) | 2 weeks |
| Dataset curation | [Argilla Docs](https://docs.argilla.io/) | 1 week |
| Model evaluation & benchmarks | [Eleuther LM Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) | 1 week |

---

## Phase 4 · Production

> AI systems that don't break at 3am.

Folder: [`phase-4-production/`](./phase-4-production/)

### MLOps
| Topic | Free resource | Time |
|---|---|---|
| Experiment tracking (MLflow) | [MLflow Docs](https://mlflow.org/docs/latest/index.html) | 1 week |
| Data versioning (DVC) | [DVC Docs](https://dvc.org/doc) | 3 days |
| CI/CD for ML (GitHub Actions) | [GitHub Actions Docs](https://docs.github.com/en/actions) | 1 week |

### Deployment
| Topic | Free resource | Time |
|---|---|---|
| FastAPI for AI APIs | [FastAPI Docs](https://fastapi.tiangolo.com/) | 1 week |
| Docker + Kubernetes | [Play with Docker](https://labs.play-with-docker.com/) | 2 weeks |
| Cloud deployment (AWS/GCP) | [AWS Free Tier](https://aws.amazon.com/free/) | 2 weeks |

### Observability & Safety
| Topic | Free resource | Time |
|---|---|---|
| LLM monitoring (Langfuse) | [Langfuse Docs](https://langfuse.com/docs) | 3 days |
| Guardrails & evals | [RAGAS](https://docs.ragas.io/) · [DeepEval](https://docs.confident-ai.com/) | 1 week |
| AI security basics | [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | 3 days |

---

## Final Project

The capstone for everything. Folder: [`final-project/`](./final-project/)

Build a **multi-agent research assistant** that:
- Takes a question or topic from the user
- Plans and delegates subtasks to specialized agents
- Retrieves information via RAG from a custom document collection
- Generates a structured report with cited sources
- Is deployed as an API with active monitoring

Demonstrates: Agents · RAG · LLMs · FastAPI · Docker · Observability

---

## Essential free resources

| Resource | Why it matters |
|---|---|
| [fast.ai](https://fast.ai) | Best practical deep learning course, completely free |
| [DeepLearning.AI](https://www.deeplearning.ai/courses/) | Short courses on LLMs, RAG and Agents by Andrew Ng |
| [HuggingFace Learn](https://huggingface.co/learn) | Hands-on NLP, diffusion and agents with real code |
| [Andrej Karpathy YouTube](https://www.youtube.com/@AndrejKarpathy) | Build LLMs from scratch — unmissable |
| [The Batch](https://www.deeplearning.ai/the-batch/) | Weekly AI newsletter by DeepLearning.AI |

---

## Contributing

Found a better resource, a missing topic or a broken link?

1. Fork the repo
2. Create a branch: `git checkout -b add/your-topic`
3. Open a Pull Request with a clear description

---

MIT License — free to use, share and adapt.
