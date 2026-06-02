# Phase 1 - Python for AI

**Duration:** 2-4 weeks  
**Goal:** Write async, typed Python. Call HTTP APIs. Handle JSON and environment config. Get fluent enough that the language never slows you down.

No math. No ML theory. Just Python as a working tool.

---

## Why only Python here

Real job posting data is blunt about this:

- Python shows up in 82% of AI Engineer roles. It is the one real prerequisite.
- Math and ML theory appear in fewer than 20% of postings, mostly for ML Engineer roles, which is a different job.
- LLM APIs, RAG, and agents all run on Python, HTTP, and JSON.

Get Python solid, then move to Phase 2. Everything else builds on top of it.

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

Most LLM work is just waiting. You send a request and wait for the model to respond. Async lets you fire off multiple requests at the same time instead of waiting for each one to finish before starting the next.

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

Type hints make your code readable and catch bugs before runtime. Any production AI codebase you join will expect this.

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

Never hardcode API keys. Use `.env` files and `python-dotenv`. This is non-negotiable in any real project.

```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("OPENAI_API_KEY")
```

### HTTP APIs with httpx

`httpx` is better than `requests` for async work. You will use it constantly when calling LLM APIs and building integrations.

Resource: [HTTPX Docs](https://www.python-httpx.org/)

### Pandas basics

Load datasets, inspect data, prepare inputs for LLM pipelines. You do not need to be a data scientist. You need to be able to load a CSV and filter it without looking things up.

Resource: [Kaggle Learn - Pandas](https://www.kaggle.com/learn/pandas)

---

## Exercises

All exercises are Jupyter notebooks. Open them in Google Colab or run them locally with Jupyter.

| Notebook | What you build |
|---|---|
| [01_async_calls.ipynb](./exercises/01_async_calls.ipynb) | Call 5 APIs concurrently with `asyncio.gather` |
| [02_typed_models.ipynb](./exercises/02_typed_models.ipynb) | Typed dataclasses and Pydantic models for documents and search results |
| [03_env_config.ipynb](./exercises/03_env_config.ipynb) | Load API keys from `.env` locally and from Colab secrets in the cloud |
| [04_http_client.ipynb](./exercises/04_http_client.ipynb) | Fetch data from a real public API and handle errors |
| [05_pandas_basics.ipynb](./exercises/05_pandas_basics.ipynb) | Load a CSV, filter, groupby, export |

Each notebook installs its own dependencies, so no setup needed in Colab. For local use:

```bash
pip install httpx pandas python-dotenv pydantic
```

---

## When you're ready for Phase 2

Write a script that:
1. Loads an API key from `.env`
2. Makes 3 concurrent async HTTP requests
3. Parses the responses into typed Pydantic models
4. Prints a formatted summary

If that feels natural, move to [Phase 2 - LLM Engineering](../phase-2-llm-engineering/).
