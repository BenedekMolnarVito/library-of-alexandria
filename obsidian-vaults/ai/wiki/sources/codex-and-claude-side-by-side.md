---
title: "I Ran Codex and Claude Side by Side. Here's What I Found."
type: source
domain: ai
tags:
  - codex
  - claude-code
  - multi-model
  - adversarial-review
  - ai-compliance
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/I Ran Codex and Claude Side by Side. Here’s What I Found.md]]"
---

# I Ran Codex and Claude Side by Side. Here's What I Found.

**Authors**: Yanli Liu
**Date**: 2026-04
**Type**: article

## Summary

Yanli Liu explores two levels of multi-model AI collaboration: (1) running OpenAI's official Codex plugin inside Claude Code for adversarial code review, and (2) Microsoft Copilot Cowork's enterprise-scale multi-model architecture ('Critique' and 'Model Council'). The practical finding is that Claude and Codex have different training distributions and failure modes, so their disagreements reliably surface real bugs. The structural finding is that Microsoft's 'Critique' feature hides intermediate model attribution — a compliance gap that regulated industries (especially banks) cannot currently bridge under SR 11-7 and EU AI Act Article 12.

## Key Takeaways

- OpenAI released an official Codex plugin for Claude Code on March 30, 2026 — two competing companies, one integration
- `/codex:adversarial-review` caught 3 real bugs that Claude's self-review missed (KeyError, malformed JSON handling, silent non-200 discard)
- Two architectures in Copilot Cowork: Critique (sequential — GPT drafts, Claude audits, one clean output) vs. Model Council (parallel — both models produce full reports, judge model synthesizes disagreements)
- Critique hides which model version produced which claim — an accountability gap for regulated industries
- SR 11-7 (Federal Reserve model risk guidance) and EU AI Act Article 12 both require per-model attribution that Critique cannot currently provide
- Cost estimate: ~$0.02 per /codex:rescue call at GPT-5.4 pricing (~$30/month for heavy users)
- Model Council is the more honest architecture: surfaces disagreements rather than hiding them

## Entities Mentioned

- [[wiki/entities/yanli-liu]]
- [[wiki/entities/openai]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/microsoft]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/codex]]
- [[wiki/entities/copilot-cowork]]
- [[wiki/entities/gpt-5-4]]
- [[wiki/entities/gpt-5-2]]
- [[wiki/entities/langsmith]]

## Concepts Covered

- [[wiki/concepts/multi-model-collaboration]]
- [[wiki/concepts/adversarial-review]]
- [[wiki/concepts/model-attribution]]
- [[wiki/concepts/ai-compliance]]
- [[wiki/concepts/model-council]]
- [[wiki/concepts/sr-11-7]]
- [[wiki/concepts/eu-ai-act-article-12]]
- [[wiki/concepts/agent-orchestration]]

## Notable Quotes

> "Two models. Different answers. Both useful — but one of them was actually useful."

> "The reason this works isn't magic. Claude and Codex have different training distributions, different fine-tuning histories, different failure modes. When they disagree, the disagreement is usually pointing at something real."

## Cross-Connections

The multi-model adversarial pattern described here is a practical implementation of the multi-agent collaboration patterns (CrewAI's 'critique' agent, LangGraph reviewer nodes) surveyed in [[wiki/sources/comparing-6-python-ai-agent-frameworks]]. The attribution gap problem connects directly to the 'dark code' governance issues in [[wiki/sources/amazon-fired-engineers-ai-dark-code]]. The Copilot Cowork commercial context (Microsoft Q1 2026 stock decline, 3.3% Copilot adoption) provides a market reality check on AI productivity claims. The adversarial review approach operationalizes the comprehension gate concept from the Amazon dark code article.
