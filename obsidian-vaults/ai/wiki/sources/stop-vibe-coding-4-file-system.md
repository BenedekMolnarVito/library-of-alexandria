---
title: "Stop Vibe Coding: The 4-File System That Turns AI Agents Into Reliable Engineers"
type: source
domain: ai
tags:
  - spec-driven-development
  - ai-coding
  - agents-md
  - tdd
  - context-engineering
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Stop Vibe Coding The 4-File System That Turns AI Agents Into Reliable Engineers.md]]"
---

# Stop Vibe Coding: The 4-File System That Turns AI Agents Into Reliable Engineers

**Authors**: Kristopher Dunham
**Date**: 2026-03
**Type**: article

## Summary

A METR study found that developers using AI coding tools without structured guidance were 19% slower than developers without AI — while believing themselves 24% faster. The author's response is "spec-driven development," a methodology built on four plain-text files: `spec.md` (what to build: mandate, tech stack, data models, non-goals, boundary conditions, escalation protocol), `AGENTS.md` (how to build it: project conventions, dos/don'ts, reference patterns, institutional memory), `plan.md` (architectural approach for this feature), and `tasks.md` (atomic ordered implementation steps).

A four-phase workflow structures the interaction: (1) generate 10 clarifying questions before touching any code, (2) read-only codebase research and plan.md creation, (3) atomic task decomposition into tasks.md, (4) implement with a human reviewing each increment. TDD is enforced structurally — tests must be written before implementation files, enforced via pre-commit hooks or filesystem rules. When implementation diverges from spec, the agent proposes a spec update and awaits human approval (backward propagation), keeping the spec synchronized with reality.

## Key Takeaways

- METR 2025 study: AI-assisted devs without structured guidance are 19% slower, believe they are 24% faster — the most expensive mistake in software development right now
- 86% of AI-generated code without structured prompts had XSS vulnerabilities (Veracode); ~4x code duplication increase 2020–2024 (GitClear)
- UserVille: model F1 score jumped from 44 to 65 by replacing vague prompts with precise specs — same model, better instructions
- `spec.md` must include: one-sentence mandate, tech stack with exact versions, data models, explicit non-goals, boundary conditions, escalation protocol
- `AGENTS.md` = institutional memory: grows over time with team decisions, dos/don'ts, gold-standard reference files, and file-scoped test commands
- Four-phase workflow: clarify → plan → decompose → implement-and-review
- TDD enforcement: tests must be written before implementation; otherwise agents write tests that pass by matching code, not spec
- Backward propagation: when implementation diverges from spec, agent proposes spec update and awaits human approval

## Entities Mentioned

- [[wiki/entities/kristopher-dunham]]
- [[wiki/entities/metr]]
- [[wiki/entities/veracode]]
- [[wiki/entities/gitclear]]
- [[wiki/entities/usersville]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/cursor]]
- [[wiki/entities/copilot-workspace]]
- [[wiki/entities/anthropic]]

## Concepts Covered

- [[wiki/concepts/spec-driven-development]]
- [[wiki/concepts/vibe-coding]]
- [[wiki/concepts/agents-md]]
- [[wiki/concepts/context-engineering]]
- [[wiki/concepts/4-file-system]]
- [[wiki/concepts/tdd-with-ai-agents]]
- [[wiki/concepts/backward-propagation]]
- [[wiki/concepts/escalation-protocol]]
- [[wiki/concepts/ai-coding-agent-reliability]]
- [[wiki/concepts/prompt-engineering-vs-specification]]

## Notable Quotes

> "The gap between perceived speed and real speed is the most expensive mistake in software development right now."

> "The model didn't change. The instructions did."

> "AI agents, by default, won't [ask clarifying questions]. They'll fill in every gap with a plausible-sounding assumption, and those assumptions compound across hundreds of decisions."

> "Code-to-spec, not just spec-to-code. It's what separates a one-time planning exercise from a production-grade practice."

## Cross-Connections

The `AGENTS.md` file described here is directly instantiated in this Library of Alexandria project's own schema. The spec-driven methodology is the engineering complement to [[wiki/sources/product-minded-engineers-ai-native]] — both argue that problem definition and precision of intent are the bottleneck, not execution. The four-phase workflow mirrors the `deepagents` `write_todos` planning tool behavior in [[wiki/sources/langchain-deep-agents]]. The Generator+Critic pattern from [[wiki/sources/multi-agent-architecture-patterns]] maps onto the TDD loop described here. The same author's [[wiki/sources/paperclip-ai-governance-platform]] extends this methodology with organizational-level governance.
