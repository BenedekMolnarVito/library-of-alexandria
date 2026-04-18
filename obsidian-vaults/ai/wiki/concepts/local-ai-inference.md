---
title: "Local AI Inference"
type: concept
domain: ai
tags:
  - local-models
  - inference
  - apple-silicon
  - privacy
  - ollama
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/gemma-4-local-model-codex-cli]]"
  - "[[wiki/sources/two-macs-80b-ai-cluster-exo]]"
  - "[[wiki/sources/ollama-claude-code-free]]"
  - "[[wiki/sources/openclaw-gemma4-free-private-ai]]"
---

# Local AI Inference

Local AI inference is running large language model inference on personal or on-premises hardware rather than calling cloud APIs. It enables privacy (no data leaves your hardware), offline capability, zero marginal cost per token, and the freedom to experiment with model configurations that cloud providers don't offer. Apple Silicon has emerged as particularly well-suited for local inference thanks to its unified memory architecture, and tools like Ollama, llama.cpp, and vLLM have made local inference accessible without specialized expertise.

## Definition

Local inference means the model weights reside on hardware you control — a laptop, workstation, or small cluster — and inference requests never leave your network. This is categorically different from cloud inference (API calls to OpenAI, Anthropic, Google) in terms of privacy, cost structure, latency profile, and operational model.

The practical barriers to local inference have fallen dramatically from 2023 to 2026: model quality has risen substantially, quantization techniques (4-bit, 8-bit) reduce memory requirements without severe quality loss, and hardware has improved (Apple Silicon M3/M4 chips offer up to 192GB unified memory with high bandwidth). A workload that required a $10,000 GPU in 2022 can run on a $4,000 MacBook Pro in 2025.

## How It Works

**Apple Silicon advantage**: the unified memory architecture (CPU and GPU share the same DRAM pool) enables large model inference without the VRAM bottleneck that limits GPU-based inference. A discrete GPU with 24GB VRAM can only run models that fit in 24GB. An M4 Max with 128GB unified memory can run models up to roughly 90GB in size (leaving room for OS and applications). Memory bandwidth (up to 546GB/s on M4 Max) matters more than raw compute for inference; Apple Silicon's bandwidth-per-watt ratio is excellent for this workload.

**Key local inference tools**:
- **Ollama**: the simplest entry point — model management, serving, and a simple API. Handles model downloads, quantization variants, and an OpenAI-compatible API endpoint. Best for quick local model access.
- **llama.cpp**: the performance reference implementation, supporting CPU and Metal (Apple GPU) inference. Maximum control and configuration options; used by Ollama as its inference backend.
- **vLLM**: GPU-optimized inference server with PagedAttention for efficient KV cache management. Better for multi-user or high-throughput local serving on NVIDIA hardware.
- **Exo**: distributed inference across multiple local devices — see [[distributed-inference]].
- **LM Studio**: GUI-based local model management for users who prefer graphical interfaces.

**Benchmark priorities**: for local models used in [[agentic-coding]] and [[karpathy-loop]] workflows, first-pass reliability (does the generated code compile and pass tests without manual repair?) matters more than token generation speed. A model that produces correct code at 15 tokens/second is more valuable than one that produces incorrect code at 50 tokens/second. Gemma 4 27B, for example, was evaluated primarily on first-pass reliability for coding tasks.

## Why It Matters

The privacy argument is often the most compelling in practice. For organizations with sensitive data (healthcare, legal, financial), sending data to cloud APIs raises regulatory and security concerns that may be prohibitive. Local inference eliminates this concern entirely — data never leaves the network perimeter.

The cost argument matters at scale. At 10 million tokens per day (a realistic agentic workload), frontier API costs run to thousands of dollars monthly. Local inference has a fixed hardware cost (amortized over the hardware lifetime) and zero marginal cost per token. The break-even calculation favors local inference for sustained high-volume workloads.

The [[intelligence-arbitrage]] calculation is the practical synthesis: route high-complexity tasks requiring frontier reasoning to cloud APIs; route everything else to local models. Local inference is the low-cost tier that makes the arbitrage practical.

## In Practice

The Claude Code + Ollama integration exemplifies the practical value: developers can run Gemma 4 27B locally as an Ollama backend for Claude Code, getting coding assistance at zero marginal cost for development and testing workflows. The quality is competitive with 2023-era frontier models for many tasks; for tasks requiring the latest frontier quality, the API is still available.

OpenClaw (Cline with local model support) and similar open-source Claude Code alternatives enable fully local agentic coding workflows — no cloud API required. This enables experimentation without cost constraints, which is particularly valuable for [[karpathy-loop]] optimization runs that may require hundreds of iterations.

## Related Concepts

- [[wiki/concepts/distributed-inference]] — extending local inference across multiple devices
- [[wiki/concepts/mixture-of-experts]] — architecture enabling large local models efficiently
- [[wiki/concepts/intelligence-arbitrage]] — routing between local and cloud models
- [[wiki/concepts/local-hard-takeoff]] — the quality convergence trend
- [[wiki/concepts/agentic-coding]] — the primary use case for local inference in development

## Key Entities

- [[wiki/entities/apple]] — Apple Silicon hardware for local inference
- [[wiki/entities/google-deepmind]] — Gemma 4 as a top local model

## Sources

- [[wiki/sources/gemma-4-local-model-codex-cli]]
- [[wiki/sources/two-macs-80b-ai-cluster-exo]]
- [[wiki/sources/ollama-claude-code-free]]
- [[wiki/sources/openclaw-gemma4-free-private-ai]]
