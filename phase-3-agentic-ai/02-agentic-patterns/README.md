# 02 - Agentic Patterns

The recurring patterns that make agents actually work. Learn these before jumping into frameworks — you'll understand what LangGraph is doing and why.

## ReAct (Reason + Act)

The foundation of most production agents. The model thinks before it acts, then observes the result, then thinks again.

```
Thought: I need to find the current price of NVDA stock
Action: search("NVDA stock price today")
Observation: NVDA is trading at $127.50
Thought: I have the price, I can answer now
Answer: NVDA is currently at $127.50
```

Why it works: forcing the model to reason before acting reduces hallucination and improves tool selection.

```python
REACT_PROMPT = """
You have access to these tools:
- search(query): search the web
- calculate(expression): run a math expression

For each step:
Thought: what you need to do
Action: tool_name(input)
Observation: [result will be inserted here]
... repeat until you have enough information
Answer: your final response
"""
```

## Planning

Break the goal into steps before executing any of them.

```
Goal: "Write a market analysis report on EV companies"

Plan:
1. Search for top 5 EV companies by market cap
2. Get Q3 earnings for each
3. Find recent news for each
4. Compare gross margins
5. Write summary with findings
```

Good for: complex tasks where the sequence of steps matters.
Bad for: simple tasks where planning overhead isn't worth it.

## Reflection

The agent evaluates its own output and tries again if it's not good enough.

```
Draft answer: [generated text]
Reflection: Does this answer the question? Is it accurate? Is it complete?
Score: 6/10 - missing recent data
Retry: [new attempt with corrected approach]
```

## Tool use

The model decides when and how to use external tools. The key design decision is how to define tools — description quality matters as much as implementation quality.

```python
tools = [
    {
        "name": "search",
        "description": "Search the web for current, factual information. Use when you need real-time data, recent events, or facts you're not confident about.",
        "input_schema": {"type": "object", "properties": {"query": {"type": "string"}}, "required": ["query"]}
    }
]
```

## Memory patterns

| Type | Storage | When to use |
|---|---|---|
| In-context | Message list | Short conversations, small context |
| Summary | Compressed text | Long conversations |
| External short-term | Redis/database | Multi-session conversations |
| Long-term | Vector store | Persistent facts, user preferences |
| Episodic | Structured logs | Agent that learns from past runs |

## Resources

- [ReAct: Synergizing Reasoning and Acting (paper)](https://arxiv.org/abs/2210.03629)
- [LangGraph conceptual guides](https://langchain-ai.github.io/langgraph/concepts/)
- [Lilian Weng - LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/)
