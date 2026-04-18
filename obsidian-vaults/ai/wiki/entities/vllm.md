---
title: "vLLM"
type: entity
domain: ai
tags:
  - product
  - inference-server
  - open-source
  - python
  - nvidia
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]]"
---

# vLLM

vLLM is an open-source, high-throughput LLM inference serving library written in Python, optimized for NVIDIA GPU hardware. It implements PagedAttention (a novel memory management algorithm for KV cache) and continuous batching, making it the leading production-grade inference server for large model deployments on GPU infrastructure.

## Background / History

vLLM was created by researchers at UC Berkeley (Woosuk Kwon, Zhuohan Li, et al.) and published in a 2023 paper introducing PagedAttention. The key insight in PagedAttention is borrowed from operating system memory management: rather than allocating contiguous blocks of GPU memory for each request's KV cache (which wastes memory due to fragmentation and over-allocation), vLLM manages the KV cache in pages that can be allocated non-contiguously, dramatically improving GPU memory utilization and enabling many more concurrent requests on the same hardware.

vLLM has since grown into a comprehensive inference library with support for tensor parallelism, speculative decoding, quantization, and a wide range of model architectures. It is maintained by the vLLM community and has become the de facto standard for high-throughput LLM serving on NVIDIA hardware.

## Key Contributions / Features

**PagedAttention**: The core algorithmic innovation — managing KV cache memory in non-contiguous pages — that enables 2–5x better throughput than naive memory allocation schemes. This is particularly important for long-context requests (like those involving [[wiki/entities/gemma-4]]'s 128K context) where KV cache memory dominates GPU utilization.

**Continuous Batching**: vLLM implements continuous batching (also called iteration-level scheduling), where new requests can be added to a batch at any decoding step rather than waiting for the entire current batch to complete. This improves GPU utilization by reducing idle time between requests.

**Gemma 4 on Blackwell**: vLLM was benchmarked serving Gemma 4 on NVIDIA Blackwell GPUs (RTX 5000 series), providing throughput benchmarks for production-scale Gemma 4 deployment. The results established vLLM as the recommended serving path for maximum Gemma 4 throughput on NVIDIA hardware. (Source: [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]])

**vs. Ollama**: vLLM and [[wiki/entities/ollama]] serve different use cases: Ollama is optimized for ease of use on consumer hardware (one command to run any model), while vLLM is optimized for throughput on dedicated GPU servers. For practitioners running Gemma 4 on consumer Macs, Ollama is appropriate; for serving many concurrent users from a GPU server, vLLM provides dramatically better utilization.

## Role in AI Landscape

vLLM is the production inference infrastructure layer that enables organizations to serve large models efficiently at scale. As open models like Gemma 4 reach frontier quality, the deployment toolchain matters: vLLM ensures that running a 27B MoE model at production throughput is practical without wasteful GPU utilization. It is particularly relevant for practitioners who have NVIDIA GPU infrastructure and want to move beyond Ollama's single-user optimization to serve multiple concurrent agents or users.

## Connections

- **Related entities**: [[wiki/entities/gemma-4]], [[wiki/entities/ollama]], [[wiki/entities/google-deepmind]], [[wiki/entities/exo]]
- **Key concepts**: [[wiki/concepts/inference-optimization]], [[wiki/concepts/local-ai]], [[wiki/concepts/production-ml]]
- **Sources**: [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]]
