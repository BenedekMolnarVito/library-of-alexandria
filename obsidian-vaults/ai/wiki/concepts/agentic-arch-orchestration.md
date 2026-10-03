---
title: "Agentic Architecture & Orchestration (Domain 1)"
type: concept
domain: ai
tags:
  - agentic-architecture
  - orchestration
  - multi-agent
  - claude-certification
  - agent-architecture
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/claude-certification-architect-guide]]"
---

# Agentic Architecture & Orchestration (Domain 1)

The largest Claude Certification domain (27%). Covers the agentic loop, multi-agent orchestration, and how to make agent behaviour reliable. Parent hub: [[wiki/concepts/agentic-architecture-guide]].

## Agentic loop

Send request → inspect `stop_reason` → execute tools or terminate. Continue on `tool_use`, terminate on `end_turn`; **tool results must be appended to conversation history** before the next call or the model can't reason about them. `stop_reason` is the only reliable termination signal. Anti-patterns: natural-language parsing, iteration caps as primary control, checking `content[0].type == "text"` (text can co-occur with `tool_use`). Forcing `tool_choice: "any"` to suppress text creates an infinite loop.

## Orchestration patterns

Sequential (each step needs the prior output), parallel (independent subtasks, latency matters), pipeline (staged specialisation), dynamic adaptive (model decides the split at runtime), hub-and-spoke (coordinator + specialists).

## Subagents (1.3)

Isolated Claude instances spawned via the `Task` tool (renamed `Agent` in current Claude Code). Own context, own system prompt (`AgentDefinition.prompt`, NOT `systemPrompt`), own `tools` scope. **No shared memory** — pass everything explicitly. Coordinator needs `Task`/`Agent` in `allowedTools` to delegate at all.

## Workflow enforcement & handoff (1.4)

Deterministic requirements → **prerequisite gates** (e.g. block `process_refund` until `get_customer` returned a verified ID) or hooks, not prompts. A structured **handoff** is an escalation to a human who sees only the summary: customer ID, factual summary, root cause, monetary amount, recommended action. Routing (a classifier picking which agent handles a request) is a Domain-1 trap term — it does nothing about in-agent execution and is the wrong fix for a bloated tool set.

## Agent SDK hooks (1.5)

`PreToolUse` fires before a tool runs → deny/rewrite calls, validate inputs, block dangerous operations. `PostToolUse` fires after success → normalise/redact output, audit log. Both are code-level and cannot be bypassed by prompt injection.

## Task decomposition (1.6) & session state (1.7)

Coordinator splits work at runtime; fixed decomposition for predictable tasks, dynamic for open-ended. `fork_session` branches a session for divergent exploration without polluting the main line; a stale/polluted context is fixed by a **fresh session seeded with a curated summary**, not by adding more context.

## Related Concepts

- [[wiki/concepts/agentic-architecture-guide]] — cluster hub
- [[wiki/concepts/agentic-arch-tools-mcp]] — tool/MCP design the coordinator relies on
- [[wiki/concepts/agentic-loop]] — the general form of the loop above
- [[wiki/concepts/multi-agent-orchestration]] — the broader orchestration taxonomy
- [[wiki/concepts/advisor-executor-pattern]] — a two-role specialisation of hub-and-spoke

## Sources

- [[wiki/sources/claude-certification-architect-guide]]
