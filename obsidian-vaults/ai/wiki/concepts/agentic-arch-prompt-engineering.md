---
title: "Prompt Engineering & Structured Output (Domain 4)"
type: concept
domain: ai
tags:
  - agentic-architecture
  - prompt-engineering
  - structured-output
  - claude-certification
  - agent-architecture
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/claude-certification-architect-guide]]"
---

# Prompt Engineering & Structured Output (Domain 4)

Getting reliable, machine-usable output from the model. Parent hub: [[wiki/concepts/agentic-architecture-guide]].

## System prompts with explicit criteria (4.1)

State role, task, explicit success criteria, and output contract. Explicit criteria beat vague instructions; the model can only satisfy constraints it is told.

## Few-shot prompting (4.2)

Examples teach format and edge-case handling. Choose representative, consistent examples; contradictory or off-distribution examples hurt more than help.

## Structured output (4.3)

Prefer **tool use / JSON schema** for structured output over free-text parsing — the schema guarantees the interface (not the truth of values). Include self-check fields (e.g. `calculated_total` vs `stated_total`) so discrepancies are detectable in data, not prose.

## Validation, retry & feedback loops (4.4)

On a failure, send the original request + the failed output + the specific error back to the model (retry-with-feedback). Cap retries; escalate or degrade gracefully rather than looping forever.

## Batch processing (4.5) & multi-pass review (4.6)

Batch independent items for throughput; multi-pass/multi-instance review runs separate passes (or instances) to draft then critique/verify, catching errors a single pass misses. Keep passes independent so a later pass isn't anchored.

## Related Concepts

- [[wiki/concepts/agentic-architecture-guide]] — cluster hub
- [[wiki/concepts/agentic-arch-context-reliability]] — reliability of these outputs at scale
- [[wiki/concepts/eval-driven-development]] — defining success criteria first
- [[wiki/concepts/advisor-executor-pattern]] — the draft-then-critique multi-pass idea

## Key Entities

- [[wiki/entities/anthropic]] — the model and tool-use/JSON-schema surface

## Sources

- [[wiki/sources/claude-certification-architect-guide]]
