# 03 · LLM Engineering

Building real applications on LLMs. Not just "call the API" - designing systems that work.

## Topics

### LLM APIs
- OpenAI: `gpt-4o`, function calling, structured outputs with JSON schema
- Anthropic: Claude, tool use, system prompts, streaming
- Ollama: local models, no per-token cost

### Prompt Engineering
Not magic. Engineering: experiment, measure, iterate.

| Technique | When to use |
|---|---|
| Zero-shot | Simple tasks, powerful LLMs |
| Few-shot | When output format matters |
| Chain-of-Thought | Complex reasoning, math |
| System prompt | Giving context and role to the model |
| RAG (preview of Phase 3) | When the model doesn't have the knowledge |

### LangChain
Chains, memory, document loaders. Useful tool - but understand what it does under the hood.

## Exercises

| Exercise | File | Description |
|---|---|---|
| 1 | `01_openai_basics.py` | Chat completion and streaming |
| 2 | `02_function_calling.py` | LLM that calls real functions |
| 3 | `03_anthropic_tools.py` | Tool use with Claude |
| 4 | `04_ollama_local.py` | Local LLM with Ollama |
| 5 | `05_prompt_engineering.py` | Compare prompting techniques |

## Setup

```bash
pip install openai anthropic langchain gradio python-dotenv
# for Ollama: install from https://ollama.com
```

```bash
# .env file
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
```

## Phase project

See [`project/`](./project/) - chatbot with memory and context.
