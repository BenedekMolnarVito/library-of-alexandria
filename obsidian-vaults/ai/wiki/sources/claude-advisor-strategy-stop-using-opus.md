---
title: "Claude Just Told Us to Stop Using Their Best Model"
type: source
domain: ai
tags:
  - model-cost-optimization
  - advisor-strategy
  - claude-code
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Claude Just Told Us to Stop Using Their Best Model.md]]"
---

# Claude Just Told Us to Stop Using Their Best Model

**Authors**: Nate Herk | AI Automation
**Date**: 2026-04
**Type**: video-transcript

## Summary

Anthropic introduced an 'advisor strategy' in their Messages API: pair an expensive model (Opus) as an advisor with a cheaper executor (Sonnet or Haiku) that only escalates to the advisor when it detects a hard problem. Nate Herk demos this with a custom customer service dashboard, showing 21x cost differences between Haiku and Opus on easy queries, while quality on hard queries remains near-Opus-level. In Claude Code, the equivalent is using Opus only in plan mode and Sonnet for execution.

## Key Takeaways

- The advisor strategy pairs a cheap executor (Haiku/Sonnet) with Opus as an advisor, called only when needed.
- Anthropic's evals: Sonnet+Opus advisor showed +2.7pp on SWE-bench and ~12% cost reduction vs Sonnet alone.
- Haiku+Opus on browse-comp: 41.2% vs Haiku solo at 19.7% — more than double performance at still lower cost than Opus alone.
- Pricing: Opus $5/$25 per M tokens (in/out), Sonnet $3/$15, Haiku $1/$5.
- In Claude Code: use /model opus plan to get Opus in plan mode, Sonnet 4.6 everywhere else.
- The advisor strategy only exists in the Messages API, not natively in Claude Code — but plan mode achieves the same effect.
- Don't implement without testing 100+ prompts first — cost savings are only valid if quality isn't sacrificed.

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-opus-4-6]]
- [[wiki/entities/claude-sonnet-4-6]]
- [[wiki/entities/claude-haiku-4-5]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/messages-api]]

## Concepts Covered

- [[wiki/concepts/advisor-strategy]]
- [[wiki/concepts/model-cost-optimization]]
- [[wiki/concepts/executor-advisor-pattern]]
- [[wiki/concepts/agentic-tasks]]
- [[wiki/concepts/token-cost-management]]
- [[wiki/concepts/messages-api]]
- [[wiki/concepts/plan-mode]]

## Notable Quotes

> "If you have a task that is three steps long, A, B, and C, but only step A is difficult enough where you need an expensive reasoning model like Opus, then why would you waste money having Opus do steps B and C?"

## Cross-Connections

Directly relates to model pricing strategy — important context for anyone building agentic systems with [[wiki/sources/claude-code-paperclip-destroyed-openclaw]] or [[wiki/sources/how-to-build-claude-agent-teams]]. The advisor pattern is a novel architectural concept sitting between single-model and multi-model orchestration, connecting to the harness engineering concepts in [[wiki/sources/100-hours-claude-code-vs-antigravity]]. The plan mode concept maps directly to the planning mode discussion in [[wiki/sources/building-claude-code-boris-cherny]]. The cost optimization framing connects to the broader economic disruption analysis in [[wiki/sources/polymarket-bot-438k-ai-arbitrage]].
