---
title: "Anthropic Launches Claude Managed Agents (That Make Agentic AI Workflows Real)"
type: source
domain: ai
tags:
  - claude-managed-agents
  - agent-infrastructure
  - anthropic
  - session-management
  - tool-execution
created: 2026-04-27
updated: 2026-04-27
raw: "[[raw/Anthropic Launches Claude Managed Agents (That Make Agentic AI Workflows Real).md]]"
---

# Anthropic Launches Claude Managed Agents (That Make Agentic AI Workflows Real)

**Author**: Joe Njenga
**Published**: 2026-04-09
**Type**: Feature deep-dive / tutorial

## Summary

Anthropic's Claude Managed Agents shift from "you build the harness" to "we host and manage it." A fully hosted cloud environment where Claude handles agent loop, tool execution, context management, session continuity, and automatic summarization when context window fills. Built around four concepts: Agent, Environment, Session, and Events.

## Key Takeaways

- **Two offerings**: Claude Managed Agents (fully hosted) and Claude Agent SDK (self-hosted)
- **Context management solved** — Automatic summarization when window fills keeps sessions alive
- **Built-in tools** — File ops, Bash, web search, web fetch, glob, grep, task spawning, skill invocation
- **Session persistence** — Save session ID, resume later; sessions are stateful across restarts
- **Permission modes** — Gate operations (default), auto-approve file edits, or full bypass for CI
- **Effort levels** — Controls reasoning depth; directly affects token usage and cost
- **Beta features** — Outcomes, multi-agent coordination, persistent memory (early access required)

## Entities Mentioned

- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-model-family]]

## Concepts Covered

- [[wiki/concepts/claude-managed-agents]]
- [[wiki/concepts/agent-harness]]
- [[wiki/concepts/tool-call-bottleneck]]
- [[wiki/concepts/context-window-management]]
- [[wiki/concepts/session-continuity]]

## Personal Notes

Eliminates weeks of infrastructure work. Session continuity and automatic context management are major wins. The abstraction level (Agent/Environment/Session/Events) is clean and composable.
