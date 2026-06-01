# 02 - API and Tool Use

Calling LLMs is straightforward. Calling them reliably, with structured output, while handling streaming and errors, is where the engineering skill lives.

## OpenAI API

### Streaming

```python
from openai import AsyncOpenAI

client = AsyncOpenAI()

async def stream_answer(question: str):
    stream = await client.chat.completions.create(
        model="gpt-4o",
        messages=[{"role": "user", "content": question}],
        stream=True,
    )
    async for chunk in stream:
        if chunk.choices[0].delta.content:
            print(chunk.choices[0].delta.content, end="", flush=True)
```

### Function calling

```python
tools = [{
    "type": "function",
    "function": {
        "name": "search_web",
        "description": "Search the web for current information",
        "parameters": {
            "type": "object",
            "properties": {"query": {"type": "string"}},
            "required": ["query"],
        },
    },
}]

response = await client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "What happened in tech today?"}],
    tools=tools,
)
```

### Structured output with Pydantic

```python
from pydantic import BaseModel

class MovieReview(BaseModel):
    title: str
    sentiment: str
    score: float

response = await client.beta.chat.completions.parse(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Review Inception"}],
    response_format=MovieReview,
)
review = response.choices[0].message.parsed  # typed MovieReview object
```

---

## Anthropic Claude API

### Tool use

```python
import anthropic

client = anthropic.Anthropic()

tools = [{
    "name": "get_weather",
    "description": "Get current weather for a location",
    "input_schema": {
        "type": "object",
        "properties": {"location": {"type": "string"}},
        "required": ["location"],
    },
}]

response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=1024,
    tools=tools,
    messages=[{"role": "user", "content": "Weather in Madrid?"}],
)
```

### Prompt caching

Cuts cost by up to 90% when you send the same large context repeatedly. Worth setting up from day one if you use a fixed system prompt.

```python
response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=1024,
    system=[{
        "type": "text",
        "text": "You are an expert in...",
        "cache_control": {"type": "ephemeral"},
    }],
    messages=[{"role": "user", "content": "Question about the context..."}],
)
```

---

## Ollama - local models, zero cost

```bash
ollama pull llama3.2
```

```python
import httpx

async def ask_ollama(prompt: str, model: str = "llama3.2") -> str:
    async with httpx.AsyncClient() as client:
        r = await client.post(
            "http://localhost:11434/api/generate",
            json={"model": model, "prompt": prompt, "stream": False},
        )
        return r.json()["response"]
```

---

## Exercises

| File | What you build |
|---|---|
| `01_openai_stream.py` | Streaming response that prints tokens as they arrive |
| `02_function_calling.py` | Model that calls a real function |
| `03_anthropic_tools.py` | Claude with tool use |
| `04_ollama_local.py` | Same prompt, local model |
| `05_structured_output.py` | Typed Pydantic object from any LLM |

## Setup

```bash
pip install openai anthropic httpx pydantic python-dotenv
```
