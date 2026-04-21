---
title: "MemPalace Benchmarks: What They Actually Mean"
type: source
domain: ai
tags:
  - mempalace
  - benchmarking
  - evaluation
  - retrieval
created: 2026-04-20
updated: 2026-04-20
raw: "[[raw/MemPalace Milla Jovovich’s AI Memory System — What the Benchmarks Actually Mean.md]]"
---

# MemPalace Benchmarks: What They Actually Mean

**Authors**: Ewan Mak  
**Date**: 2026-04  
**Type**: article

## Summary

A critical, technically specific read of MemPalace benchmark claims and implementation details. The article distinguishes strong baseline retrieval performance from overstated marketing narratives, emphasizing methodological caveats.

## Key Takeaways

- The 96.6% LongMemEval raw-mode number is treated as meaningful, but largely reflects Chroma retrieval over raw text.
- Reported "100%" results are presented as sensitive to benchmark-specific tuning and evaluation setup.
- AAAK is characterized as lossy in current form, with measurable recall degradation versus raw mode.
- Despite critique, local-first deployment and low-friction MCP integration are highlighted as practical strengths.

## Entities Mentioned

- [[wiki/entities/mempalace]]
- [[wiki/entities/milla-jovovich]]
- [[wiki/entities/ben-sigman]]

## Concepts Covered

- [[wiki/concepts/agent-memory]]
- [[wiki/concepts/aaak-dialect]]
- [[wiki/concepts/eval-driven-development]]
- [[wiki/concepts/memory-palace-architecture]]

## Notable Quotes

> "The 96.6% raw score, in the zero-API-cost category, is genuinely the highest published result. That’s real. The marketing around it isn’t."

## Personal Notes

High-value source for separating architecture value from claim inflation.

