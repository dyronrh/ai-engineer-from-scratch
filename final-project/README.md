# Final Project: Multi-Agent Research Assistant

The capstone. Everything from the four phases in one real system.

This is not a tutorial project. It is a deployable application that shows you can build end-to-end AI systems, the kind of thing you put in a portfolio and walk through in an interview.

---

## What it does

The assistant takes a topic or question, then produces a comprehensive, well-cited report by:

1. **Planning** - breaking the topic into sub-questions
2. **Retrieving** - searching a document collection with RAG
3. **Analyzing** - specialist agents handle different angles in parallel
4. **Synthesizing** - a coordinator agent assembles the final report
5. **Citing** - every claim is traced back to a source document

---

## Architecture

```
User query
    |
    v
+------------------+
|  Planner Agent   |  <- breaks query into sub-tasks
+--------+---------+
         |
    +----+----+
    |         |
    v         v
+--------+ +--------+
|  RAG   | |  RAG   |  <- specialist agents retrieve
| Agent 1| | Agent 2|     from document collection
+----+---+ +----+---+
    |           |
    +-----------+
          |
          v
+------------------+
| Synthesis Agent  |  <- assembles final report
+--------+---------+
         |
         v
  Structured report
  with cited sources
```

---

## Stack

| Component | Technology |
|---|---|
| Agent framework | LangGraph |
| Vector DB | ChromaDB |
| LLM | Anthropic Claude or OpenAI GPT-4o |
| Embeddings | `text-embedding-3-small` |
| API | FastAPI |
| Container | Docker + Docker Compose |
| Monitoring | Langfuse |
| CI/CD | GitHub Actions |
| Evaluation | RAGAS + DeepEval |

---

## Repository structure

```
final-project/
├── agents/
│   ├── planner.py          <- breaks query into sub-tasks
│   ├── researcher.py       <- RAG-powered specialist agent
│   ├── synthesizer.py      <- assembles final report
│   └── coordinator.py      <- LangGraph graph definition
│
├── rag/
│   ├── ingest.py           <- load and index documents
│   ├── retriever.py        <- query vector DB
│   └── embedder.py         <- embedding model wrapper
│
├── api/
│   ├── main.py             <- FastAPI app
│   ├── models.py           <- request/response schemas
│   └── middleware.py       <- auth, rate limiting, logging
│
├── evals/
│   ├── golden_set.json     <- question + expected answer pairs
│   ├── run_evals.py        <- evaluation script
│   └── metrics.py          <- faithfulness, relevance, citation accuracy
│
├── documents/              <- your document collection (gitignored)
│
├── tests/
│   ├── test_agents.py
│   ├── test_rag.py
│   └── test_api.py
│
├── .github/
│   └── workflows/
│       ├── test.yml
│       └── deploy.yml
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── .env.example
└── README.md
```

---

## Getting started

### Prerequisites

- Python 3.11+
- Docker and Docker Compose
- An OpenAI or Anthropic API key
- A Langfuse account (free tier works fine)

### Local setup

```bash
cd final-project
pip install -r requirements.txt

cp .env.example .env
# fill in:
# ANTHROPIC_API_KEY or OPENAI_API_KEY
# LANGFUSE_PUBLIC_KEY
# LANGFUSE_SECRET_KEY

# index your documents
python rag/ingest.py --docs ./documents/

# run the full system
docker compose up --build

# API at http://localhost:8000
# API docs at http://localhost:8000/docs
```

### Making a research request

```bash
curl -X POST http://localhost:8000/research \
  -H "Content-Type: application/json" \
  -d '{"question": "What are the main challenges in deploying LLMs at scale?"}'
```

### Running evaluations

```bash
python evals/run_evals.py \
  --dataset evals/golden_set.json \
  --threshold 0.80
```

---

## Success criteria

The project is complete when:

- [ ] Multi-agent system runs end-to-end without errors
- [ ] RAG retrieval faithfulness score is above 0.80 on the eval set
- [ ] API handles 10 concurrent requests without crashing
- [ ] All requests are traced in Langfuse
- [ ] Tests cover the main agent flows
- [ ] CI/CD pipeline runs on every push
- [ ] Docker deployment works on a fresh machine
- [ ] The README explains how to reproduce everything from scratch

---

## What this demonstrates to employers

| Skill | Where it shows |
|---|---|
| Agent design | Multi-agent architecture with LangGraph |
| RAG engineering | Chunking strategy, retrieval, evaluation |
| LLM integration | Prompt design, tool use, structured output |
| API development | FastAPI service with proper error handling |
| Production mindset | Monitoring, evals, CI/CD, containerization |
| Code quality | Tests, type hints, clean module structure |

---

## Extending the project (optional)

Once the base version works:

- **Web interface** - React or Streamlit frontend
- **Streaming** - stream the report as it generates
- **Document upload** - API endpoint to add new documents
- **Auth** - API key authentication
- **Caching** - cache common queries to cut costs
- **Multi-modal** - support PDFs with images and charts

Pick one extension, ship it, and add it to your portfolio.
