# 02 - Docker and Deployment

Containerize it. Ship it. Make it someone else's problem to run (in a good way).

## Dockerfile for a FastAPI AI app

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## Docker Compose for local dev

Spin up your API, a vector database, and monitoring together.

```yaml
services:
  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      - ANTHROPIC_API_KEY=${ANTHROPIC_API_KEY}
    depends_on:
      - chromadb

  chromadb:
    image: chromadb/chroma
    ports:
      - "8001:8000"

  langfuse:
    image: langfuse/langfuse
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=sqlite:///langfuse.db
```

```bash
cp .env.example .env
docker compose up --build
```

## GitHub Actions CI/CD

```yaml
# .github/workflows/deploy.yml
on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pip install -r requirements.txt
      - run: pytest tests/

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Cloud Run
        run: |
          gcloud run deploy ai-api \
            --image gcr.io/$PROJECT/$IMAGE \
            --region us-central1
```

## Exercises

| File | What you build |
|---|---|
| `01_dockerfile` | Containerize the FastAPI app |
| `02_docker_compose.yml` | Multi-service local setup |
| `03_deploy_cloud_run.sh` | Deploy to GCP Cloud Run |
| `04_github_actions/` | CI/CD pipeline |

## Resources

- [Play with Docker](https://labs.play-with-docker.com/)
- [Google Cloud Run quickstart](https://cloud.google.com/run/docs/quickstarts/build-and-deploy/deploy-python-service)
- [AWS App Runner](https://docs.aws.amazon.com/apprunner/latest/dg/getting-started.html)
