# 02 · Deployment

Getting your model from notebook to a service that handles real traffic.

## FastAPI for AI APIs

FastAPI is the standard for Python AI services. It's fast, has automatic docs, and handles async natively.

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class QueryRequest(BaseModel):
    question: str
    max_tokens: int = 512

@app.post("/query")
async def query(request: QueryRequest) -> dict:
    answer = await your_llm_pipeline(request.question)
    return {"answer": answer}
```

## Docker

Every AI service runs in a container. No exceptions.

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## Exercises

| Exercise | Folder | Description |
|---|---|---|
| 1 | `01_fastapi_service/` | REST API for an LLM pipeline |
| 2 | `02_dockerize/` | Containerize the FastAPI service |
| 3 | `03_docker_compose/` | Multi-service setup (API + vector DB) |
| 4 | `04_cloud_deploy/` | Deploy to AWS or GCP |

## Phase project

See [`project/`](./project/) — production LLM API with monitoring.

## Resources

- [FastAPI Docs](https://fastapi.tiangolo.com/)
- [Play with Docker](https://labs.play-with-docker.com/)
- [AWS Free Tier](https://aws.amazon.com/free/)
- [Google Cloud Run](https://cloud.google.com/run)
