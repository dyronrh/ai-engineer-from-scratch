# 03 - LangGraph

Stateful, controllable agents. In 39.9% of agentic AI engineering job postings.

LangGraph models an agent as a graph: nodes are functions (LLM calls, tool calls, logic), edges are transitions, and state is passed between them. This gives you control, visibility, and persistence that simple chain-based agents don't have.

## Core concepts

### State

The object that travels through the graph. Every node reads from it and writes to it.

```python
from typing import TypedDict, Annotated
from langgraph.graph import add_messages

class AgentState(TypedDict):
    messages: Annotated[list, add_messages]
    tool_calls: list
    final_answer: str
```

### Nodes

Functions that take state in and return updated state.

```python
def call_llm(state: AgentState) -> dict:
    response = llm.invoke(state["messages"])
    return {"messages": [response]}

def run_tool(state: AgentState) -> dict:
    # execute the tool the LLM requested
    result = execute_tool(state["tool_calls"][-1])
    return {"messages": [ToolMessage(content=result)]}
```

### Edges

Connect nodes. Can be conditional — route based on state.

```python
from langgraph.graph import StateGraph, END

def should_continue(state: AgentState) -> str:
    last_message = state["messages"][-1]
    if last_message.tool_calls:
        return "run_tool"   # model wants to use a tool
    return END              # model has the answer

graph = StateGraph(AgentState)
graph.add_node("call_llm", call_llm)
graph.add_node("run_tool", run_tool)
graph.add_edge("run_tool", "call_llm")
graph.add_conditional_edges("call_llm", should_continue)
graph.set_entry_point("call_llm")

agent = graph.compile()
```

### Persistence (checkpointing)

Save and resume agent state. Essential for long-running agents and human-in-the-loop.

```python
from langgraph.checkpoint.sqlite import SqliteSaver

checkpointer = SqliteSaver.from_conn_string("agent.db")
agent = graph.compile(checkpointer=checkpointer)

config = {"configurable": {"thread_id": "session-123"}}
result = await agent.ainvoke({"messages": [HumanMessage("start")]}, config)
# resume later with the same thread_id
```

## Exercises

| File | What you build |
|---|---|
| `01_basic_agent.py` | Single-node ReAct agent |
| `02_tool_agent.py` | Agent with web search and calculator tools |
| `03_conditional_routing.py` | Agent that routes based on user intent |
| `04_persistent_agent.py` | Agent that remembers across sessions |
| `05_human_in_loop.py` | Agent that pauses for human approval |

## Resources

- [LangGraph Docs](https://langchain-ai.github.io/langgraph/)
- [LangGraph tutorials](https://langchain-ai.github.io/langgraph/tutorials/)
- [LangGraph How-to guides](https://langchain-ai.github.io/langgraph/how-tos/)
