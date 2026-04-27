---
title: "I Tested the 1-Bit LLM That Fits in 1 GB — It Shouldn't Be This Good"
type: source
domain: ai
tags:
  - 1-bit-quantization
  - model-compression
  - benchmarks
  - local-inference
  - efficiency
created: 2026-04-27
updated: 2026-04-27
raw: "[[raw/I Tested the 1-Bit LLM That Fits in 1 GB — It Shouldn't Be This Good.md]]"
---

# I Tested the 1-Bit LLM That Fits in 1 GB — It Shouldn't Be This Good

**Author**: Chew Loong Nian (AI Engineer)
**Published**: 2026-04-07
**Type**: Benchmark / technical review

## Summary

A Caltech startup compressed 8.2B parameters into 1.15 GB using extreme 1-bit quantization. The author benchmarks it against Llama 3.1, Qwen 3, and Gemma 4. Surprisingly strong performance on coding and reasoning tasks despite radical compression. Implications for edge deployment and offline accessibility.

## Key Takeaways

- **Extreme compression works** — 1-bit quantization yields usable model at 1.15 GB
- **Performance trade-off minimal** — Comparable to 4-bit quantization on many tasks; marginally slower
- **Coding performance strong** — Tool-use and reasoning hold up better than expected
- **Edge deployment viable** — Model fits on mobile phones, IoT devices with practical performance
- **Trade-off discovery** — Speed vs. size; quality vs. compression; all four were measured

## Entities Mentioned

- [[wiki/entities/llama-cpp]]
- [[wiki/entities/qwen3]]
- [[wiki/entities/gemma-4]]

## Concepts Covered

- [[wiki/concepts/quantization]]
- [[wiki/concepts/model-compression]]
- [[wiki/concepts/extreme-edge-deployment]]
- [[wiki/concepts/inference-speed]]

## Personal Notes

Practical validation that extreme quantization doesn't necessarily mean severe capability loss. Opens door to offline-first, privacy-preserving inference. Relevant for embedded systems and resource-constrained environments.
