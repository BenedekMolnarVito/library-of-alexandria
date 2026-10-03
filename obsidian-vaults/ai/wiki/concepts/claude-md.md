---
title: "CLAUDE.md (Specification Files)"
type: concept
domain: ai
tags:
  - agent-instructions
  - claude-code
  - specification
  - prompt-engineering
  - agent-patterns
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-claude-md-file]]"
  - "[[wiki/sources/building-claude-code-boris-cherny]]"
---

# CLAUDE.md (Specification Files)

A CLAUDE.md file (also called AGENTS.md, .cursorrules, or generically a "spec file") is a markdown document placed in a project root that loads automatically at every agent session. It encodes standing instructions, behavioral constraints, project conventions, and agent failure-mode mitigations. The key insight behind the pattern is that LLM coding agents fail in predictable ways — and a well-crafted spec file addresses each failure mode systematically before any task begins, rather than correcting mistakes after they occur.

## Definition

CLAUDE.md is a persistent configuration document that acts as the agent's operating manual for a specific project. Unlike a one-off system prompt or a prompt template, it loads automatically whenever an agent session begins in that directory — meaning every task the agent performs is shaped by its contents without the human needing to re-specify constraints each time. It is the difference between training an employee once and correcting them on every shift.

The pattern generalizes across platforms: Claude Code reads CLAUDE.md, GitHub Copilot agent mode reads `.github/copilot-instructions.md`, Cursor uses `.cursorrules`, and the AGENTS.md convention is used for multi-agent orchestration. The underlying idea is identical: a markdown file that tells the agent what to do before it does anything.

## How It Works

Karpathy identified five recurring failure modes in LLM coding agents that CLAUDE.md directly addresses:

1. **Silent wrong assumptions** — the agent assumes something about the codebase, project conventions, or desired behavior that is incorrect, and doesn't flag the assumption
2. **Not flagging confusion** — when the agent doesn't understand the requirements, it guesses rather than asking
3. **Overcomplicating solutions** — the agent writes more code than necessary, introducing complexity and surface area
4. **Touching adjacent code** — the agent modifies files or functions outside the scope of the task
5. **Not cleaning up dead code** — the agent leaves remnants of failed attempts or superseded implementations

Forrest Chang distilled these into four operational principles for CLAUDE.md content:
1. Surface uncertainty and tradeoffs — explicitly ask the agent to flag when it's unsure
2. Minimum code, nothing speculative — constrain the agent to what was asked
3. Touch only what was asked — prevent scope creep to adjacent code
4. Define done and loop until verified — require the agent to check its own output before declaring completion

## Why It Matters

The CLAUDE.md pattern shifts the human's role from reactive corrector to proactive architect. Without it, agents fail in the same ways repeatedly across projects. With it, the failure modes are addressed structurally — the agent's behavior is shaped before it begins, not patched after it fails.

Context window constraints impose an important design discipline: frontier models handle approximately 150–200 standing instructions before coherence degrades, and Claude Code's own system prompt uses roughly 50. Shorter CLAUDE.md files that encode the highest-leverage constraints outperform exhaustive specifications that dilute priority. The discipline of writing a good CLAUDE.md is the discipline of knowing what matters most.

Related variants extend the pattern:
- **[[skill-md]]** — task-specific expertise files (UI generation, database queries, etc.) that encode domain knowledge for particular task types
- **[[soul-md]]** — a persistent identity/context file encoding the agent's goals and accumulated knowledge, distinct from instruction-giving
- **heartbeat.md** — a pattern for tracking agent state and health between sessions

## In Practice

Boris Cherny's account of building Claude Code describes how the system's own behavior was shaped by an internal equivalent of CLAUDE.md — a set of behavioral constraints baked into the agent's setup rather than specified on each task. This meta-application (using the pattern on the tool that uses the pattern) illustrates how structural specification scales: you don't repeat yourself, you encode once and inherit everywhere.

Spec-driven development (see [[spec-driven-development]]) extends this logic to task-level: before asking an agent to implement a feature, you write a spec that defines inputs, outputs, constraints, and acceptance criteria. CLAUDE.md is the project-level complement — the always-on context that the task-level spec builds on top of.

The interplay with [[llm-wiki]] is important: this wiki's `AGENTS.md` file is itself a CLAUDE.md-style specification, encoding the three-layer architecture, page conventions, workflow procedures, and linking rules that govern how the wiki is maintained. Every agent session begins by reading it, ensuring consistent behavior across all ingest, query, and lint operations.

## Related Concepts

- [[wiki/concepts/skill-md]] — task-specific expertise files, the CLAUDE.md for domains
- [[wiki/concepts/soul-md]] — persistent identity file, complementary to CLAUDE.md
- [[wiki/concepts/spec-driven-development]] — task-level analog of CLAUDE.md
- [[wiki/concepts/harness-engineering]] — the infrastructure-level discipline CLAUDE.md feeds into
- [[wiki/concepts/llm-wiki]] — uses AGENTS.md as its foundational schema file
- [[wiki/concepts/context-window-management]] — why shorter CLAUDE.md files are often better
- [[wiki/concepts/dark-code]] — what happens without structural specification
- [[wiki/concepts/agentic-arch-claude-code-config]] — the CLAUDE.md hierarchy per Claude Certification
- [[wiki/concepts/vibe-coding]] — the anti-pattern CLAUDE.md is designed to prevent

## Key Entities

- [[wiki/entities/andrej-karpathy]] — identified the five failure modes
- [[wiki/entities/boris-cherny]] — built Claude Code around these principles
- [[wiki/entities/forrest-chang]] — distilled Karpathy's principles into four rules

## Sources

- [[wiki/sources/karpathy-claude-md-file]]
- [[wiki/sources/building-claude-code-boris-cherny]]
