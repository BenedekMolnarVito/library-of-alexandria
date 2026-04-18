---
title: "skill.md"
type: concept
domain: ai
tags:
  - agent-instructions
  - claude-code
  - extensibility
  - specialization
  - agent-patterns
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/claude-code-skills-got-better]]"
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
  - "[[wiki/sources/master-claude-code-skills]]"
---

# skill.md

A skill.md file is a task-specific markdown document that encodes expertise for a particular domain — UI generation, database queries, autoresearch, documentation optimization, or any other bounded capability. It is Claude Code's extensibility mechanism: rather than baking all domain knowledge into the base agent, users write skill files that inject specialized knowledge on demand. Balu Kosuri demonstrated that skill.md files can themselves be the target of the [[karpathy-loop]] — making skills not just portable but evolvable through automated optimization.

## Definition

skill.md sits one level below [[claude-md]] in the instruction hierarchy. CLAUDE.md is project-wide standing context — it loads every session. skill.md is invoked on demand for a specific task type: when you ask Claude Code to "use the UI skill" or "run autoresearch," the agent loads the relevant skill file, inheriting its specialized instructions, mutation operators, evaluation criteria, and workflow steps.

This separation of concerns — global project context versus task-specific expertise — follows the principle that instruction files should be focused and short. CLAUDE.md remains lean (project conventions, failure mode mitigations); skill.md can be richly detailed without cluttering the base context.

## How It Works

A skill.md file typically encodes:
- **What the skill does** — a clear description of the task domain
- **How to approach it** — methodology, phase sequence, decision rules
- **Evaluation criteria** — how to measure success (feeding directly into [[eval-driven-development]])
- **Mutation operators** (for optimization skills) — the named transformation strategies
- **Edge cases and constraints** — what to do when standard approaches fail

Balu Kosuri's autoresearch skill.md is the canonical example of a sophisticated implementation. It encodes the five-phase autoresearch workflow, six mutation operators, plateau-breaking logic, context window management (sliding window), and an isolated validation set to prevent overfitting the optimized artifact to its evaluator. This degree of methodological encoding — normally implicit in an expert practitioner's head — is what makes skill.md files intellectually valuable artifacts, not just configuration.

The key insight in making skills evolvable is that the skill file can be the target of its own optimization: run autoresearch on the skill.md itself, using task performance as the fitness function. A skill that improves its own description of how to perform a task, measured by how well agents following that description perform the task, is a self-improving system within the broader [[karpathy-loop]] framework.

## Why It Matters

skill.md files represent a form of **institutionalized expertise** — turning tacit knowledge (how an expert approaches a domain) into explicit, machine-readable, LLM-executable instructions. This matters in three ways:

**Portability**: a skill file works across any Claude Code installation, any project, any user. Expertise encoded in a skill file travels with the file.

**Evolvability**: unlike human tacit knowledge (which degrades with employee turnover, is inconsistently transferred, and is hard to improve systematically), skill files can be measured and improved through automated optimization. The skill that performs best on an evaluation set is the one that survives.

**Composability**: multiple skill files can be loaded together. An agent working on a full-stack feature might load a UI skill, a database skill, and a testing skill simultaneously, combining specialized knowledge without conflict.

## In Practice

Claude Code's built-in skills demonstrated immediate quality improvements in tasks like sequential thinking, self-consistency, and multi-step reasoning. User-created skills extend this to domain-specific workflows. The practical discipline is: when you find yourself giving the same instructions to an agent repeatedly across tasks, extract them into a skill.md.

The relationship with [[soul-md]] is worth noting: skill.md encodes *how* to do things; soul.md encodes *who* the agent is. Both augment CLAUDE.md's foundational behavioral constraints, but from different directions — expertise versus identity.

## Related Concepts

- [[wiki/concepts/claude-md]] — the parent pattern; project-level standing context
- [[wiki/concepts/soul-md]] — the identity complement to skill expertise
- [[wiki/concepts/autoresearch]] — the most sophisticated example of a skill.md
- [[wiki/concepts/karpathy-loop]] — skills can be targets of the optimization loop
- [[wiki/concepts/eval-driven-development]] — skills encode their own evaluation criteria
- [[wiki/concepts/context-window-management]] — skills must be concise to fit in context

## Key Entities

- [[wiki/entities/balu-kosuri]] — created the autoresearch universal skill
- [[wiki/entities/anthropic]] — built the skill system into Claude Code

## Sources

- [[wiki/sources/claude-code-skills-got-better]]
- [[wiki/sources/karpathy-autoresearch-universal-skill]]
- [[wiki/sources/master-claude-code-skills]]
