---
title: "Claude Code MCP Setup"
type: concept
domain: ai
tags:
  - claude-code
  - mcp
  - tools
  - agentic-coding
  - agent-architecture
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/langchain-mcp-sample-patterns]]"
---

# Claude Code MCP Setup

Claude Code (terminal) connects to external MCP servers over HTTP. You register a server once with `claude mcp add`, then authenticate it interactively via `/mcp` the first time you start a session. After that the server's tools are available to Claude in that session.

## Adding an MCP server

```bash
claude mcp add --transport http <name> <url>
```

For example:

```bash
claude mcp add --transport http my-mcp https://example.com/mcp
```

The `<name>` is an arbitrary local alias — it appears in `/mcp` and in tool names within the session.

## Authenticating

1. Start Claude: `claude`
2. Type `/mcp` in the prompt.
3. Find the server name you added.
4. Select **Authenticate** — a browser window opens.
5. Complete the login flow; return to the terminal.
6. The MCP server is now active for the session.

## Related Concepts

- [[wiki/concepts/langchain-mcp-client]] — connecting a LangChain agent to an MCP server
- [[wiki/concepts/agentic-arch-tools-mcp]] — tool/MCP design principles
- [[wiki/concepts/agentic-arch-claude-code-config]] — configuring Claude Code more broadly

## Key Entities

- [[wiki/entities/claude-code]] — the CLI being configured
- [[wiki/entities/mcp]] — the protocol being registered

## Sources

- [[wiki/sources/langchain-mcp-sample-patterns]]
