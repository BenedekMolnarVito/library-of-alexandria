---
title: "TurboQuant MoE on Apple Silicon: Running 122B Models Locally"
type: source
domain: ai
tags:
  - local-ai
  - quantization
  - mixture-of-experts
  - apple-silicon
created: 2026-04-20
updated: 2026-04-20
raw: "[[raw/How I run 122B-parameter LLMs on a MacBook — outperforming MXFP4 and standard quantization on Apple….md]]"
---

# TurboQuant MoE on Apple Silicon: Running 122B Models Locally

**Authors**: Manjunath Janardhan  
**Date**: 2026-04  
**Type**: article

## Summary

This source reports extending TurboQuant to MoE models on Apple Silicon, including GPT-OSS and Qwen3.5 122B-class models. The key contribution is practical compression + kernel optimization that makes very large local MoE inference feasible on 64GB M4 Max hardware.

## Key Takeaways

- TurboQuant 3-bit reportedly enables 120B+ MoE models to fit and run on 64GB Apple Silicon machines.
- The article reports quality/size gains versus MXFP4 and strong throughput after fused-kernel fixes.
- A one-line kernel indexing correction produced a dramatic speed improvement in the reported benchmark.
- The work strengthens the case that local high-parameter inference is increasingly practical with architecture-aware quantization.

## Entities Mentioned

- [[wiki/entities/manjunath-janardhan]]
- [[wiki/entities/qwen3]]

## Concepts Covered

- [[wiki/concepts/local-ai-inference]]
- [[wiki/concepts/mixture-of-experts]]
- [[wiki/concepts/intelligence-arbitrage]]

## Notable Quotes

> "No existing quantization format fits on 64GB RAM. TurboQuant 3-bit is the only way to run this 120B LLM on consumer Apple Silicon hardware."

## Personal Notes

Important datapoint for the local-first trajectory: model-serving feasibility is now strongly linked to quantization quality, not just raw model size.

