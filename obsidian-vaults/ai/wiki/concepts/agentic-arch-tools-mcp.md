---
title: "Tool Design & MCP Integration (Domain 2)"
type: concept
domain: ai
tags:
  - agentic-architecture
  - tools
  - mcp
  - claude-certification
  - agent-architecture
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/claude-certification-architect-guide]]"
---

# Tool Design & MCP Integration (Domain 2)

How an agent's tools are described, scoped, and integrated. Parent hub: [[wiki/concepts/agentic-architecture-guide]].

## Tool interface design (2.1)

Tool **descriptions are the primary tool-selection mechanism** — not metadata. A good description states what the tool does, its inputs (types/formats/required vs optional), example queries it handles well, and boundaries (what it does not do). Overlapping vague descriptions cause misrouting.

## Structured error responses (2.2)

Return errors as structured, actionable data the model can recover from (what failed, why, how to fix, whether to retry) rather than raw exceptions/stack traces. Let the agent self-correct on the next loop iteration.

## Tool distribution & choice (2.3)

Scope tools to role-focused sets; too many tools degrades selection. `tool_choice` controls whether the model must/may/can't call a tool (`auto`, `any`, a specific tool, `none`). Forcing tool use where the agent should be free is an anti-pattern.

## MCP server integration (2.4) & built-in tools (2.5)

MCP exposes external tools/data to the agent over a standard protocol; know the transport and auth shapes. Built-in tools (e.g. computer use, code execution, web search, text editor) are provided by the platform — prefer them over reimplementing equivalent custom tools.

## Related Concepts

- [[wiki/concepts/agentic-architecture-guide]] — cluster hub
- [[wiki/concepts/agentic-arch-orchestration]] — the loop that calls these tools
- [[wiki/concepts/tool-call-bottleneck]] — why tool count and latency dominate wall-clock time
- [[wiki/concepts/langchain-mcp-client]] — a concrete MCP client integration

## Key Entities

- [[wiki/entities/mcp]] — the Model Context Protocol this domain integrates
- [[wiki/entities/anthropic]] — defines the built-in tool set

## Sources

- [[wiki/sources/claude-certification-architect-guide]]
