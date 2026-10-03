---
title: "Claude Code Configuration & Workflows (Domain 3)"
type: concept
domain: ai
tags:
  - agentic-architecture
  - claude-code
  - workflows
  - claude-certification
  - agentic-coding
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/claude-certification-architect-guide]]"
---

# Claude Code Configuration & Workflows (Domain 3)

Configuring Claude Code for real projects. Parent hub: [[wiki/concepts/agentic-architecture-guide]].

## CLAUDE.md hierarchy (3.1)

Instructions load hierarchically (enterprise → project → subdirectory → user); more specific scopes override broader ones. Keep it modular; import shared rules rather than duplicating. Path-specific rules (3.3) load conventions conditionally based on which files are in play.

## Slash commands & skills (3.2)

Custom slash commands are reusable prompt templates; skills are discoverable capability bundles (procedure + optional helper scripts) an agent picks up by name/description. Prefer a skill when behaviour recurs and should be auto-selected.

## Plan mode vs direct execution (3.4)

Plan mode explores and proposes without mutating; direct execution acts. Use plan mode for high-stakes or ambiguous changes and gate execution behind approval.

## Iterative refinement (3.5) & CI/CD (3.6)

Refine via tight feedback loops (run → observe → adjust). In CI/CD, Claude Code runs headless/non-interactive; wire it to checks, keep actions idempotent and permission-scoped, and treat its output as reviewable artifacts.

## Related Concepts

- [[wiki/concepts/agentic-architecture-guide]] — cluster hub
- [[wiki/concepts/agentic-arch-prompt-engineering]] — prompts these workflows drive
- [[wiki/concepts/claude-md]] — the standing-instruction file this domain scopes
- [[wiki/concepts/skill-md]] — the capability-bundle format behind "skills"
- [[wiki/concepts/agentic-coding]] — the paradigm Claude Code implements

## Key Entities

- [[wiki/entities/claude-code]] — the tool being configured
- [[wiki/entities/anthropic]] — defines the config surface

## Sources

- [[wiki/sources/claude-certification-architect-guide]]
