---
title: "Spec-Driven Development"
type: concept
domain: ai
tags:
  - software-engineering
  - agentic-coding
  - specification
  - methodology
  - dark-code
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/amazon-fired-engineers-ai-dark-code]]"
  - "[[wiki/sources/building-claude-code-boris-cherny]]"
  - "[[wiki/sources/dhh-new-way-writing-code-agent-first]]"
---

# Spec-Driven Development

Spec-driven development is the practice of writing a complete specification before asking an AI agent to implement anything. The specification defines inputs, outputs, constraints, edge cases, and acceptance criteria — all the things the engineer must have thought through before the AI begins. It was mandated at Amazon after the [[dark-code]] incident, advocated by DHH as his primary workflow shift with AI coding agents, and reflected in Boris Cherny's account of how Claude Code itself was built. The discipline forces the human to think before delegating and gives the AI a verifiable target rather than an underspecified goal.

## Definition

A specification in this context is not a high-level design document — it is an **executable description** of what correct implementation looks like. It should be specific enough that two reasonable engineers, given only the spec, would produce functionally equivalent implementations. It should contain:

- **Input/output definition**: what does the function/feature take as input and what does it produce?
- **Constraint enumeration**: what must always be true? What must never happen? What are the invariants?
- **Edge case specification**: what happens at boundaries, with empty inputs, with malformed data, at scale limits?
- **Acceptance criteria**: what tests constitute evidence of correctness? What does "done" mean?
- **Anti-specification**: what explicitly should the implementation NOT do? (Constrains scope creep)

The anti-specification is particularly important for AI coding agents, which tend toward overbuilding: they add handling for cases the engineer didn't ask about, introducing complexity and surface area. Explicitly specifying what the implementation should NOT include is as important as specifying what it should.

## How It Works

The workflow:

1. Engineer writes the specification in markdown (or a structured format the agent can read)
2. Engineer reviews the spec for completeness — the review reveals assumptions and edge cases that weren't obvious until written down
3. Agent implements against the spec
4. Agent evaluates its own implementation against the acceptance criteria before declaring done
5. Engineer reviews the implementation against the spec (not against intuition) — the spec is the verification target

Step 4 is critical and often omitted: the agent checking its own work against explicit criteria is more reliable than assuming the initial implementation is correct. This is [[eval-driven-development]] applied at the task level — the criteria are defined before implementation begins, not derived afterward.

DHH's characterization of his workflow shift captures the essence: "I stopped telling AI what to do and started telling AI what to build." The "what to do" framing is procedural and vague; the "what to build" framing is outcome-focused and specific. The spec is the articulation of "what to build" that is complete enough to be verified.

## Why It Matters

Spec-driven development solves three problems simultaneously:

**Dark code prevention**: a spec is documentation of intent. When the implementation drifts from the intent (which AI-generated code often does in subtle ways), the spec makes the drift visible. Code review becomes "does this implement the spec?" rather than "is this code correct?" — a much more tractable question.

**Scope control**: [[vibe-coding]] produces scope creep because there's no authoritative definition of what's in and what's out. A spec with an anti-specification is a scope boundary that both the human and the AI can reference. The agent can't add features that aren't in the spec because the spec explicitly excludes them.

**Forced clarity**: writing a complete spec forces the engineer to think through the problem before implementation begins. This catches design flaws that would otherwise be discovered expensively during implementation. The spec is a cheap design simulation.

## In Practice

The connection to [[claude-md]] is important: CLAUDE.md is the project-level spec (standing constraints, behavioral rules, naming conventions); the task-level spec is written fresh for each implementation task. Together they form a layered specification that constrains AI behavior at both the session level and the task level.

Amazon's mandatory spec requirement applied specifically to AI-assisted commits to production services — not to all development. This is a sensible calibration: spec-driven development has overhead that's worth paying for critical code and not worth paying for experimental or low-stakes code. The discipline scales with the stakes.

Boris Cherny's account of building Claude Code describes an internal specification culture where behavioral requirements were written before implementation, enabling rapid iteration without specification drift. The specification was the product; the code was the implementation.

## Related Concepts

- [[wiki/concepts/dark-code]] — what happens without spec-driven development
- [[wiki/concepts/vibe-coding]] — the anti-pattern spec-driven development replaces
- [[wiki/concepts/claude-md]] — the project-level complement to task-level specs
- [[wiki/concepts/eval-driven-development]] — the methodology that spec-driven development implements
- [[wiki/concepts/harness-engineering]] — specs as the input to agent harness configuration
- [[wiki/concepts/agentic-coding]] — the context in which spec-driven development matters most

## Key Entities

- [[wiki/entities/amazon]] — mandated spec-driven development after dark code incident
- [[wiki/entities/boris-cherny]] — built Claude Code with spec-driven culture
- [[wiki/entities/dhh]] — adopted spec-driven development as primary AI coding workflow

## Sources

- [[wiki/sources/amazon-fired-engineers-ai-dark-code]]
- [[wiki/sources/building-claude-code-boris-cherny]]
- [[wiki/sources/dhh-new-way-writing-code-agent-first]]
