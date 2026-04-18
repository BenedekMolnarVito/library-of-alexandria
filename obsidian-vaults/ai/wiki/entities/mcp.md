---
title: "MCP (Model Context Protocol)"
type: entity
domain: ai
tags:
  - product
  - protocol
  - anthropic
  - open-standard
  - tool-integration
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/ai-50x-faster-getting-2x-wrong-thing]]"
  - "[[wiki/sources/comparing-6-python-ai-agent-frameworks]]"
---

# MCP (Model Context Protocol)

The Model Context Protocol (MCP) is an open standard published by [[wiki/entities/anthropic]] for connecting AI models to external tools, data sources, and services in a standardized way. It defines a common interface that allows any MCP-compatible tool to be used by any MCP-compatible model or agent framework, reducing the integration work required to connect AI to the real world.

## Background / History

Anthropic published MCP in late 2024 as an open protocol, recognizing that the proliferation of AI tools and the proliferation of models were creating an N×M integration problem: every tool needed to implement adapters for every model API, and every model needed to document its tool-calling format for every tool author. A standard protocol reduces this to N+M implementations — each tool implements MCP once, and each model/agent framework implements MCP once, and they all work together.

MCP is intentionally similar in spirit to the Language Server Protocol (LSP) for code editors — a successful open standard that solved a similar N×M problem in the IDE ecosystem. The analogy is apt: LSP allowed every programming language to expose its analysis capabilities to any editor through a single protocol, and MCP aims to do the same for AI tool connectivity.

## Key Contributions / Features

**Standardized Tool Interface**: MCP defines a JSON-based protocol for AI models to discover and call external tools — querying databases, reading files, calling web APIs, executing code, and more. The standard covers tool discovery (what tools are available?), input schemas (what parameters does each tool accept?), and response formats (what does the tool return?).

**Server/Client Architecture**: MCP implementations consist of MCP servers (which expose tools) and MCP clients (which use tools). Anthropic ships MCP servers for common integrations (GitHub, Slack, file systems, web search), and the community has contributed many more. Any agent framework that implements the MCP client can use all these servers without custom integration work.

**Wide Adoption**: Despite being an Anthropic initiative, MCP has been adopted by tools beyond Anthropic's ecosystem — including [[wiki/entities/langchain]] and other agent frameworks that have implemented MCP clients to access the growing ecosystem of MCP servers. (Source: [[wiki/sources/comparing-6-python-ai-agent-frameworks]])

**"Stopgap" Criticism**: [[wiki/entities/nate-b-jones]] characterized MCP as a "stopgap" for human-speed APIs — arguing that MCP essentially wraps existing synchronous APIs (designed for human-pace interactions) in a protocol that makes them accessible to AI agents, but that purpose-built agent-native APIs would be fundamentally better. This is a genuine tension: MCP enables today's tools to be used by agents, but it inherits the latency, rate limits, and semantic mismatches of those tools. (Source: [[wiki/sources/ai-50x-faster-getting-2x-wrong-thing]])

## Role in AI Landscape

MCP's significance is as infrastructure for the agentic era — the connectivity layer that allows AI agents to interact with the rest of the software ecosystem. Whether it becomes a durable standard (like LSP) or is superseded by purpose-built agent-native interfaces (as Nate B. Jones suggests) is an open question. For now, it is the most widely adopted standard for AI tool integration and is a reasonable default for practitioners building agentic applications that need to connect to external services.

> [!question] Open Question
> Will MCP remain the standard tool integration protocol as agent-native APIs emerge, or will it be displaced by approaches designed specifically for AI-speed rather than human-speed interaction patterns?

## Connections

- **Related entities**: [[wiki/entities/anthropic]], [[wiki/entities/langchain]], [[wiki/entities/langgraph]], [[wiki/entities/claude-code]], [[wiki/entities/nate-b-jones]]
- **Key concepts**: [[wiki/concepts/tool-calling]], [[wiki/concepts/agent-orchestration]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/ai-native-infrastructure]]
- **Sources**: [[wiki/sources/ai-50x-faster-getting-2x-wrong-thing]], [[wiki/sources/comparing-6-python-ai-agent-frameworks]]
