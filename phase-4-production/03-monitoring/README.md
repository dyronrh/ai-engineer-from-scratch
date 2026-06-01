# 03 - Monitoring

A 200 status code does not mean the answer was good. LLM applications need a different approach to monitoring than traditional software.

## What to track

| Signal | Why |
|---|---|
| Latency per request | User experience degrades fast above 3 seconds |
| Token usage and cost | LLM costs compound quickly. Catch spikes early. |
| Error rate | API errors, timeouts, rate limits |
| Answer quality | Are responses actually correct and relevant? |
| Cache hit rate | Are you paying for the same prompt twice? |

## Langfuse

Traces every LLM call with prompt, response, latency, cost, and model, all queryable in a dashboard.

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
docker run -p 3000:3000 langfuse/langfuse
```

## Guardrails

Validate inputs and outputs at the boundary between your app and the model. Do not rely on the model to catch bad inputs.

```python
def validate_input(text: str) -> str:
    injection_patterns = [
        "ignore previous instructions",
        "system prompt",
        "jailbreak",
    ]
    lower = text.lower()
    for pattern in injection_patterns:
        if pattern in lower:
            raise ValueError("Input rejected: potential injection")
    return text

def validate_output(text: str, max_length: int = 5000) -> str:
    if len(text) > max_length:
        raise ValueError("Output too long")
    return text
```

## Evaluation pipeline

Run automated evals on every deployment to catch quality regressions before users do.

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
