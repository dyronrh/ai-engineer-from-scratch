# 01 - FastAPI

The standard for Python AI APIs. Async, fast, and Pydantic-native.

## Basic async LLM endpoint

```python
from fastapi import FastAPI
from pydantic import BaseModel
from anthropic import AsyncAnthropic

app = FastAPI()
client = AsyncAnthropic()

class QueryRequest(BaseModel):
    question: str
    max_tokens: int = 1024

class QueryResponse(BaseModel):
    answer: str
    tokens_used: int

@app.post("/query", response_model=QueryResponse)
async def query(request: QueryRequest) -> QueryResponse:
    response = await client.messages.create(
        model="claude-opus-4-8",
        max_tokens=request.max_tokens,
        messages=[{"role": "user", "content": request.question}],
    )
    return QueryResponse(
        answer=response.content[0].text,
        tokens_used=response.usage.input_tokens + response.usage.output_tokens,
    )
```

## Streaming endpoint

```python
from fastapi.responses import StreamingResponse

@app.post("/query/stream")
async def query_stream(request: QueryRequest):
    async def generate():
        async with client.messages.stream(
            model="claude-opus-4-8",
            max_tokens=request.max_tokens,
            messages=[{"role": "user", "content": request.question}],
        ) as stream:
            async for text in stream.text_stream:
                yield f"data: {text}\n\n"
    return StreamingResponse(generate(), media_type="text/event-stream")
```

## Dependency injection for clients

```python
from functools import lru_cache
from fastapi import Depends

@lru_cache
def get_anthropic_client() -> AsyncAnthropic:
    return AsyncAnthropic()

@app.post("/query")
async def query(
    request: QueryRequest,
    client: AsyncAnthropic = Depends(get_anthropic_client),
):
    ...
```

## Health check (required for every deployed service)

```python
@app.get("/health")
async def health() -> dict:
    return {"status": "ok"}
```

## Exercises

| File | What you build |
|---|---|
| `01_basic_api.py` | Async chat endpoint |
| `02_streaming_api.py` | SSE streaming endpoint |
| `03_agent_api.py` | Endpoint that runs an agent and returns the result |
| `04_background_tasks.py` | Long-running agent job with status polling |

## Resources

- [FastAPI Docs](https://fastapi.tiangolo.com/)
- [FastAPI best practices](https://github.com/zhanymkanov/fastapi-best-practices)
