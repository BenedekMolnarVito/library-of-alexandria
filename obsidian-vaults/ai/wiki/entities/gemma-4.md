---
title: "Gemma 4"
type: entity
domain: ai
tags:
  - model
  - google-deepmind
  - open-weight
  - moe
  - multimodal
  - tool-calling
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]]"
  - "[[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]]"
  - "[[wiki/sources/gemma-4-open-source-ai-drop]]"
  - "[[wiki/sources/gemma-4-local-model-codex-cli]]"
  - "[[wiki/sources/openclaw-gemma4-free-private-ai]]"
---

# Gemma 4

Gemma 4 is the fourth generation of [[wiki/entities/google-deepmind]]'s Gemma open model family, released in April 2026. It represents a dramatic leap in open-weight model capability for agentic tasks — particularly tool-calling — and has materially changed the calculus for practitioners considering local AI versus cloud API deployments.

## Background / History

The Gemma series was Google DeepMind's entry into the open-weight model space, beginning with Gemma 1 in early 2024. Earlier versions were respectable but not competitive with frontier proprietary models on the tool-calling and instruction-following tasks that matter most for agentic coding. Gemma 4 changes this with a complete architectural revamp, most notably the adoption of Mixture of Experts (MoE) for the flagship variant and massive improvements in tool-calling benchmark scores. The release coincided with the broader open model ecosystem reaching a point where local inference is becoming practically viable for the tasks previously requiring cloud APIs.

## Key Contributions / Features

**Model Variants**:
- **Gemma 4 4B (E4B)**: A 4-billion parameter embedded variant optimized for on-device and edge deployment — designed to run in constrained environments like mobile and embedded systems.
- **Gemma 4 12B (Dense)**: A 12-billion parameter dense model providing a balance between the efficiency of E4B and the capability of the flagship.
- **Gemma 4 27B (MoE)**: The flagship variant, using a Mixture of Experts architecture with approximately 27B total parameters but only ~3.8B activated parameters per token. This makes the 27B MoE roughly 5x faster than an equivalent dense 27B model at the same memory bandwidth — a significant inference efficiency gain.

All variants are multimodal, accepting both image and text inputs.

**Tool-Calling Benchmark Leap**: The single most important data point about Gemma 4 is its tool-calling performance improvement: Gemma 3 scored **6.6%** on the tau2-bench tool-calling benchmark; Gemma 4 scored **86.4%** — a 13x improvement that transforms the model from impractical to highly capable for agentic tasks requiring tool use. This jump makes local agentic coding with open models practically viable for the first time. (Source: [[wiki/sources/gemma-4-open-source-ai-drop]])

**MoE Efficiency**: The 27B MoE design demonstrates why MoE architectures are increasingly preferred for large open models: the activated parameter count (~3.8B per token) means the model runs at inference speeds comparable to a much smaller dense model while retaining the knowledge and capability of a larger one. For practitioners running Gemma 4 on consumer hardware, this translates to acceptable inference speed on machines that would struggle with a dense 27B model.

**Inference Options**: Gemma 4 can be served via [[wiki/entities/vllm]] on NVIDIA hardware for maximum throughput, or via [[wiki/entities/ollama]] and [[wiki/entities/llama-cpp]] for local CPU/Apple Silicon deployment. [[wiki/entities/daniel-vaughan]] benchmarked the 27B variant with llama.cpp for Codex CLI agentic coding. (Sources: [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]], [[wiki/sources/gemma-4-local-model-codex-cli]])

**Vs. Qwen3.5 4B**: In the small-model category, Gemma 4 E4B was benchmarked against [[wiki/entities/qwen3]] Qwen3.5 4B across multiple tasks, with results varying by task type. (Source: [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]])

## Role in AI Landscape

Gemma 4's significance extends beyond benchmark numbers. The jump from 6.6% to 86.4% on tool-calling represents a phase transition — not just quantitative improvement but a qualitative change in what local open models can reliably do. Agentic coding requires a model to call tools (read file, execute code, write file, search web) reliably and in the correct sequence; at 6.6%, Gemma 3 was not competitive with cloud models for this use case. At 86.4%, Gemma 4 is. This makes Gemma 4 the first open model to credibly challenge Claude Sonnet as the default choice for agentic coding practitioners who prioritize privacy, cost, or offline operation.

## Connections

- **Related entities**: [[wiki/entities/google-deepmind]], [[wiki/entities/vllm]], [[wiki/entities/ollama]], [[wiki/entities/llama-cpp]], [[wiki/entities/openclaw]], [[wiki/entities/codex-cli]], [[wiki/entities/qwen3]], [[wiki/entities/daniel-vaughan]], [[wiki/entities/networkchuck]]
- **Key concepts**: [[wiki/concepts/mixture-of-experts]], [[wiki/concepts/tool-calling]], [[wiki/concepts/local-ai]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/multimodal-models]]
- **Sources**: [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]], [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]], [[wiki/sources/gemma-4-open-source-ai-drop]], [[wiki/sources/gemma-4-local-model-codex-cli]], [[wiki/sources/openclaw-gemma4-free-private-ai]]
