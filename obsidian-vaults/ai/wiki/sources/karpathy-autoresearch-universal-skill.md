---
title: "I Turned Andrej Karpathy's Autoresearch Into a Universal Skill"
type: source
domain: ai
tags:
  - karpathy
  - autoresearch
  - prompt-optimization
  - evolutionary-ai
  - eval-driven
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/I Turned Andrej Karpathy's Autoresearch Into a Universal Skill.md]]"
---

# I Turned Andrej Karpathy's Autoresearch Into a Universal Skill

**Authors**: Balu Kosuri
**Date**: 2026-04
**Type**: article

## Summary

Balu Kosuri takes Karpathy's 'autoresearch' project (an AI agent that autonomously optimizes ML training code via a keep/discard loop) and generalizes it into a universal prompt optimization skill applicable to any domain with a measurable output. Inspired by Nick Saraev's application of the pattern to text-to-image prompts, Kosuri built a skill.md with 5 phases, then iteratively improved it with 7 advanced features including eval isolation, a fixed validation set, structured mutation operators, context window management, and a plateau-breaker mechanism. The result reached 40/40 on documentation SEO in 14 runs.

## Key Takeaways

- Karpathy's autoresearch pattern: three ingredients — objective metric, automated measurement tool, something to change — maps cleanly onto prompt optimization
- Nick Saraev applied it to text-to-image prompt optimization: started at 32/40, reached 40/40 in 12 minutes using 4 binary yes/no criteria
- Universal skill phases: repo discovery → target suggestion → metric definition → baseline → autoresearch loop
- Key improvements over v1: eval isolation (judge output without seeing the prompt), fixed validation set, 6 named mutation operators (add constraint, negative example, restructure, tighten language, remove bloat, add counterexample)
- Plateau breaker: after 5 stale runs, discard the prompt structure entirely and rebuild from scratch using only criteria + failure history
- Documentation SEO example: 24/40 → 40/40 in 14 runs; add_counterexample was the most effective mutation operator
- The skill is self-critiquing: Kosuri ran the v1 skill through analysis and each identified gap became a specific targeted fix

## Entities Mentioned

- [[wiki/entities/balu-kosuri]]
- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/nick-saraev]]
- [[wiki/entities/claude]]
- [[wiki/entities/cursor]]
- [[wiki/entities/gemini]]

## Concepts Covered

- [[wiki/concepts/autoresearch]]
- [[wiki/concepts/prompt-optimization]]
- [[wiki/concepts/evolutionary-prompting]]
- [[wiki/concepts/automated-evaluation]]
- [[wiki/concepts/binary-eval-criteria]]
- [[wiki/concepts/mutation-operators]]
- [[wiki/concepts/self-improving-ai]]
- [[wiki/concepts/eval-driven-development]]

## Notable Quotes

> "Let an AI agent run experiments on its own, measure the results, keep what works, throw away what doesn't, and repeat until it's good."

> "The mapping was perfect. And if it worked for diagrams, it could work for anything with a measurable output."

## Cross-Connections

Autoresearch is the evolutionary/optimization sibling of the LLM wiki pattern — both are compounding loops where AI improves an artifact over time. The binary eval criteria framework connects directly to eval-driven development (RLHF, constitutional AI benchmarking). The 'plateau breaker' concept mirrors simulated annealing in classical optimization. Both articles by [[wiki/entities/balu-kosuri]] in this vault represent a hands-on practitioner's perspective on building with Karpathy-inspired ideas. See also [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]] for Kosuri's implementation of the LLM wiki pattern.
