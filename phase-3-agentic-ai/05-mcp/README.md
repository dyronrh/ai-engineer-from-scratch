# 05 - MCP: Model Context Protocol

An open standard from Anthropic for connecting LLMs to external tools and data sources. Already appearing in job descriptions and likely to become the standard interface layer for agentic systems.

## What MCP is

Before MCP, every AI application had to write its own integration code. Custom logic to connect the LLM to a database, a file system, a search API. MCP standardizes that interface so any LLM host can use any MCP server without custom glue code.

```
Without MCP:
LLM App -> custom code -> Database
LLM App -> custom code -> File system
LLM App -> custom code -> GitHub API

With MCP:
LLM App -> MCP protocol -> Database MCP server
LLM App -> MCP protocol -> File system MCP server
LLM App -> MCP protocol -> GitHub MCP server
```

## Architecture

- **Host**: the LLM application (Claude Desktop, your custom app)
- **Client**: handles the MCP protocol inside the host
- **Server**: exposes tools, resources, and prompts over the protocol

## Build an MCP server

```python
from mcp.server import Server
from mcp.server.models import InitializationOptions
import mcp.types as types

server = Server("my-tools")

@server.list_tools()
async def list_tools() -> list[types.Tool]:
    return [
        types.Tool(
            name="read_file",
            description="Read a file from the local filesystem",
            inputSchema={
                "type": "object",
                "properties": {"path": {"type": "string"}},
                "required": ["path"],
            },
        )
    ]

@server.call_tool()
async def call_tool(name: str, arguments: dict) -> list[types.TextContent]:
    if name == "read_file":
        content = open(arguments["path"]).read()
        return [types.TextContent(type="text", text=content)]
```

## Connect to Claude

```python
import anthropic
import mcp

async with mcp.StdioServerParameters(...) as params:
    async with mcp.ClientSession(*params) as session:
        tools = await session.list_tools()
        response = client.messages.create(
            model="claude-opus-4-8",
            tools=[t.to_anthropic_format() for t in tools.tools],
            messages=[...]
        )
```

## Existing MCP servers you can use today

- **Filesystem** - read and write local files
- **GitHub** - repos, issues, pull requests
- **Postgres / SQLite** - query databases
- **Brave Search** - web search
- **Slack** - send messages, read channels
- **Puppeteer** - browser automation

All available at: [github.com/modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers)

## Exercises

| File | What you build |
|---|---|
| `01_first_mcp_server.py` | MCP server with one tool |
| `02_file_tools_server.py` | MCP server for file read/write/list |
| `03_claude_with_mcp.py` | Claude connected to your MCP server |
| `04_multi_server.py` | Agent using 2 MCP servers at once |

## Setup

```bash
pip install mcp anthropic
```

## Resources

- [MCP official docs](https://modelcontextprotocol.io/)
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk)
- [MCP server examples](https://github.com/modelcontextprotocol/servers)
- [MCP spec](https://spec.modelcontextprotocol.io/)
