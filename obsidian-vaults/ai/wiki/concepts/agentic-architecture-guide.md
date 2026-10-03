---
title: "Agentic System Architecture (Claude Certification Guidance)"
type: concept
domain: ai
tags:
  - agentic-architecture
  - orchestration
  - claude-certification
  - agent-patterns
  - agent-architecture
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/claude-certification-architect-guide]]"
---

# Agentic System Architecture (Claude Certification Guidance)

Vendor-neutral design guidance for building agentic systems with Claude, synthesized from the Claude Certification **Architect (Foundations)** track — five domains, 30 lessons, and a 257-question drill set. Although the concrete API surface is Anthropic's, the principles below (loop control, deterministic enforcement, hub-and-spoke orchestration, structured output, provenance) transfer to any agent framework. This is the hub page for a five-domain cluster.

## The five domains

1. [[wiki/concepts/agentic-arch-orchestration]] — Agentic Architecture & Orchestration (27%, the largest domain)
2. [[wiki/concepts/agentic-arch-tools-mcp]] — Tool Design & MCP Integration
3. [[wiki/concepts/agentic-arch-claude-code-config]] — Claude Code Configuration & Workflows
4. [[wiki/concepts/agentic-arch-prompt-engineering]] — Prompt Engineering & Structured Output
5. [[wiki/concepts/agentic-arch-context-reliability]] — Context Management & Reliability

## Cross-cutting decision rules (the most-tested principles)

- **Loop control uses `stop_reason`, never text or caps.** Continue on `tool_use`, terminate on `end_turn`. Parsing "I'm done", checking `content[0].type == "text"`, or using an iteration cap as the primary stop are all anti-patterns. Iteration caps are safety nets only. A production loop also handles `pause_turn`, `max_tokens`, `stop_sequence`, `refusal`, `model_context_window_exceeded` — treat anything but `end_turn` as "not done, check why".
- **Deterministic guarantees need code, not prompts.** When a requirement says "must always" / "guaranteed" / compliance / audit / financial / security, the answer is programmatic enforcement — PreToolUse/PostToolUse hooks or a prerequisite gate — not a stronger prompt. Prompts are probabilistic.
- **Multi-agent = hub-and-spoke.** A coordinator decomposes, sequences, and aggregates; specialist subagents are isolated (no shared memory), so all context passes explicitly through the task definition. Subagents never talk peer-to-peer. A coordinator that "won't delegate" usually lacks `Task`/`Agent` in `allowedTools` — a config gate, not a prompt problem.
- **Scope each agent to a small, role-focused tool set** — the guide contrasts 4–5 tools with 18, where selection reliability degrades on decision complexity alone.
- **Handoff = escalation to a human** who has only the structured summary (customer ID, factual summary, root cause, recommended action) — not the transcript. There is no agent-to-agent handoff primitive.

## Why It Matters

This cluster condenses the design decisions that most often separate a reliable agent from a demo. The recurring theme: push correctness into deterministic code (hooks, gates, schemas, classifier thresholds) and reserve the model for genuinely probabilistic judgment. It is the rigorous counterpart to the looser patterns described across the wiki's agent-architecture pages.

## Related Concepts

- [[wiki/concepts/agentic-loop]] — the core execution cycle these rules harden
- [[wiki/concepts/multi-agent-orchestration]] — hub-and-spoke at the system level
- [[wiki/concepts/harness-engineering]] — structuring what each agent sees
- [[wiki/concepts/claude-md]] — the instruction-file hierarchy Domain 3 covers
- [[wiki/concepts/context-window-management]] — the discipline behind Domain 5

## Key Entities

- [[wiki/entities/anthropic]] — Claude, Claude Code, the certification substrate
- [[wiki/entities/claude-code]] — the agentic coding tool Domain 3 configures
- [[wiki/entities/mcp]] — the tool-integration protocol in Domain 2

## Sources

- [[wiki/sources/claude-certification-architect-guide]]
