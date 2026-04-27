---
title: "How I Doubled My Local LLM's Speed (Without Buying New Hardware)"
type: source
domain: ai
tags:
  - local-inference
  - optimization
  - quantization
  - performance-tuning
  - llm-speed
created: 2026-04-27
updated: 2026-04-27
raw: "[[raw/How I Doubled My Local LLM's Speed (Without Buying New Hardware).md]]"
---

# How I Doubled My Local LLM's Speed (Without Buying New Hardware)

**Author**: Amar Chetri (PhD)
**Published**: 2026-02-22
**Type**: Technical tutorial / optimization guide

## Summary

A practical guide to doubling local LLM inference speed without hardware upgrades. Covers quantization tuning, context window optimization, batch processing, vLLM settings, and memory management. Real-world case: 70B parameter model, Q4_K_M quantization, optimized for 1–2 tok/s inference on consumer hardware.

## Key Takeaways

- **Quantization sweet spots** — Q5_K_M and Q6_K balance quality and speed better than Q4_K_M
- **Context window tuning** — Large context windows slow inference; tune to actual need
- **Batch processing** — Multiple requests batched together use GPU more efficiently
- **vLLM optimization** — Specific settings for PagedAttention, continuous batching
- **Memory management** — CPU offloading (fallback) vs. GPU-only modes; tradeoffs clear
- **2x speedup realistic** — Achievable through combination of tactics, not single trick

## Entities Mentioned

- [[wiki/entities/vllm]]
- [[wiki/entities/llama-cpp]]

## Concepts Covered

- [[wiki/concepts/local-ai-inference]]
- [[wiki/concepts/quantization]]
- [[wiki/concepts/inference-optimization]]
- [[wiki/concepts/vram-management]]

## Personal Notes

Practical, actionable. De-mystifies the hardware constraints. Shows that software optimization often yields better ROI than hardware upgrades for local inference. Valuable for developers running models on constrained devices.
