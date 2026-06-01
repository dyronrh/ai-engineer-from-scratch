# 03 - Monitoring

A 200 status code doesn't mean the answer was good. LLM apps need different monitoring than traditional software.

## What to monitor

| Signal | Why |
|---|---|
| Latency per request | User experience degrades fast above 3 seconds |
| Token usage and cost | LLM bills compound — catch spikes early |
| Error rate | API errors, timeouts, rate limits |
| Answer quality | Are responses actually correct and relevant? |
| Cache hit rate | Are you paying for the same prompt twice? |

## Langfuse

Traces every LLM call — prompt, response, latency, cost, model — queryable in a dashboard.

```python
from langfuse.decorators import observe, langfuse_context

@observe()
async def run_agent(question: str) -> str:
    langfuse_context.update_current_observation(
        input=question,
        metadata={"user_id": "user-123"},
    )
    response = await call_llm(question)
    langfuse_context.update_current_observation(output=response)
    return response
```

```bash
# local Langfuse with Docker
docker run -p 3000:3000 langfuse/langfuse
```

## Guardrails

Validate inputs and outputs at the boundary between your app and the model.

```python
def validate_input(text: str) -> str:
    # block obvious prompt injection
    injection_patterns = [
        "ignore previous instructions",
        "system prompt",
        "jailbreak",
    ]
    lower = text.lower()
    for pattern in injection_patterns:
        if pattern in lower:
            raise ValueError(f"Input rejected: potential injection")
    return text

def validate_output(text: str, max_length: int = 5000) -> str:
    if len(text) > max_length:
        raise ValueError("Output too long")
    return text
```

## Evaluation pipeline

Run automated evals on every deployment to catch regressions.

```python
# evals/run_evals.py
import json
from ragas import evaluate
from ragas.metrics import faithfulness, answer_relevancy

def run_evals(golden_set_path: str, threshold: float = 0.80):
    with open(golden_set_path) as f:
        dataset = json.load(f)
    results = evaluate(dataset, metrics=[faithfulness, answer_relevancy])
    score = results["faithfulness"]
    if score < threshold:
        raise SystemExit(f"Eval failed: faithfulness {score:.2f} < {threshold}")
    print(f"Evals passed: {score:.2f}")
```

## Resources

- [Langfuse Docs](https://langfuse.com/docs)
- [RAGAS - RAG evaluation](https://docs.ragas.io/)
- [DeepEval](https://docs.confident-ai.com/)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
