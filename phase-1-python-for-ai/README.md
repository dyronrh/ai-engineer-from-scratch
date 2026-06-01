# Phase 1 - Python for AI

**Duration:** 2-4 weeks  
**Goal:** Write async, typed Python. Call HTTP APIs. Handle JSON and environment config. Be fluent enough that the language never slows you down.

No math. No ML theory. Just Python as a working tool.

---

## Why only Python here

Based on real job postings:
- Python appears in 82% of AI Engineer roles — it's the one true prerequisite
- Math and ML theory appear in <20% of postings, mostly for ML Engineer roles (a different job)
- LLM APIs, RAG, and agents all run on Python + HTTP + JSON

Get Python solid and move to Phase 2. Everything else builds on top of it.

---

## What you need to be able to do

By the end of this phase:

- [ ] Write async functions that call external APIs concurrently
- [ ] Define typed classes with `dataclasses` or Pydantic models
- [ ] Load API keys from a `.env` file without hardcoding them
- [ ] Call a REST API with `httpx` and parse the JSON response
- [ ] Load a CSV with Pandas and do basic filtering and groupby

---

## Topics

### Async Python

Most LLM work involves waiting for API responses. Async lets you run multiple calls at the same time instead of one by one.

```python
import asyncio
import httpx

async def fetch(url: str) -> dict:
    async with httpx.AsyncClient() as client:
        response = await client.get(url)
        return response.json()

async def main():
    results = await asyncio.gather(
        fetch("https://api.example.com/a"),
        fetch("https://api.example.com/b"),
    )
    print(results)
```

Resource: [Real Python - Async IO](https://realpython.com/async-io-python/)

### Type hints and OOP

Type hints make your code readable and catch bugs before runtime. Expected in any production AI codebase.

```python
from dataclasses import dataclass
from typing import Optional

@dataclass
class Document:
    id: str
    content: str
    source: str
    score: Optional[float] = None
```

Resource: [Python Docs - typing](https://docs.python.org/3/library/typing.html)

### Environment config

Never hardcode API keys. Use `.env` files and `python-dotenv`.

```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("OPENAI_API_KEY")
```

### HTTP APIs with httpx

Better than `requests` for async work. You'll use this constantly to call LLM APIs and build integrations.

Resource: [HTTPX Docs](https://www.python-httpx.org/)

### Pandas basics

Load datasets, inspect data, prepare inputs for LLM pipelines.

Resource: [Kaggle Learn - Pandas](https://www.kaggle.com/learn/pandas)

---

## Exercises

| File | What you build |
|---|---|
| `01_async_calls.py` | Call 5 APIs concurrently with `asyncio.gather` |
| `02_typed_models.py` | Typed dataclasses for a document and search result |
| `03_env_config.py` | Load API keys and config from `.env` |
| `04_http_client.py` | Fetch data from a public API and parse the response |
| `05_pandas_basics.py` | Load a CSV, filter, groupby, export |

## Setup

```bash
pip install httpx pandas python-dotenv pydantic
```

---

## When you're ready for Phase 2

You should be able to write a script that:
1. Loads an API key from `.env`
2. Makes 3 concurrent async HTTP requests
3. Parses the responses into typed Pydantic models
4. Prints a formatted summary

If that feels natural, move to [Phase 2 - LLM Engineering](../phase-2-llm-engineering/).
