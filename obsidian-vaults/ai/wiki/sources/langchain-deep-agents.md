---
title: "LangChain Just Released Deep Agents — And It Changes How You Build AI Systems"
type: source
domain: ai
tags:
  - langchain
  - agents
  - context-management
  - python
  - subagents
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/LangChain Just Released Deep Agents — And It Changes How You Build AI Systems.md]]"
---

# LangChain Just Released Deep Agents — And It Changes How You Build AI Systems

**Authors**: Darshandagaa
**Date**: 2026-04
**Type**: article

## Summary

LangChain released `deepagents`, a high-level Python library dubbed an "agent harness" built on top of LangGraph that ships five built-in capabilities out of the box: a planning tool (`write_todos`), a virtual filesystem for context management, subagent spawning, automatic context compression and summarization, and long-term cross-session memory. The library abstracts away the boilerplate of LangGraph state graphs so developers can focus on domain logic rather than plumbing infrastructure. It also ships a CLI coding agent comparable to Claude Code or Aider, built on the same SDK.

The central metaphor—"LangGraph gives you an engine; Deep Agents gives you a car"—captures the layering clearly. Rather than managing state transitions manually, developers declare a goal and let the harness handle context budgeting, subtask delegation, and persistence. This is LangChain's bet that the solutions every production agent team independently reinvents are common enough to be standardized and shipped as a library.

## Key Takeaways

- `deepagents` sits above LangGraph: "LangGraph gives you an engine and a transmission. Deep Agents gives you a car."
- Virtual filesystem offloads tool results exceeding 20,000 tokens to disk, retrieving on demand rather than truncating — a direct answer to context-window overflow
- Subagent spawning keeps the main agent's context clean by delegating subtasks to fresh instances with their own context windows
- Automatic summarization triggers at 85% context usage, replacing full history with a structured summary while preserving originals to disk
- Long-term memory persists across threads and restarts via a `/memories/` path in a LangGraph Store backend
- The `deepagents` CLI coding agent enables terminal-based workflows with persistent project memory, rivaling Claude Code and Aider
- Best suited for complex, long-horizon tasks; simple agents should stick with LangChain's `create_agent`

## Entities Mentioned

- [[wiki/entities/langchain]]
- [[wiki/entities/langgraph]]
- [[wiki/entities/deepagents]]
- [[wiki/entities/darshandagaa]]
- [[wiki/entities/towards-ai]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-sonnet]]
- [[wiki/entities/tavily]]
- [[wiki/entities/modal]]
- [[wiki/entities/daytona]]

## Concepts Covered

- [[wiki/concepts/agent-harness]]
- [[wiki/concepts/context-window-management]]
- [[wiki/concepts/subagent-delegation]]
- [[wiki/concepts/virtual-filesystem]]
- [[wiki/concepts/automatic-context-compression]]
- [[wiki/concepts/long-term-agent-memory]]
- [[wiki/concepts/tool-calling-loop]]
- [[wiki/concepts/langgraph-state-machine]]

## Notable Quotes

> "LangGraph gives you an engine and a transmission. Deep Agents gives you a car."

> "Every team building production agents has had to engineer solutions to these exact problems from scratch. `deepagents` is LangChain's bet that these solutions are common enough to be standardized."

## Cross-Connections

The virtual-filesystem plus subagent pattern in `deepagents` is architecturally identical to the AGENTS.md / skills system described in [[wiki/sources/stop-vibe-coding-4-file-system]] and [[wiki/sources/master-claude-code-skills]] — all three converge on externalizing agent state and instructions. The governance layer missing from `deepagents` is precisely what [[wiki/sources/paperclip-ai-governance-platform]] provides: `deepagents` handles cognitive infrastructure while Paperclip handles financial and operational governance.
