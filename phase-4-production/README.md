# Phase 4 - Production

**Estimated duration:** 4-6 weeks  
**Prerequisite:** Phase 3 done

---

## Market context for this phase

The skills in this phase are what separate candidates who can demo things from candidates who can ship them. Every company hiring AI engineers wants both — but production skills are the bottleneck.

- Docker and Kubernetes appear in 15-17% of all AI Engineer job postings
- FastAPI has 1,700+ active job listings that combine it with AI
- 63% of companies report a shortage of engineers with MLOps experience
- End-to-end production experience puts you in the top 10% of candidates

---

## Modules

### [01 - MLOps](./01-mlops/)

The infrastructure that makes AI projects maintainable. Without it, you can't reproduce results, you don't know what's in production, and deploying a new version is a manual nightmare.

**Topics:**
- Experiment tracking with MLflow: log params, metrics, and model artifacts
- Data versioning with DVC: track datasets like code
- CI/CD for ML with GitHub Actions: automate testing and deployment
- Model registry: version, stage, and serve models

**Resources:**
| Resource | Time |
|---|---|
| [MLflow Docs](https://mlflow.org/docs/latest/index.html) | 1 week |
| [DVC Docs](https://dvc.org/doc) | 3 days |
| [GitHub Actions Docs](https://docs.github.com/en/actions) | 1 week |

---

### [02 - Deployment](./02-deployment/) — high priority

FastAPI, Docker, and a cloud provider. This stack shows up in nearly every mid-size company and startup AI engineer posting. Without it you can build things, but you can't ship them.

**Topics:**
- FastAPI: build production-grade AI APIs with async support
- Docker: containerize your app so it runs the same everywhere
- Docker Compose: local multi-service setups (API + vector DB + monitoring)
- Kubernetes basics: orchestration for production
- Cloud: AWS (ECS/SageMaker) or GCP (Cloud Run/Vertex AI)

**Resources:**
| Resource | Time |
|---|---|
| [FastAPI Docs](https://fastapi.tiangolo.com/) | 1 week |
| [Play with Docker](https://labs.play-with-docker.com/) | 2 weeks |
| [AWS Free Tier](https://aws.amazon.com/free/) | 2 weeks |

---

### [03 - Observability](./03-observability/)

LLM apps need different monitoring than traditional software. You can't just check if the server is up — you need to know if the answers are any good.

**Topics:**
- LLM monitoring with Langfuse: traces, costs, latency, quality
- Guardrails: input/output validation, prompt injection detection
- Evaluation pipelines: automated evals on every deployment
- OWASP LLM Top 10: the security risks specific to LLM applications

**Resources:**
| Resource | Time |
|---|---|
| [Langfuse Docs](https://langfuse.com/docs) | 3 days |
| [RAGAS](https://docs.ragas.io/) and [DeepEval](https://docs.confident-ai.com/) | 1 week |
| [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | 3 days |

---

## Phase project

**Production LLM API with monitoring**

FastAPI + Docker + Langfuse. A real service with traces, health checks, and a CI/CD pipeline. This is what companies mean when they ask for "production experience."

**Stack:** FastAPI, Docker, Langfuse, GitHub Actions  
**Demonstrates:** API design, containerization, observability, automated deployment

Project folder: [`02-deployment/project/`](./02-deployment/project/)

---

## Phase checklist

- [ ] Logged a full experiment with MLflow (params, metrics, artifact)
- [ ] Versioned a dataset with DVC
- [ ] Built and containerized a FastAPI service with Docker
- [ ] GitHub Actions runs tests and deploys on push
- [ ] Deployed something to the cloud that someone else can hit
- [ ] Set up Langfuse traces for an LLM app
- [ ] Implemented at least one guardrail

Next: [Final Project](../final-project/)
