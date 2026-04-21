---
title: "This 196B Open-Source Model Beats Claude Opus 4.5, Kimi K2.5, and GLM 4.7. Nobody Is Talking About It."
type: source
domain: ai
tags:
  - mixture-of-experts
  - open-source-models
  - sparse-activation
  - benchmarks
  - stepfun
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/This 196B Open-Source Model Beats Claude Opus 4.5,.md]]"
---

# This 196B Open-Source Model Beats Claude Opus 4.5, Kimi K2.5, and GLM 4.7. Nobody Is Talking About It.

**Authors**: Ari Vance
**Date**: 2026-03
**Type**: article

## Summary

StepFun (Shanghai) quietly published Step-3.5-Flash in February 2026: a 196B total-parameter Sparse Mixture-of-Experts model that activates only 11B parameters per token, achieving 1.0x inference cost relative to a dense 11B model while outscoring Claude Opus 4.5 on agentic benchmarks. It leads open-source on AIME 2025 (97.3), LiveCodeBench-V6 (86.4), τ²-Bench (88.2), and GAIA (84.5), and beats both Gemini DeepResearch and OpenAI DeepResearch on ResearchRubrics (65.3).

The article's secondary thesis is as important as its primary one: the near-zero English-language coverage of Step-3.5-Flash is explained by StepFun's Chinese-first PR strategy — not by model quality. Moonshot AI (Kimi K2.5) deliberately seeded English communities; StepFun published a technical report and let results speak. This exposes a systemic bias in AI coverage: if discovery starts with what gets written about in English, evaluation selects against efficiency. The author introduces "intelligence density" — reasoning quality per activated parameter — as the correct metric for 2026.

## Key Takeaways

- 196B total params, only 11B activated per token (Sparse MoE) — inference cost is 1.0x vs Kimi K2.5's 18.9x at equivalent context
- Hybrid attention: 3:1 ratio of SWA (linear cost) to Full Attention (quadratic) enables 256K context window without cost explosion
- MTP-3 (3-way Multi-Token Prediction) generates 100–350 tokens/second, parallelizing decoding to break the serial bottleneck
- Leads open-source on AIME 2025 (97.3), LiveCodeBench-V6 (86.4), τ²-Bench (88.2), GAIA (84.5), ResearchRubrics (65.3)
- Beats both Gemini DeepResearch and OpenAI DeepResearch on ResearchRubrics — a 196B open-source model defeating purpose-built proprietary research systems
- Known weaknesses: multi-turn conversational instability, mixed-language output risk, requires 128GB+ unified memory for local deployment
- Coverage gap explained: Moonshot AI seeded English communities deliberately; StepFun published a technical report and let results speak
- "Intelligence density" — reasoning quality per activated parameter — introduced as the right metric for 2026

## Entities Mentioned

- [[wiki/entities/stepfun]]
- [[wiki/entities/step-3-5-flash]]
- [[wiki/entities/ari-vance]]
- [[wiki/entities/claude-opus-4-5]]
- [[wiki/entities/kimi-k2-5]]
- [[wiki/entities/deepseek-v3-2]]
- [[wiki/entities/glm-4-7]]
- [[wiki/entities/minimax]]
- [[wiki/entities/moonshot-ai]]
- [[wiki/entities/anthropic]]

## Concepts Covered

- [[wiki/concepts/mixture-of-experts]]
- [[wiki/concepts/sparse-activation]]
- [[wiki/concepts/intelligence-density]]
- [[wiki/concepts/inference-cost]]
- [[wiki/concepts/hybrid-attention]]
- [[wiki/concepts/sliding-window-attention]]
- [[wiki/concepts/multi-token-prediction]]
- [[wiki/concepts/agentic-benchmarks]]
- [[wiki/concepts/open-source-ai-bias]]

## Notable Quotes

> "Total parameters and active parameters are not the same thing."

> "If your evaluation process starts with what gets written about, you're selecting against efficiency."

> "Step-3.5-Flash is a specialist, not a generalist."

## Cross-Connections

Architecture (Sparse MoE, 11B active params) is the same efficiency class discussed in [[wiki/sources/gemma-4-open-source-ai-drop]] — both demonstrate that raw parameter count is a misleading metric. The coverage bias analysis applies to how AI practitioners discover and evaluate all models surveyed in this corpus. The local deployment requirement (128GB hardware) connects to the Gemma 4 edge deployment story and offline agent use cases from [[wiki/sources/ollama-claude-code-free]]. The 6x inference cost advantage over Kimi K2.5 is directly relevant to the cost pressure concerns in [[wiki/sources/uber-agentic-engineering-shift]] (6x cost increase since 2024).
