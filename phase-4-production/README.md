# Phase 4 · Production

> AI systems that don't break at 3am.

**Estimated duration:** 4–6 weeks  
**Prerequisite:** Phase 3 complete

---

## What you'll be able to do after this phase

- Track experiments and reproduce results reliably
- Package and deploy AI services with Docker and Kubernetes
- Set up monitoring for LLM applications in production
- Implement guardrails and evaluation pipelines
- Complete the phase project: production LLM API with full observability

---

## Modules

### [01 · MLOps](./01-mlops/)

The infrastructure that keeps AI projects alive long-term.

**Topics:**
- Experiment tracking with MLflow: log metrics, parameters, artifacts
- Data versioning with DVC: track datasets like code
- CI/CD for ML with GitHub Actions: automate training, testing, deployment
- Model registry: version, stage and serve models

**Resources:**
| Resource | Time |
|---|---|
| [MLflow Docs](https://mlflow.org/docs/latest/index.html) | 1 week |
| [DVC Docs](https://dvc.org/doc) | 3 days |
| [GitHub Actions Docs](https://docs.github.com/en/actions) | 1 week |

---

### [02 · Deployment](./02-deployment/)

Getting your model from notebook to a service that handles real traffic.

**Topics:**
- FastAPI: build production-grade AI APIs
- Docker: containerize your application
- Docker Compose: local multi-service setup
- Kubernetes: orchestration basics
- Cloud deployment: AWS (SageMaker, ECS) or GCP (Cloud Run, Vertex AI)

**Resources:**
| Resource | Time |
|---|---|
| [FastAPI Docs](https://fastapi.tiangolo.com/) | 1 week |
| [Play with Docker](https://labs.play-with-docker.com/) | 2 weeks |
| [AWS Free Tier](https://aws.amazon.com/free/) | 2 weeks |

---

### [03 · Observability](./03-observability/)

You can't fix what you can't see. LLM apps need different monitoring than traditional software.

**Topics:**
- LLM monitoring with Langfuse: traces, costs, latency, quality
- Guardrails: input/output validation, toxicity filtering, PII detection
- Evaluation pipelines: automated evals running on every deployment
- OWASP LLM Top 10: prompt injection, insecure output handling, and more

**Resources:**
| Resource | Time |
|---|---|
| [Langfuse Docs](https://langfuse.com/docs) | 3 days |
| [RAGAS](https://docs.ragas.io/) · [DeepEval](https://docs.confident-ai.com/) | 1 week |
| [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | 3 days |

---

## Phase project

**Production LLM API with monitoring**

A complete LLM service deployed with Docker, with a FastAPI interface and Langfuse monitoring.

**Stack:** FastAPI · Docker · Langfuse · GitHub Actions  
**Demonstrates:** Production deployment · Monitoring · CI/CD · API design

Project folder: [`02-deployment/project/`](./02-deployment/project/)

---

## Phase checklist

- [ ] Tracked an experiment with MLflow (metrics, params, model artifact)
- [ ] Versioned a dataset with DVC
- [ ] Containerized an AI app with Docker
- [ ] Set up a GitHub Actions workflow for ML
- [ ] Deployed a FastAPI service to the cloud
- [ ] Set up Langfuse traces for an LLM app
- [ ] Implemented at least one guardrail

Next: [Final Project](../final-project/)
