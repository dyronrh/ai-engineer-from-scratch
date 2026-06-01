# 04 - Multi-Agent Systems

One agent trying to do everything produces mediocre results. Multiple specialized agents — each focused, each tool-equipped — produce better outputs on complex tasks.

## When to use multi-agent

Use multi-agent when:
- The task has clearly separable subtasks (research, writing, fact-checking)
- Subtasks can run in parallel
- Each subtask needs different tools or expertise
- A single context window isn't enough for the full task

Don't use multi-agent when:
- The task is simple and sequential
- You're adding coordination overhead for no real benefit
- You need tight control over the execution order

## Coordinator + specialist pattern

The most common production pattern.

```
Coordinator
    |--- Research Agent (web search, document retrieval)
    |--- Analysis Agent (data processing, calculations)
    |--- Writing Agent (drafting, formatting)
    |--- Review Agent (fact-checking, quality evaluation)
```

The coordinator plans, delegates, and assembles the final result. Specialists have narrow scope and focused tools.

## CrewAI

Higher-level multi-agent orchestration. Less control than LangGraph, faster to build.

```python
from crewai import Agent, Task, Crew

researcher = Agent(
    role="Research Analyst",
    goal="Find accurate information about the topic",
    tools=[search_tool, scrape_tool],
    llm="claude-opus-4-8",
)

writer = Agent(
    role="Technical Writer",
    goal="Write clear, structured reports",
    llm="claude-opus-4-8",
)

research_task = Task(
    description="Research recent developments in {topic}",
    agent=researcher,
    expected_output="Bullet points with key findings and sources",
)

write_task = Task(
    description="Write a 500-word report based on the research",
    agent=writer,
    context=[research_task],
)

crew = Crew(agents=[researcher, writer], tasks=[research_task, write_task])
result = crew.kickoff(inputs={"topic": "agentic AI"})
```

## Exercises

| File | What you build |
|---|---|
| `01_parallel_agents.py` | Two agents running the same query in parallel |
| `02_coordinator_crew.py` | Coordinator that delegates to 3 specialists |
| `03_crewai_pipeline.py` | Full research + write pipeline with CrewAI |

## Phase project

See [`project/`](./project/) - research agent with RAG and MCP.

## Resources

- [CrewAI Docs](https://docs.crewai.com/)
- [LangGraph multi-agent docs](https://langchain-ai.github.io/langgraph/concepts/multi_agent/)
- [AutoGen GitHub](https://github.com/microsoft/autogen)
