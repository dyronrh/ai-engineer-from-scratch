# 03 - Prompt Engineering

Not a soft skill. Write a prompt, measure outputs, iterate. These techniques have documented, measurable effects on output quality and every AI Engineer role expects you to know them.

## Core techniques

### System prompt

Sets context, role, and rules before the conversation starts. Use it for everything.

```python
messages = [
    {
        "role": "system",
        "content": (
            "You are a code reviewer. "
            "Always point out security issues first. "
            "Respond in markdown with clear section headers."
        )
    },
    {"role": "user", "content": "Review this code: ..."}
]
```

### Few-shot

Show examples of input and output before the real request. Dramatically improves format consistency, especially for structured data.

```python
examples = """
Input: "I loved this movie"
Output: {"sentiment": "positive", "score": 0.9}

Input: "Waste of time"
Output: {"sentiment": "negative", "score": 0.1}

Input: "It was okay"
Output:"""
```

### Chain-of-Thought

Tell the model to reason step by step before answering. Works particularly well for logic and multi-step problems.

```python
prompt = """
Solve this step by step:
A store has 50 items. 30% are on sale. 
How many items are NOT on sale?

Step 1:
"""
```

### Self-consistency

Run the same prompt multiple times with temperature above 0 and take the majority answer. More reliable than a single pass for reasoning tasks.

```python
answers = await asyncio.gather(*[ask(question) for _ in range(5)])
# pick most common answer
```

### Structured output instructions

Be explicit about format. When you cannot use the structured output API, put a JSON example directly in the prompt.

```python
prompt = """
Extract entities from this text.
Return ONLY valid JSON in this exact format:
{
  "people": ["name1", "name2"],
  "organizations": ["org1"],
  "locations": ["city1"]
}

Text: ...
"""
```

## What actually matters in production

1. Be specific. Vague prompts produce vague results.
2. Show the format. Do not describe it, show an example.
3. Set constraints. Tell the model what not to do.
4. Test against a set of examples, not just one.
5. Version your prompts. Treat them like code, because they are.

## Resources

- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
- [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering)
- [Prompting Guide](https://www.promptingguide.ai/)
