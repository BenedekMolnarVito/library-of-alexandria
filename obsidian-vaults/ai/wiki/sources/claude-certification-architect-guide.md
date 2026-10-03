---
title: "Claude Certification Guide — Architect (Foundations) track"
type: source
domain: ai
tags:
  - agentic-architecture
  - claude-certification
  - orchestration
  - prompt-engineering
  - mcp
created: 2026-10-03
updated: 2026-10-03
raw: "https://claudecertificationguide.com/learn/1-agentic-architecture/1-1-agentic-loops"
---

# Claude Certification Guide — Architect (Foundations) track

**Authors**: claudecertificationguide.com (community study guide)
**Date**: 2026-09
**Type**: webpage (open certification study guide)
**Source URL**: https://claudecertificationguide.com

## Summary

The free, fully-open Architect (Foundations) certification study guide for building agentic systems with Claude. It is organized into **5 exam domains**, 30 lesson pages, 5 glossaries, and 5 quick references, plus a spaced-repetition **drill set of 257 multiple-choice questions** (each with one correct answer, several distractors, and per-option explanations). The material is vendor-neutral agentic-design guidance that happens to use Claude/Anthropic APIs as the concrete substrate — the principles (loop control via `stop_reason`, deterministic enforcement in code not prompts, hub-and-spoke multi-agent, structured output via tool use, provenance tracking) generalize across agent frameworks.

Drill question counts by domain: {Domain 1: 65, Domain 2: 46, Domain 3: 56, Domain 4: 44, Domain 5: 46}.

This source was transferred from a sibling CFAAI LLM wiki as general (non-SAP) knowledge; the SAP-internal cross-references present in the original pages were stripped on import.

## Key Takeaways

- **Loop control uses `stop_reason`, never text or caps.** Continue on `tool_use`, terminate on `end_turn`. Parsing "I'm done", checking `content[0].type == "text"`, or using an iteration cap as the primary stop are all anti-patterns (caps are safety nets only).
- **Deterministic guarantees need code, not prompts.** "Must always" / compliance / audit / financial / security requirements call for programmatic enforcement — PreToolUse/PostToolUse hooks or a prerequisite gate — not a stronger prompt.
- **Multi-agent = hub-and-spoke.** A coordinator decomposes/sequences/aggregates; specialist subagents are isolated (no shared memory), so all context passes explicitly through the task definition. No agent-to-agent handoff primitive — handoff is escalation to a human with a structured summary.
- **Scope each agent to a small, role-focused tool set.** Selection reliability degrades as the tool count grows regardless of task complexity.
- **Tool descriptions are the primary tool-selection mechanism** — not metadata.
- **Structured output via tool use / JSON schema** beats free-text parsing; include self-check fields so discrepancies surface in data.
- **Escalation triggers on classifier scores below a per-category threshold, not on the agent's self-reported confidence** (poorly calibrated).

## Concepts Covered

- [[wiki/concepts/agentic-architecture-guide]]
- [[wiki/concepts/agentic-arch-orchestration]]
- [[wiki/concepts/agentic-arch-tools-mcp]]
- [[wiki/concepts/agentic-arch-claude-code-config]]
- [[wiki/concepts/agentic-arch-prompt-engineering]]
- [[wiki/concepts/agentic-arch-context-reliability]]

## Entities Mentioned

- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/mcp]]

## Cross-Connections

The loop-control guidance (terminate on `end_turn`, not text) is the rigorous version of the cycle described in [[wiki/concepts/agentic-loop]]. The hub-and-spoke multi-agent model maps directly onto [[wiki/concepts/multi-agent-orchestration]] and [[wiki/concepts/advisor-executor-pattern]]. The CLAUDE.md-hierarchy and skills material corresponds to [[wiki/concepts/claude-md]] and [[wiki/concepts/skill-md]]. The context-window / fresh-session-with-summary guidance is the disciplined form of [[wiki/concepts/context-window-management]] and [[wiki/concepts/harness-engineering]].
