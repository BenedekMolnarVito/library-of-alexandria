---
title: "Qwen3"
type: entity
domain: ai
tags:
  - model
  - alibaba
  - open-weight
  - local-ai
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/two-macs-80b-ai-cluster-exo]]"
  - "[[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]]"
---

# Qwen3

Qwen3 is Alibaba Cloud's third-generation open-weight model family, notable in this corpus for two specific appearances: Qwen3-Next-80B was used by [[wiki/entities/manjunath-janardhan]] to demonstrate [[wiki/entities/exo]]'s distributed inference capability at 70–80 tokens per second across two Macs, and Qwen3.5-4B was benchmarked head-to-head against [[wiki/entities/gemma-4]] E4B in the small-model tier.

## Background / History

The Qwen (通义千问) series is Alibaba Cloud's flagship open-weight model family, developed by the Tongyi Lab. Alibaba has consistently released models across the full parameter range — from efficient small models (0.5B–7B) suitable for on-device deployment, through mid-range models (14B–72B), to large models (110B+) for high-capability tasks. The series has been notable for its strong performance on multilingual tasks, its competitive coding capability, and the breadth of its open-weight releases compared to Western counterparts.

Qwen3 represents the third major architectural iteration, with improvements in instruction following, tool calling, and reasoning. The family includes both dense and MoE variants.

## Key Contributions / Features

**Qwen3-Next-80B (Exo Benchmark)**: The 80B parameter variant of Qwen3-Next was the model used to demonstrate Exo's distributed inference capability on consumer hardware. Running across two Mac machines, it achieved 70–80 tokens per second — a throughput that makes the 80B model practical for interactive tasks. This demonstration established Qwen3-Next-80B as a reference model for the "what can you run on a two-Mac cluster?" question. (Source: [[wiki/sources/two-macs-80b-ai-cluster-exo]])

**Qwen3.5-4B (Small Model Competition)**: The compact 4B parameter variant was benchmarked against Gemma 4 E4B across multiple task categories. At the 4B tier, both models are competing for the same use case: capable inference on edge devices, mobile, and embedded systems. The comparison results vary by task type, reflecting the different optimization choices made by Alibaba and Google DeepMind at this model scale. (Source: [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]])

**Multilingual Strength**: Qwen models have historically demonstrated stronger performance than Western open models on Chinese-language tasks and on multilingual benchmarks generally, reflecting Alibaba's prioritization of a global user base from day one.

## Role in AI Landscape

Qwen3 represents Alibaba's ongoing commitment to open-weight model releases that are competitive with Western frontier open models. The 80B variant is particularly interesting as it sits in the "large enough to be highly capable, small enough to be locally deployable" size class that practitioners optimizing for local inference increasingly target. Its appearance in the Exo benchmark demonstrates that distributed consumer inference for 80B models is practically achievable, not just theoretically possible.

## Connections

- **Related entities**: [[wiki/entities/exo-labs]], [[wiki/entities/exo]], [[wiki/entities/gemma-4]], [[wiki/entities/ollama]], [[wiki/entities/manjunath-janardhan]]
- **Key concepts**: [[wiki/concepts/distributed-inference]], [[wiki/concepts/local-ai]], [[wiki/concepts/open-weight-models]]
- **Sources**: [[wiki/sources/two-macs-80b-ai-cluster-exo]], [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]]
