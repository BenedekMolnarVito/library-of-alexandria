---
title: "Eval-Driven Development"
type: concept
domain: ai
tags:
  - methodology
  - evaluation
  - software-engineering
  - tdd
  - agent-patterns
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
---

# Eval-Driven Development

Eval-driven development (EDD) is a software engineering methodology adapted for AI systems: define evaluation criteria before building, then iterate until the criteria are met. It is the AI-era adaptation of test-driven development (TDD), with "evaluations" replacing "tests" to accommodate the probabilistic, non-deterministic outputs of language models. The key discipline is the same as TDD: the criteria must be defined before implementation begins, not derived from inspection of what was actually built.

## Definition

The central practice of eval-driven development:

1. Define what success looks like as a set of measurable, preferably binary criteria
2. Implement an evaluator that measures those criteria automatically
3. Build or optimize the AI system until the evaluator reports passing
4. Use the passing evaluator as the definition of "done"

The difference from ordinary software testing is that AI systems produce outputs that vary, that must be judged rather than merely compared to expected values, and that can "pass" tests in ways that don't reflect the intended behavior. An eval-driven approach addresses this by investing heavily in the evaluator — making it a precise, automation-friendly measurement of the actual success criterion, not a proxy for it.

## How It Works

**Binary criteria are superior to scalar criteria** for the same reason binary tests are superior to "mostly correct" tests in TDD: they eliminate interpretation. An evaluator that says "this prompt produces correct output" is more useful than one that says "this prompt produces output scoring 8.2/10." The binary evaluator produces a sharp signal; the scalar evaluator produces noise that requires meta-judgment to interpret.

**The evaluator is the product**. In traditional software development, tests are scaffolding that checks the product. In eval-driven development for AI, the evaluator often represents more intellectual work than the system being evaluated — it encodes the human judgment about what "good" means in an automated, reproducible form. A team with a great evaluator can run unlimited optimization; a team with a poor evaluator runs blind.

**Connection to RLHF and constitutional AI**: [[karpathy-loop]] optimization loops are informal versions of the formal reinforcement learning from human feedback (RLHF) framework. RLHF trains a reward model on human preference labels and uses it to fine-tune the policy. The Karpathy Loop uses an automated evaluator as the reward signal and uses the LLM's own generation (not gradient descent) as the optimization mechanism. Both are eval-driven; the loop is the lightweight, no-training version.

**Connection to TDD in traditional engineering**: TDD's red-green-refactor cycle maps cleanly: write a failing test (define the evaluator), make it pass (build or optimize until the eval passes), refactor (improve structure without breaking the eval). The discipline is the same; the subject matter (AI system behavior rather than function output) changes the tools but not the methodology.

## Why It Matters

Eval-driven development solves the "how do I know I'm done?" problem that plagues AI system development. Without explicit evaluation criteria, the definition of "good enough" is vague and shifts with the developer's mood. With an evaluator, done has a precise meaning: the eval passes on the test set.

This also enables the [[karpathy-loop]] and [[evolutionary-prompting]] — both require an automated evaluator to function. Eval-driven development is not just a methodology for building AI systems; it is the prerequisite infrastructure for automated optimization of those systems.

[[spec-driven-development]] and eval-driven development are complementary and mutually reinforcing: the spec defines what the system should do (in natural language); the eval operationalizes the spec into an automated measurement. Good specs make good evals easier to write; good evals provide feedback that improves specs.

## In Practice

The practical challenge is evaluator construction. For some domains, building a good evaluator is trivial: "does this code compile?" or "does this test suite pass?" are unambiguous. For others — "is this response helpful?", "is this design beautiful?", "is this argument persuasive?" — the evaluator must itself use an LLM as a judge, raising the question of whether the judge is calibrated correctly.

LLM-as-judge evaluators are increasingly viable for subjective quality dimensions, but require careful design: the judge prompt must specify evaluation criteria precisely, provide calibration examples, and produce binary or small-vocabulary outputs (not 0–100 scores). A well-designed LLM judge can be a reliable evaluator for dimensions like "is this response safe?", "does this answer the question asked?", and "is this consistent with the specified tone?"

## Related Concepts

- [[wiki/concepts/karpathy-loop]] — the optimization loop that eval-driven development enables
- [[wiki/concepts/autoresearch]] — the implementation of an EDD-based optimization loop
- [[wiki/concepts/evolutionary-prompting]] — applying EDD to prompt optimization
- [[wiki/concepts/spec-driven-development]] — the complementary specification discipline
- [[wiki/concepts/dark-code]] — what happens without clear evaluation criteria

## Key Entities

- [[wiki/entities/andrej-karpathy]] — core practitioner of eval-driven optimization loops

## Sources

- [[wiki/sources/karpathy-autoresearch-universal-skill]]
