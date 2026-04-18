---
title: "Ollama + Claude Code = 99% CHEAPER"
type: source
domain: ai
tags:
  - ollama
  - claude-code
  - open-source-models
  - cost-optimization
  - local-inference
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Ollama + Claude Code = 99% CHEAPER.md]]"
---

# Ollama + Claude Code = 99% CHEAPER

**Authors**: Nate Herk | AI Automation
**Date**: 2026-04
**Type**: video-transcript

## Summary

A step-by-step tutorial showing two methods for running Claude Code with free LLM backends: local open-source models via Ollama (demonstrated with Qwen 3.5 9B), and free cloud models via OpenRouter. The core insight is that Claude Code is the harness (the car) and the LLM is the engine — they are separable, and swapping the engine does not require touching the harness or violate Anthropic's terms of service.

Open-source models have caught up significantly on coding benchmarks: several open-weight models now outperform Claude Sonnet 3.7 on SWE-bench verified. However, they can still misbehave in Claude Code because they were not trained on its tool protocol, may have small context windows, or may not follow its JSON schema — experimentation per model is required. At recording time, Google Gemma 4 models showed the best Elo-to-size ratio on the benchmarks surveyed.

## Key Takeaways

- Claude Code = agent harness (car); LLM = engine — they are separable at a configuration level
- Method 1: Install Ollama, pull a model (`ollama pull qwen3.5`), point Claude Code to the local endpoint — completely free
- Method 2: Use OpenRouter free-tier models as the Claude Code backend — also free
- Google Gemma 4 models showed the best Elo-to-size ratio at time of recording
- Open-source models may misbehave due to not being trained on Claude Code's tool protocol, small context windows, or non-standard JSON schema
- SWE-bench verified shows several open-weight models now outperform Claude Sonnet 3.7
- Swapping the engine is not against Anthropic's terms of service
- Ask Claude Code itself which model size your hardware can handle based on your specs

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/ollama]]
- [[wiki/entities/openrouter]]
- [[wiki/entities/qwen-3-5]]
- [[wiki/entities/gemma-4]]
- [[wiki/entities/google]]
- [[wiki/entities/claude-opus-4-6]]
- [[wiki/entities/claude-sonnet-3-7]]

## Concepts Covered

- [[wiki/concepts/open-source-vs-closed-source-models]]
- [[wiki/concepts/local-llm-inference]]
- [[wiki/concepts/model-swapping]]
- [[wiki/concepts/swe-bench-benchmarks]]
- [[wiki/concepts/cost-optimization]]
- [[wiki/concepts/agent-harness-architecture]]
- [[wiki/concepts/ollama-setup]]
- [[wiki/concepts/openrouter]]

## Notable Quotes

> "Claude Code is the car and the chat model is the engine."

> "Some of the open-weight models that we can access today are better than Claude Sonnet 3.7 — and when that model dropped, everyone was freaking out."

## Cross-Connections

Directly complements [[wiki/sources/master-claude-code-skills]] by the same author — both are Nate Herk tutorials covering different dimensions of Claude Code usage (capability vs. cost). The open-source vs. closed-source framing connects to [[wiki/sources/chandra-ocr-2-benchmark]], where a small specialized model beats frontier models — the same theme of capable small models in specific domains. The Gemma 4 recommendation links to [[wiki/sources/gemma-4-open-source-ai-drop]] where the same model is profiled in detail.
