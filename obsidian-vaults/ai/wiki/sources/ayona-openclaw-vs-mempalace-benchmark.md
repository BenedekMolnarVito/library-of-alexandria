---
title: "Ayona (OpenClaw) vs MemPalace Benchmark Comparison"
type: source
domain: ai
tags:
  - mempalace
  - bm25
  - retrieval
  - benchmarking
created: 2026-04-20
updated: 2026-04-20
raw: "[[raw/Ayona (OpenClaw) vs Milla (MemPalace) I Challenged a Specialized Memory Library With a 30-Year-Old….md]]"
---

# Ayona (OpenClaw) vs MemPalace Benchmark Comparison

**Authors**: Serhii Zabolotnii  
**Date**: 2026-04  
**Type**: article

## Summary

This source benchmarks Ayona retrieval against MemPalace on LongMemEval under shared conditions. The key claim is that strong BM25-first pipelines can match or beat vector-heavy setups in some conversational-memory workloads, especially when latency is constrained.

## Key Takeaways

- BM25 baseline reportedly reached 96.8% R@5, close to MemPalace raw-mode results on the same benchmark.
- Embeddings improved some categories (preferences, multi-session) but hurt others (temporal, single-session-user), so global hybridization was not always net-positive.
- Temporal parsing and keyword boosting produced meaningful gains with low latency overhead.
- Retrieval architecture should be query-type-aware, not one-size-fits-all.

## Entities Mentioned

- [[wiki/entities/openclaw]]
- [[wiki/entities/mempalace]]
- [[wiki/entities/milla-jovovich]]

## Concepts Covered

- [[wiki/concepts/agent-memory]]
- [[wiki/concepts/memory-palace-architecture]]
- [[wiki/concepts/vectorless-rag]]
- [[wiki/concepts/eval-driven-development]]

## Notable Quotes

> "The best retrieval system is the one you’ve actually measured."

## Personal Notes

Useful counterweight to sweeping "vector > lexical" assumptions; reinforces benchmark-driven architecture decisions.
