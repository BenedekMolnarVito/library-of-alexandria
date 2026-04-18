---
title: "llama.cpp"
type: entity
domain: ai
tags:
  - product
  - inference-engine
  - open-source
  - cpp
  - cpu
  - apple-silicon
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/gemma-4-local-model-codex-cli]]"
---

# llama.cpp

llama.cpp is an open-source C++ inference engine for large language models, enabling efficient model execution on CPU and Apple Silicon hardware without requiring NVIDIA GPUs. It is the foundational layer that makes local LLM inference practical on the widest range of consumer hardware, including Macs, Windows PCs, and even mobile devices.

## Background / History

llama.cpp was created by Georgi Gerganov in early 2023, initially as a port of Meta's LLaMA model to pure C/C++. The original release demonstrated that a 7B parameter model could run on a MacBook with reasonable performance purely on CPU — a result that surprised many in the AI community who assumed GPU was mandatory for LLM inference. The project grew explosively as the community recognized its implications: LLM inference was possible on hardware that hundreds of millions of people already owned.

The project has since expanded to support virtually every open model architecture (LLaMA, Mistral, Gemma, Qwen, GLM, and many others), added quantization support (reducing model size and memory requirements by representing weights in lower precision), and integrated Apple's Metal GPU acceleration for significantly faster inference on Apple Silicon. It underpins many higher-level tools including [[wiki/entities/ollama]], which uses llama.cpp as its inference backend for CPU and Apple Silicon deployments.

## Key Contributions / Features

**CPU-First Inference**: The core contribution of llama.cpp is demonstrating and enabling efficient LLM inference on CPU hardware. Through aggressive quantization (4-bit, 5-bit, 8-bit weight precision) and architecture-specific optimizations (SIMD instructions, memory access patterns), llama.cpp achieves CPU inference speeds that are practical for real use — typically 10–30 tok/s on a modern laptop CPU for a 7B model, faster with quantization.

**Apple Silicon Metal Acceleration**: On Apple Silicon (M1/M2/M3/M4), llama.cpp uses Metal (Apple's GPU framework) to accelerate inference, achieving speeds comparable to dedicated GPU inference on larger models. This makes Macs with unified memory (which can hold large models that a discrete GPU cannot) the best consumer hardware for local inference.

**Quantization**: llama.cpp pioneered GGUF quantization (previously GGML) — a family of quantization schemes that reduce model size and memory requirements by 2–8x while retaining most of the model's capability. A 70B model quantized to 4-bit fits in about 40GB of RAM, making it runnable on a Mac Studio with 48GB or 64GB unified memory.

**Gemma 4 Support**: [[wiki/entities/daniel-vaughan]] used llama.cpp as the inference engine for [[wiki/entities/gemma-4]] in his Codex CLI benchmark — demonstrating that llama.cpp's Gemma 4 support enables the full local agentic coding stack on consumer hardware. (Source: [[wiki/sources/gemma-4-local-model-codex-cli]])

## Role in AI Landscape

llama.cpp is the bedrock of the local AI movement. Without it, local model inference would require NVIDIA GPUs — dramatically increasing the cost and limiting the hardware on which local AI is practical. By enabling CPU and Apple Silicon inference, llama.cpp made the hundreds of millions of existing consumer devices into capable AI inference hardware. Ollama's ease of use is built on llama.cpp's performance; the entire local AI ecosystem depends on the C++ inference efficiency that Georgi Gerganov's project provides.

## Connections

- **Related entities**: [[wiki/entities/ollama]], [[wiki/entities/gemma-4]], [[wiki/entities/codex-cli]], [[wiki/entities/daniel-vaughan]], [[wiki/entities/exo]]
- **Key concepts**: [[wiki/concepts/local-ai]], [[wiki/concepts/quantization]], [[wiki/concepts/inference-optimization]]
- **Sources**: [[wiki/sources/gemma-4-local-model-codex-cli]]
