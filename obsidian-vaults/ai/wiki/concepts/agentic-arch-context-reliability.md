---
title: "Context Management & Reliability (Domain 5)"
type: concept
domain: ai
tags:
  - agentic-architecture
  - context-management
  - reliability
  - claude-certification
  - agent-architecture
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/claude-certification-architect-guide]]"
---

# Context Management & Reliability (Domain 5)

Keeping long-running agents accurate. Parent hub: [[wiki/concepts/agentic-architecture-guide]].

## Context-window management (5.1)

Budget the window: keep what still matters, summarise or drop the rest. Stale context signals — the model repeats itself, contradicts earlier statements, or ignores recent tool results — call for a **fresh session seeded with a curated summary**, not more context.

## Escalation & ambiguity (5.2)

Escalate on policy exceptions, destructive operations, and genuine ambiguity. A **classifier score below a per-category threshold** is a valid escalation trigger; an agent's **self-reported confidence is not** (poorly calibrated). Never silently fail — produce a structured handoff.

## Error propagation (5.3)

In multi-agent systems, one agent's error can cascade. Contain failures at the boundary, attach metadata, and prefer partial results with provenance over a silent wrong answer.

## Codebase exploration (5.4)

Explore breadth-first with scoped reads; avoid dumping whole trees into context (degradation). Delegate large scans to a subagent that returns a distilled finding.

## Human review & calibration (5.5) & provenance (5.6)

Calibrate when to ask a human vs act. Track **information provenance** — separate observed facts from inferred claims, cite sources, and check freshness before applying a result to a changed situation.

## Related Concepts

- [[wiki/concepts/agentic-architecture-guide]] — cluster hub
- [[wiki/concepts/agentic-arch-orchestration]] — the loops/subagents this stabilises
- [[wiki/concepts/context-window-management]] — the general token-budget discipline
- [[wiki/concepts/harness-engineering]] — structuring context deliberately

## Key Entities

- [[wiki/entities/anthropic]] — the model whose context window is managed

## Sources

- [[wiki/sources/claude-certification-architect-guide]]
