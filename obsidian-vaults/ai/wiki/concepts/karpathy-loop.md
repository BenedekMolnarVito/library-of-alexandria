---
title: "Karpathy Loop"
type: concept
domain: ai
tags:
  - optimization
  - autoresearch
  - evolutionary-algorithms
  - agent-patterns
  - karpathy
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
  - "[[wiki/sources/300-dollars-auto-research-karpathy-loop]]"
---

# Karpathy Loop

The Karpathy Loop is a general-purpose optimization algorithm based on a single insight: let an AI agent run experiments, measure results, keep what works, throw away what doesn't, and repeat until the objective is met. The loop is deceptively simple — three ingredients, a while-loop, and a fitness function — but its generality is remarkable. It was first used to optimize ML training code; it has since been applied to text-to-image prompts, skill.md files, documentation quality, and any domain where an automated evaluator can score a candidate.

## Definition

The loop has three required ingredients: an **objective metric** (a number that measures success, ideally binary — pass or fail), an **automated measurement tool** (something that scores a candidate without human intervention), and **something to change** (the artifact being optimized — code, a prompt, a configuration file, a markdown document).

Given those three, the algorithm is:
1. Generate a candidate (initial version or mutation of current best)
2. Measure it with the evaluator
3. If score improves, keep it; otherwise discard and try again
4. Repeat until the metric is satisfied or a budget is exhausted

This is stochastic hill-climbing — a classic optimization technique — but the LLM provides the mutation intelligence. Instead of random bit-flips, the agent generates semantically coherent mutations informed by why the previous attempt scored as it did.

## How It Works

Andrej Karpathy's original application was ML training code: an agent would rewrite a training loop, run it, compare validation loss, and keep the rewrite only if loss improved. The agent accumulated a series of successful rewrites, each building on the last — a gradient descent through the space of training scripts.

Nick Saraev generalized it to text-to-image prompt optimization. Starting from a prompt scoring 32/40 on a visual quality rubric, the loop reached 40/40 in 12 minutes without human intervention, cycling through mutations (word substitutions, structural changes, emphasis shifts) and discarding anything that scored lower.

Balu Kosuri generalized it further into a **universal skill** by adding infrastructure around the core loop: repo discovery, target suggestion, metric definition, and baseline measurement as setup phases, then the loop itself with six named mutation operators (see [[autoresearch]]). This made the loop portable across any optimization domain.

The key efficiency insight is that the measurement step must be **automated**. If a human must evaluate each candidate, the loop becomes impractical. The skill of designing the Karpathy Loop for a new domain is largely the skill of designing the automated evaluator.

## Why It Matters

The Karpathy Loop shifts optimization from a human craft to an engineering problem. Once you have a metric and an evaluator, the loop does the work. This is particularly powerful in AI-adjacent domains (prompt engineering, agent configuration, code quality) where the search space is vast and gradients are not analytically available.

The loop also captures a deeper epistemological point: **most things that feel like creative craft are actually optimization problems in disguise**. Writing a good prompt feels creative, but it has a measurable quality (does the model produce the right output?) and a mutable artifact (the prompt text). Substituting evaluation for intuition removes the human bottleneck.

The plateau-breaker mechanism — discarding all structure and rebuilding from scratch after five stale runs — mirrors simulated annealing's temperature reset. Without it, the loop converges to local optima and stagnates. With it, the search space remains globally explorable even after local convergence. This detail separates a useful loop from a robust one.

## In Practice

The loop's economics depend entirely on the cost of the measurement step. If evaluation is cheap (a fast unit test, a local model scoring rubric), loops of hundreds of iterations are viable for cents. If evaluation is expensive (human review, API calls, long test suites), the loop must be designed more carefully — using a fast proxy metric first, then validating against the expensive oracle only for promising candidates.

Intelligence arbitrage applies directly: use a cheap/fast local model for generating mutations, reserve the frontier API for evaluating borderline cases. See [[intelligence-arbitrage]] for the cost-routing framework.

## Related Concepts

- [[wiki/concepts/autoresearch]] — the full implementation of this loop for ML and skill optimization
- [[wiki/concepts/evolutionary-prompting]] — the prompt-specific application
- [[wiki/concepts/eval-driven-development]] — the methodology that makes loops measurable
- [[wiki/concepts/intelligence-arbitrage]] — routing mutations/evaluations to optimal models
- [[wiki/concepts/agentic-loop]] — the broader agent execution cycle this loop runs within
- [[wiki/concepts/soul-md]] — Nate B Jones' use of the loop with persistent agent identity

## Key Entities

- [[wiki/entities/andrej-karpathy]] — originator
- [[wiki/entities/nick-saraev]] — text-to-image generalization
- [[wiki/entities/balu-kosuri]] — universal skill generalization

## Sources

- [[wiki/sources/karpathy-autoresearch-universal-skill]]
- [[wiki/sources/300-dollars-auto-research-karpathy-loop]]
