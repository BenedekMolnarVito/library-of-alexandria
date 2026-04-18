---
title: "Autoresearch"
type: concept
domain: ai
tags:
  - optimization
  - agent-patterns
  - prompt-optimization
  - karpathy
  - mutation-operators
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
---

# Autoresearch

Autoresearch is Andrej Karpathy's specific implementation of the [[karpathy-loop]] for ML research: an agent autonomously rewrites training code, evaluates the result against a fixed metric, and keeps improvements or reverts — cycling until it reaches a target or exhausts its budget. Balu Kosuri extended this into a universal skill that can be applied to any optimization target (prompts, documentation, configuration files, agent instructions) by packaging it as a portable `skill.md` with defined phases, mutation operators, and plateau-breaking logic.

## Definition

Autoresearch is distinguished from generic optimization loops by two structural features: **systematic mutation operators** (named strategies for transforming the candidate) and **phase separation** (distinct stages of setup before the loop begins). These features make the loop more reliable and its behavior more predictable across different domains.

In Karpathy's original ML context, autoresearch meant: given a training script, autonomously improve it by rewriting sections, running the training job, comparing loss curves, and retaining only rewrites that improve the metric. The agent doesn't need to understand why a change helps — it needs only to measure whether it does.

## How It Works

Balu Kosuri's universal implementation proceeds through five phases:

1. **Repo discovery** — the agent reads the codebase, documentation, and existing context to understand what it's working with
2. **Target suggestion** — the agent identifies what to optimize (a specific prompt, a configuration, a documentation page)
3. **Metric definition** — the agent proposes a measurable, ideally binary success criterion
4. **Baseline measurement** — the current version is scored so improvements have a reference point
5. **Autoresearch loop** — the core keep/discard cycle with mutation operators applied until the target is met

The six **mutation operators** are the heart of Kosuri's contribution. Each represents a different axis of transformation:

- **add_constraint** — tighten the target by adding a specific rule or boundary
- **negative_example** — add a counterexample showing what the target should not do
- **restructure** — change the organization or ordering without changing the content
- **tighten_language** — reduce verbosity and increase precision
- **remove_bloat** — delete redundant or non-contributory sections
- **add_counterexample** — the most powerful operator in empirical testing (24→40/40 in 14 runs in the documentation SEO example): add a specific case that forces the model to distinguish correct from incorrect behavior

The selection of which operator to apply at each iteration is itself a model decision, informed by why the previous attempt scored as it did — making the loop semi-adaptive rather than purely random.

## Why It Matters

Autoresearch operationalizes [[eval-driven-development]] at machine speed. The gap between "write a prompt" and "write a good prompt" has historically been filled by human iteration, intuition, and luck. Autoresearch replaces that with a mechanical process: define success, instrument it, and iterate. The human's job shifts from writing the final artifact to designing the evaluator and setting the target.

The naming of mutation operators is also intellectually significant. By giving names to distinct transformation strategies, Kosuri made the search space legible. An agent applying `add_counterexample` knows it's trying to improve discrimination, not just making arbitrary changes. This is the difference between informed search and random walk — the operators encode domain knowledge about what tends to help.

The plateau-breaker mechanism deserves special mention: after five consecutive runs with no improvement, the agent discards the current structure entirely and regenerates from scratch. This is the autoresearch implementation of simulated annealing — escaping local optima by accepting a temporary regression in order to explore a different region of the solution space. Without it, the loop reliably converges to mediocre local maxima.

## In Practice

The universal skill packaging means autoresearch can be dropped into any project as a `skill.md` file and invoked by Claude Code or any compatible agent. The skill file encodes the five phases, the mutation operators, plateau-breaking logic, and evaluation strategy. It also includes context window management (sliding window for long runs) as one of its seven advanced features, preventing context overflow during extended optimization sessions.

The most practically important design decision is the evaluator. Binary evaluators (pass/fail) outperform scalar ones (0–100 scores) because they eliminate judgment calls about whether a small score improvement justifies keeping a mutation. When the target is binary, the loop's behavior is sharp and unambiguous.

## Related Concepts

- [[wiki/concepts/karpathy-loop]] — the parent pattern this implements
- [[wiki/concepts/evolutionary-prompting]] — the prompt-specific application of these techniques
- [[wiki/concepts/eval-driven-development]] — the methodology underlying the loop
- [[wiki/concepts/skill-md]] — the packaging format used to make autoresearch portable
- [[wiki/concepts/context-window-management]] — the sliding window feature for long runs

## Key Entities

- [[wiki/entities/andrej-karpathy]] — original ML autoresearch
- [[wiki/entities/balu-kosuri]] — universal skill implementation

## Sources

- [[wiki/sources/karpathy-autoresearch-universal-skill]]
