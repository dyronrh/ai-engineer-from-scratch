# Phase 4 - Production

**Duration:** 4-6 weeks  
**Prerequisite:** Phase 3 done

---

## What this phase covers

The gap between a demo and a product. FastAPI and Docker appear in 1,700+ active AI engineer postings, and 63% of companies report a shortage of engineers who can actually do this well.

If you can build agents and RAG pipelines but cannot ship them as a service, you are a prototype engineer. This phase is about changing that.

---

## Modules

### [01 - FastAPI](./01-fastapi/)

The standard for Python AI APIs. Async by default, automatic docs, Pydantic models, and straightforward to test.

**Topics:**
- Async endpoints that call LLMs without blocking
- Pydantic request and response schemas
- Dependency injection for API keys and clients
- Streaming responses for LLM output
- Background tasks for long-running agent jobs
- Health checks and basic auth

**Resources:**
| Resource | Time |
|---|---|
| [FastAPI Docs](https://fastapi.tiangolo.com/) | 1 week |
| [FastAPI best practices](https://github.com/zhanymkanov/fastapi-best-practices) | 2 days |

---

### [02 - Docker and Deployment](./02-docker-and-deployment/)

Containerize your app and ship it to the cloud. Docker and Kubernetes appear in 15-17% of all AI Engineer postings.

**Topics:**
- Dockerfile for a FastAPI and LLM app
- Docker Compose for local multi-service setups (API + vector DB + monitoring)
- Environment variables and secrets management
- Deploying to AWS (ECS/App Runner) or GCP (Cloud Run)
- GitHub Actions CI/CD: test on push, deploy on merge

**Resources:**
| Resource | Time |
|---|---|
| [Play with Docker](https://labs.play-with-docker.com/) | 1 week |
| [AWS Free Tier](https://aws.amazon.com/free/) | 1 week |
| [GitHub Actions Docs](https://docs.github.com/en/actions) | 3 days |

---

### [03 - Monitoring](./03-monitoring/)

LLM apps break in ways traditional apps do not. A 200 response does not mean the answer was good. You need to trace prompts, measure quality, and catch regressions before users do.

**Topics:**
- Langfuse: trace every LLM call, prompt, response, latency, cost
- Structured logging for agent steps
- Evaluation pipelines: run evals on every deployment
- Guardrails: input validation, output validation, PII detection
- OWASP LLM Top 10: prompt injection and the other real security risks

**Resources:**
| Resource | Time |
|---|---|
| [Langfuse Docs](https://langfuse.com/docs) | 3 days |
| [RAGAS](https://docs.ragas.io/) + [DeepEval](https://docs.confident-ai.com/) | 1 week |
| [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | 2 days |

---

## Phase project

**Production LLM API with monitoring**

A FastAPI service wrapping an agent pipeline, containerized with Docker, deployed to cloud, with Langfuse tracing and a GitHub Actions CI/CD pipeline.

Project folder: [`02-docker-and-deployment/project/`](./02-docker-and-deployment/project/)

---

## Phase checklist

- [ ] FastAPI service with async LLM endpoint and streaming
- [ ] Containerized with Docker, runs on a fresh machine with `docker compose up`
- [ ] Deployed to cloud, someone outside your network can hit it
- [ ] GitHub Actions runs tests on push
- [ ] Every LLM call is traced in Langfuse
- [ ] Input guardrail blocks obvious prompt injection

Next: [Final Project](../final-project/)
