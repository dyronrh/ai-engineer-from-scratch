# 02 · AI Agents

Agents that plan, use tools, and adapt. Not chatbots wrapped in a loop.

## What makes something an agent

A chatbot responds. An agent acts.

An agent has:
- **Goals** - what it's trying to achieve
- **Tools** - actions it can take (search web, run code, call APIs)
- **Memory** - context it carries across steps
- **Planning** - ability to break a goal into steps

## ReAct pattern

The foundation of most practical agents:

```
Thought: I need to find the latest price of X
Action: search("current price of X")
Observation: [search results]
Thought: Now I can answer the question
Action: final_answer("The price is...")
```

## LangGraph

State machines for agents. Better than linear chains when your agent needs to:
- Branch based on tool results
- Loop until a condition is met
- Coordinate multiple sub-agents
- Handle errors and retries

## Notebooks

| Notebook | Description |
|---|---|
| `01_react_agent.ipynb` | ReAct agent from scratch |
| `02_langgraph_basics.ipynb` | State graphs and nodes |
| `03_agent_with_tools.ipynb` | Agent with web search + code execution |
| `04_multi_agent.ipynb` | Coordinator + specialist agents with CrewAI |
| `05_mcp_intro.ipynb` | Model Context Protocol basics |

## Setup

```bash
pip install langchain langgraph crewai openai anthropic tavily-python
```

## Phase project

See [`project/`](./project/) - research agent with RAG.

## Resources

- [LangGraph Docs](https://langchain-ai.github.io/langgraph/)
- [CrewAI Docs](https://docs.crewai.com/)
- [Anthropic MCP Docs](https://modelcontextprotocol.io/)
- [AutoGen GitHub](https://github.com/microsoft/autogen)
