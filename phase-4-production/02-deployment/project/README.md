# Project · Production LLM API with Monitoring

A complete LLM service: FastAPI + Docker + Langfuse monitoring + GitHub Actions CI/CD.

## What it does

- REST API that wraps an LLM pipeline (RAG or direct completion)
- Every request is traced in Langfuse: prompt, response, latency, cost
- Health check and metrics endpoints
- Containerized with Docker
- CI/CD pipeline that tests and deploys on push

## Stack

- **API:** FastAPI + uvicorn
- **LLM:** OpenAI GPT-4o or Anthropic Claude
- **Monitoring:** Langfuse
- **Container:** Docker + Docker Compose
- **CI/CD:** GitHub Actions

## How to run locally

```bash
cd phase-4-production/02-deployment/project
cp .env.example .env
# fill in API keys

docker compose up --build
# API at http://localhost:8000
# Langfuse at http://localhost:3000
```

## How to run in production (AWS)

```bash
# build and push image
docker build -t your-registry/llm-api:latest .
docker push your-registry/llm-api:latest

# deploy (see deploy/aws/ for full instructions)
```

## Structure

```
project/
├── app/
│   ├── main.py             ← FastAPI app
│   ├── pipeline.py         ← LLM pipeline with Langfuse tracing
│   ├── models.py           ← Pydantic request/response models
│   └── config.py           ← settings from env
├── tests/
│   ├── test_api.py
│   └── test_pipeline.py
├── deploy/
│   └── aws/                ← ECS task definition and scripts
├── .github/
│   └── workflows/
│       └── deploy.yml      ← CI/CD pipeline
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── .env.example
└── README.md
```

## What it demonstrates

- Production API design with FastAPI
- Full observability with Langfuse traces
- Containerization with Docker
- Automated CI/CD pipeline
- Cloud deployment
