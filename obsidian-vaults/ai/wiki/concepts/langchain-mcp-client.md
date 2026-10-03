---
title: "LangChain MCP Client"
type: concept
domain: ai
tags:
  - langchain
  - mcp
  - tools
  - agent-patterns
  - agent-architecture
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/langchain-mcp-sample-patterns]]"
---

# LangChain MCP Client

How to connect a LangChain agent to an MCP server — discover tools at runtime and convert MCP tool definitions into LangChain `StructuredTool` format so the agent can call them. Covers both the stdio (subprocess) and HTTP (JSON-RPC over POST) transports.

## The conversion bridge

MCP tool definitions use JSON Schema. LangChain wants a `StructuredTool` backed by a Pydantic model. The bridge:

```python
def mcp_tool_to_langchain(mcp_tool, session: ClientSession) -> StructuredTool:
    # 1. Extract properties + required fields from inputSchema
    # 2. Build a Pydantic model dynamically with create_model()
    # 3. Wrap session.call_tool() in an async coroutine
    # 4. Return StructuredTool.from_function(coroutine=..., args_schema=ArgsModel)
```

Type mapping: `{"integer": int, "string": str, "number": float, "boolean": bool}`. Optional fields default to `None`.

## Session lifecycle (stdio)

The agent uses `mcp.client.stdio.stdio_client` — it spawns the server as a subprocess over stdin/stdout:

```python
async with stdio_client(StdioServerParameters(command="python", args=["server.py"])) as (read, write):
    async with ClientSession(read, write) as session:
        await session.initialize()
        tools_response = await session.list_tools()
        tools = [mcp_tool_to_langchain(t, session) for t in tools_response.tools]
        agent = create_agent(llm, tools, system_prompt=...)
        result = await agent.ainvoke({"messages": messages})
```

The server process must be running before the client starts.

## HTTP MCP (JSON-RPC over POST)

A raw HTTP MCP session follows four steps:

1. `POST /mcp` with `method: initialize` → get `Mcp-Session-Id` from response header
2. `POST /mcp` with `method: notifications/initialized` → confirm session
3. `POST /mcp` with `method: tools/list` → enumerate tools
4. `POST /mcp` with `method: tools/call` → invoke a tool

The `Mcp-Session-Id` header must be echoed back in every subsequent request. Responses may be SSE-framed (`data: {...}`).

## Related Concepts

- [[wiki/concepts/langchain-agent-patterns]] — general LangChain agent patterns
- [[wiki/concepts/agentic-arch-tools-mcp]] — tool/MCP design principles
- [[wiki/concepts/claude-code-mcp-setup]] — registering an MCP server with the Claude Code CLI

## Key Entities

- [[wiki/entities/langchain]] — the agent framework
- [[wiki/entities/mcp]] — the Model Context Protocol

## Sources

- [[wiki/sources/langchain-mcp-sample-patterns]]
