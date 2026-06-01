# 03 · Observability

You can't fix what you can't see. LLM apps need different monitoring than traditional software.

## What to monitor in an LLM app

| Metric | Why it matters |
|---|---|
| Latency (p50, p95, p99) | User experience degrades above ~3s |
| Cost per request | LLM tokens add up fast at scale |
| Error rate | API errors, timeouts, context length exceeded |
| Quality scores | Are responses actually good? |
| Input/output length | Spot context window issues early |
| Cache hit rate | Are you paying for the same prompt twice? |

## Langfuse

Tracing for LLM applications. Every prompt, every response, every tool call — logged and queryable.

```python
from langfuse import Langfuse
from langfuse.decorators import observe

langfuse = Langfuse()

@observe()
def my_pipeline(question: str) -> str:
    response = openai_client.chat.completions.create(...)
    return response.choices[0].message.content
```

## Guardrails

Validation at the boundary between your app and the LLM:

- **Input validation:** detect prompt injection, filter PII, enforce length limits
- **Output validation:** check format, detect hallucinations, enforce content policy

```python
from guardrails import Guard
from guardrails.hub import ToxicLanguage, ValidLength

guard = Guard().use(ToxicLanguage).use(ValidLength, min=10, max=2000)
validated = guard.validate(llm_output)
```

## Evaluation pipelines

Run evals automatically on every deployment:

```bash
# .github/workflows/eval.yml
- run: python evals/run_evals.py --dataset evals/golden_set.json --threshold 0.85
```

## Exercises

| Exercise | File | Description |
|---|---|---|
| 1 | `01_langfuse_tracing.py` | Instrument a pipeline with Langfuse |
| 2 | `02_guardrails.py` | Input and output validation |
| 3 | `03_eval_pipeline.py` | Automated evaluation with DeepEval |

## Resources

- [Langfuse Docs](https://langfuse.com/docs)
- [RAGAS — RAG evaluation](https://docs.ragas.io/)
- [DeepEval](https://docs.confident-ai.com/)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
