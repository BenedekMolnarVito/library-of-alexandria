---
title: "Dark Code"
type: concept
domain: ai
tags:
  - agentic-coding
  - software-engineering
  - code-quality
  - amazon
  - ai-risks
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/amazon-fired-engineers-ai-dark-code]]"
---

# Dark Code

Dark code is Amazon's term for AI-generated code that nobody on the engineering team fully understands — it compiles, passes tests, and runs in production, but cannot be safely modified. The root cause is that LLM coding agents optimize for passing tests and satisfying specified requirements, not for human comprehensibility. Code that achieves the test suite with minimum friction is not necessarily code that reflects the intended design, handles edge cases explicitly, or makes its logic legible to the next engineer who touches it. Amazon's December 2024 production outage, caused by dark code in a critical service, prompted mandatory [[spec-driven-development]] across teams.

## Definition

Dark code is not buggy code — that would be caught by tests. It is code that:
- Is syntactically and semantically correct
- Passes all existing tests
- Works correctly for the cases the tests cover
- Cannot be understood well enough to reason about untested cases
- Cannot be safely modified without risk of introducing invisible errors
- May have hidden assumptions that aren't reflected in comments, variable names, or structure

The "dark" metaphor is apt: the code is present but opaque. It blocks useful light (understanding) from passing through the system.

## How It Works

The mechanism that produces dark code is the mismatch between what LLMs optimize for and what humans need. An LLM tasked with "implement this feature so the tests pass" will do exactly that. It may use an approach that happens to work for the tested cases while being systematically wrong for untested ones. It may inline complex logic without explanatory naming. It may use obscure language features that achieve the result efficiently but are unfamiliar to most readers. It may omit the conceptual scaffolding (comments explaining why, not just what) that makes code navigable.

The problem compounds with the [[vibe-coding]] pattern: when engineers iterate with AI without a plan, each iteration produces plausible-looking code that patches the previous output. After five iterations, the code may technically work while being structurally incoherent. No single piece of code is obviously wrong; the aggregate is a maze.

Amazon's December 2024 incident illustrated the failure mode: an AI-generated function in a critical service had a subtle conditional logic error that wasn't covered by the test suite. The function was so complex (and so devoid of explanatory structure) that no engineer on the team could quickly understand what it was supposed to do, making diagnosis and fix extremely slow. The cost was not just the downtime — it was the months of subsequent work to replace dark code with comprehensible implementations.

## Why It Matters

Dark code represents a form of technical debt that is qualitatively worse than ordinary technical debt. Ordinary technical debt (messy code, duplicated logic, lack of abstraction) can be refactored by an engineer who understands the system. Dark code cannot be refactored because the engineer doesn't understand the system well enough to know what "correct" refactoring would look like.

The danger scales with the proportion of dark code in a codebase. A codebase that is 5% dark code has isolated problem areas. A codebase that is 30% dark code — common when teams adopt AI-assisted development without structural safeguards — has a systemic comprehensibility problem. Debugging, onboarding new engineers, and implementing new features all become dramatically harder.

The connection to tacit knowledge is important: when the code is opaque, the team's operational knowledge of what the code does can only be maintained by the original engineer who worked with the AI to produce it. When that engineer leaves, the knowledge goes with them. Dark code destroys institutional knowledge even faster than ordinary undocumented code.

## In Practice

Amazon's response — mandatory [[spec-driven-development]] — addresses dark code at its root. If the engineer writes a complete specification before asking the AI to code, the specification serves as documentation of intent. If the AI's implementation doesn't match the specification's intent, the mismatch is visible. The spec is also a target for the human review: "does this code implement the spec correctly?" is a tractable review question; "does this code do the right thing?" without a spec is not.

Other mitigations: pair programming patterns where humans author the conceptual structure and AI fills in the implementation; code review requirements specifically targeting comprehensibility (not just correctness); and deliberate limits on AI-assisted commits to critical infrastructure without additional human review.

## Related Concepts

- [[wiki/concepts/spec-driven-development]] — the direct mitigation Amazon adopted
- [[wiki/concepts/vibe-coding]] — the development practice most likely to produce dark code
- [[wiki/concepts/claude-md]] — structural specification that reduces dark code risk
- [[wiki/concepts/agentic-coding]] — the context in which dark code emerges
- [[wiki/concepts/eval-driven-development]] — testing rigor that can catch dark code earlier

## Key Entities

- [[wiki/entities/amazon]] — coined the term after the December 2024 incident

## Sources

- [[wiki/sources/amazon-fired-engineers-ai-dark-code]]
