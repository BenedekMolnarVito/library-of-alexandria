---
title: "Vibe Coding"
type: concept
domain: ai
tags:
  - agentic-coding
  - software-engineering
  - ai-coding
  - methodology
  - anti-pattern
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/stop-vibe-coding-4-file-system]]"
  - "[[wiki/sources/dhh-new-way-writing-code-agent-first]]"
---

# Vibe Coding

Vibe coding is the practice of iterating on software with AI assistance driven by feel, intuition, and immediate feedback rather than a plan, specification, or design. The term was coined by Andrej Karpathy affectionately — as a description of a low-friction, high-creativity development mode where you simply describe what you want and react to what you get. It has since acquired a more critical connotation: as a description of development practices that produce [[dark-code]], accumulate hidden technical debt, and fail catastrophically in production when the untested assumptions beneath the working surface are finally exercised.

## Definition

Vibe coding is characterized by four patterns:

1. **No specification upfront** — the developer starts with a vague goal and discovers the requirements through iteration
2. **Approval-based iteration** — the developer approves or rejects AI outputs based on whether they "feel right" rather than against explicit criteria
3. **Accumulating patches** — when something doesn't work, the developer asks the AI to fix it, layering patches on patches rather than redesigning
4. **No ground truth** — there's no definitive document that says what the code is supposed to do, making it impossible to verify correctness

In prototype and personal project contexts, this mode is fine and often optimal. For exploring a problem space, building a demo, or writing throwaway code, the low overhead of vibe coding matches the low stakes of the context.

In production or critical contexts, it's dangerous. The patches accumulate, the structure degrades, the tests don't cover the actual behavior (they test the patched surface, not the intended invariants), and eventually something triggers an untested edge case with consequences.

## How It Works

The "Stop Vibe Coding" movement proposes a 4-file antidote system:

- **spec.md**: what the feature is supposed to do — inputs, outputs, constraints, acceptance criteria
- **plan.md**: how it will be built — the implementation approach, module structure, phases
- **changelog.md**: what has changed and why — the decision log that makes the history legible
- **.cursorrules** (or equivalent CLAUDE.md): behavioral constraints for the AI agent throughout development

This 4-file system doesn't eliminate AI-assisted iteration — it structures it. The developer still moves fast and uses AI heavily. But each iteration is against the spec, logged in the changelog, and constrained by the rules. The vibes are calibrated to a documented reality.

DHH's reframing is useful: the transition from vibe coding to spec-driven development isn't slower or more bureaucratic — it's a change in where the cognitive work happens. Vibe coding front-loads work in debugging and back-loads it in understanding; spec-driven development front-loads it in specification and eliminates much of the debugging.

## Why It Matters

The production failure mode of vibe coding is not a hypothetical — it's the mechanism behind Amazon's [[dark-code]] incident and many similar outages. The connection is direct: vibe coding produces code whose structure reflects accumulated patches rather than intended design, which is precisely what dark code is.

But the critique should be calibrated. Karpathy coined the term approvingly for a reason: the ability to move from idea to working prototype in hours, guided by feel and fast iteration, is genuinely valuable. The error is not using AI for fast iteration; it's using fast-iteration practices (vibe coding) in contexts that require rigorous practices (production systems, critical infrastructure, data integrity). The two modes should coexist — vibe coding for exploration, spec-driven development for production — rather than one replacing the other.

## In Practice

A practical heuristic: vibe code until you're ready to commit, then spec-drive the commit. The exploration phase (figuring out what you want) benefits from low overhead. The implementation phase (building what you've decided you want) benefits from a specification. The transition between the two is the moment when you write the spec from what you've learned in the vibe phase.

The 4-file system is most effective when adopted at the project start rather than retrofitted onto an existing vibe-coded codebase. Retrofitting requires reconstructing intent from code — harder than writing intent down while it's fresh.

## Related Concepts

- [[wiki/concepts/dark-code]] — the production failure mode of vibe coding
- [[wiki/concepts/spec-driven-development]] — the structured alternative
- [[wiki/concepts/claude-md]] — the behavioral constraint layer that partially mitigates vibe coding risks
- [[wiki/concepts/agentic-coding]] — the broader context
- [[wiki/concepts/eval-driven-development]] — the missing evaluation rigor in vibe coding

## Key Entities

- [[wiki/entities/andrej-karpathy]] — coined the term
- [[wiki/entities/dhh]] — prominent advocate for moving beyond vibe coding

## Sources

- [[wiki/sources/stop-vibe-coding-4-file-system]]
- [[wiki/sources/dhh-new-way-writing-code-agent-first]]
