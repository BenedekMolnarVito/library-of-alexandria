---
title: "Gemma 4 on vLLM vs Ollama: Benchmarks on a 96 GB Blackwell GPU"
type: source
domain: ai
tags:
  - inference-engines
  - gemma-4
  - mixture-of-experts
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Gemma 4 on vLLM vs Ollama Benchmarks on a 96 GB Blackwell GPU.md]]"
---

# Gemma 4 on vLLM vs Ollama: Benchmarks on a 96 GB Blackwell GPU

**Authors**: Allen Kuo (kwyshell)
**Date**: 2026-04
**Type**: article

## Summary

Allen Kuo benchmarks all three Gemma 4 models (E4B/8B, 26B MoE, 31B Dense) on both vLLM and Ollama using an NVIDIA RTX PRO 6000 Blackwell GPU. Key findings: vLLM wins TTFT (3x faster) and concurrent throughput (3.6x higher) due to PagedAttention and Continuous Batching; Ollama wins single-user decode speed (1.5x) via Q4_K_M quantization vs vLLM's BF16. The surprise result is that the 26B MoE model runs faster than the 8B E4B on vLLM because it only activates ~4B parameters per token, delivering 26B-class intelligence at near-4B speed.

## Key Takeaways

- vLLM wins TTFT: 58ms vs 184ms (E4B), a 3.2x advantage — critical for agent loops and RAG pipelines.
- vLLM wins concurrent throughput: 441 tok/s vs 124 tok/s (E4B, 4 parallel requests), 3.6x higher.
- Ollama wins single-user decode: 196 tok/s vs 124 tok/s (E4B), 1.6x faster — due to Q4_K_M quantization cutting weight size.
- Ollama wins VRAM efficiency: 29 GiB vs 89 GiB for E4B — critical for desktop coexistence with other GPU apps.
- Gemma 4 26B MoE is the sweet spot: 131 tok/s on vLLM, only 5% slower than E4B despite 3x more total parameters.
- MoE architecture: 26B total params but only ~4B activated per token — near-4B speed with 26B-class quality.
- Avoid Gemma 4 31B on vLLM BF16: 22 tok/s is painfully slow; Ollama gives 58 tok/s with Q4_K_M.
- Most of the speed gap between vLLM and Ollama is precision (BF16 vs Q4_K_M), not engine architecture.

## Entities Mentioned

- [[wiki/entities/allen-kuo]]
- [[wiki/entities/google]]
- [[wiki/entities/gemma-4-e4b]]
- [[wiki/entities/gemma-4-26b-moe]]
- [[wiki/entities/gemma-4-31b-dense]]
- [[wiki/entities/nvidia-rtx-pro-6000-blackwell]]
- [[wiki/entities/vllm]]
- [[wiki/entities/ollama]]

## Concepts Covered

- [[wiki/concepts/inference-engines]]
- [[wiki/concepts/vllm]]
- [[wiki/concepts/ollama]]
- [[wiki/concepts/ttft-time-to-first-token]]
- [[wiki/concepts/concurrent-throughput]]
- [[wiki/concepts/quantization-bf16-vs-q4km]]
- [[wiki/concepts/mixture-of-experts]]
- [[wiki/concepts/paged-attention]]
- [[wiki/concepts/continuous-batching]]
- [[wiki/concepts/local-llm-inference]]
- [[wiki/concepts/blackwell-gpu]]

## Notable Quotes

> "26B MoE gives you 26B-class intelligence at near-4B speed."

> "Most of the decode speed gap between vLLM and Ollama comes from precision, not from engine architecture."

> "TTFT and concurrency are vLLM's structural advantages — these come from PagedAttention and Continuous Batching, architectural features that cannot be replicated by changing quantization."

## Cross-Connections

Directly related to [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]] (same model family, different focus). The MoE architecture efficiency finding is relevant to understanding [[wiki/entities/glm-5-1]] and other large models that activate only a subset of parameters — see [[wiki/sources/glm-5-1-beats-gpt-5-4-claude-opus]]. The agent loop TTFT discussion ties to orchestration latency concerns in [[wiki/sources/from-ides-to-ai-agents-steve-yegge]] and [[wiki/sources/how-to-build-claude-agent-teams]]. The Gemma 4 models also appear in [[wiki/sources/best-llms-opencode-qwen-gemma-tested-locally]] for agentic coding evaluation.
