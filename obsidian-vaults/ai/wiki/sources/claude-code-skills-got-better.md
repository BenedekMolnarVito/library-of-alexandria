---
title: "Claude Code Skills Just Got Even Better"
type: source
domain: ai
tags:
  - claude-skills
  - skill-evaluation
  - agent-workflows
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Claude Code Skills Just Got Even Better.md]]"
---

# Claude Code Skills Just Got Even Better

**Authors**: Nate Herk | AI Automation
**Date**: 2026-03
**Type**: video-transcript

## Summary

This video explains Claude Code's skill system and covers Anthropic's new official 'skill creator skill' — a meta-skill that builds, evaluates, benchmarks, and trigger-tunes other skills. Two types of skills are distinguished: capability uplift skills (teach the model to do something better) and encoded preference skills (sequential workflows specific to the user). The video ends with a live demo building a branded YouTube weekly roundup PDF report skill.

## Key Takeaways

- Two skill types: capability uplift (e.g. better front-end design prompts) and encoded preference (sequential user-specific workflows).
- Capability uplift skills may become obsolete as base models improve; encoded preference skills are more durable.
- Anthropic's skill creator skill encodes their full best-practice guide for building, testing, and refining skills.
- Evals let agents compare skill output against gold examples to catch regressions or spot when a skill is no longer needed.
- Benchmarks provide pass rate, time, and token usage comparisons across model versions.
- Trigger tuning optimizes skill descriptions so the agent calls the right skill from natural language.
- Anthropic prediction: 'Over time, a natural language description of what the skill should do may be enough — the model figures out the rest.'

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/claude-opus-4-6]]
- [[wiki/entities/claude-opus-5]]

## Concepts Covered

- [[wiki/concepts/claude-skills]]
- [[wiki/concepts/capability-uplift-skills]]
- [[wiki/concepts/encoded-preference-skills]]
- [[wiki/concepts/skill-evaluation]]
- [[wiki/concepts/trigger-tuning]]
- [[wiki/concepts/skill-benchmarking]]
- [[wiki/concepts/agent-workflows]]

## Notable Quotes

> "Over time, a natural language description of what the skill should do may be enough, with the model figuring out the rest."

> "Capability uplift skills might fade over time… encoded preference skills will probably stay pretty durable because the process is very specific usually to you."

## Cross-Connections

Closely tied to [[wiki/sources/claude-code-paperclip-destroyed-openclaw]] and [[wiki/sources/how-to-build-claude-agent-teams]] — skills are the building blocks that all agent systems rely on. The skill evaluation/benchmark concept parallels broader ML evaluation practices applied to prompt engineering, echoing the eval infrastructure discussion in [[wiki/sources/300-dollars-auto-research-karpathy-loop]]. The skill-learning architecture has parallels to [[wiki/sources/hermes-agent-vs-openclaw]]'s session-to-skill conversion. The concept of encoded preferences as durable vs capability uplift as transient connects to the context portability problem in [[wiki/sources/anthropic-openai-memory-context-portability]].
