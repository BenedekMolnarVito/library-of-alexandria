---
title: "Boris Cherny"
type: entity
domain: ai
tags:
  - person
  - engineer
  - anthropic
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/building-claude-code-boris-cherny]]"
---

# Boris Cherny

Boris Cherny is the software engineer at [[wiki/entities/anthropic]] who built [[wiki/entities/claude-code]] from the ground up — turning the concept of an AI-native coding assistant into one of the most widely-used agentic development tools of 2025–2026.

## Background / History

Before Anthropic, Cherny worked at PlanGrid (construction tech), where he built developer tooling at scale. He is a recognized figure in the TypeScript community, having contributed to the language ecosystem and authored *Programming TypeScript* (O'Reilly), a well-regarded book on typed JavaScript that demonstrates his depth in language tooling and developer experience. His combination of systems-level thinking and sensitivity to developer ergonomics made him a natural fit for building a coding agent from scratch.

## Key Contributions / Features

**Building Claude Code**: Cherny made the foundational architectural and product decisions that shaped Claude Code's character. Rather than Python (the obvious choice given AI tooling's ecosystem), he chose TypeScript — reasoning that TypeScript's reach across web, server, and tooling domains would maximize the number of engineers who could contribute and extend the codebase. He also made the deliberate decision to open-source the majority of Claude Code, a departure from typical AI company practice that aligned with his developer-community values.

**"The model IS the product"**: Cherny's central product philosophy, as shared in his interview with [[wiki/entities/gergely-orosz]] for The Pragmatic Engineer, is that UI and UX refinements are largely irrelevant if the underlying model cannot perform the task at hand. This insight guided Claude Code's iterative development: rather than spending engineering cycles on interface polish, the team focused relentlessly on expanding the model's capability envelope — what it could reliably do, and at what cost.

**Agentic architecture decisions**: Under Cherny's direction, Claude Code was designed as a genuinely autonomous programmer rather than a glorified autocomplete tool. It can read and write files, run shell commands, browse the web, call external APIs, and orchestrate sub-agents — placing it closer to an autonomous software engineer than a coding copilot.

## Role in AI Landscape

Cherny's work on Claude Code represents one of the clearest examples of an individual engineer's design philosophy becoming the shape of a product category. His emphasis on model capability over interface, his TypeScript choice, and his openness about the architecture (through interviews and the open-source release) have collectively shaped how the industry thinks about agentic coding tools. The product he built became the primary reference point against which [[wiki/entities/openclaw]], [[wiki/entities/codex-cli]], and other tools are compared.

## Connections

- **Related entities**: [[wiki/entities/anthropic]], [[wiki/entities/gergely-orosz]], [[wiki/entities/claude-code]], [[wiki/entities/claude-model-family]]
- **Key concepts**: [[wiki/concepts/agentic-coding]], [[wiki/concepts/agent-first-development]]
- **Sources**: [[wiki/sources/building-claude-code-boris-cherny]]
