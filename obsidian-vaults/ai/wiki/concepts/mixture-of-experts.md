---
title: "Mixture of Experts"
type: concept
domain: ai
tags:
  - model-architecture
  - efficiency
  - neural-networks
  - local-inference
  - moe
created: 2026-04-28
updated: 2026-04-20
sources:
  - "[[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]]"
  - "[[wiki/sources/two-macs-80b-ai-cluster-exo]]"
  - "[[wiki/sources/gemma-4-local-model-codex-cli]]"
  - "[[wiki/sources/turboquant-moe-122b-macbook-apple-silicon]]"
---

# Mixture of Experts

Mixture of Experts (MoE) is a neural network architecture in which a model contains many specialized "expert" sub-networks but activates only a small subset of them for any given input token. This sparse activation is the key innovation: a MoE model with 27B total parameters might activate only 3.8B parameters per token, consuming the same memory bandwidth as a 3.8B dense model while retaining the representational capacity of the full 27B. The result is models that are dramatically more efficient at inference than their parameter count suggests — enabling local inference of frontier-quality models on consumer hardware.

## Definition

In a standard dense neural network, every parameter in every layer participates in every forward pass. A 27B-parameter dense model activates 27B parameters to process every token — expensive in terms of memory bandwidth and compute.

In a MoE model, the feed-forward layers (the "experts") are replaced by a set of N expert networks (often 8–64 experts) plus a routing network (the "gating" function). For each token, the gating network selects the top-K experts (typically K=1 or K=2) and routes the token through only those experts. The other N-K experts receive no computation for that token.

The computational cost per token scales with K×(expert size), not total parameters. The representational capacity scales with total parameters. This decoupling — more parameters at lower cost — is the architectural breakthrough.

## How It Works

The concrete numbers from Gemma 4 27B illustrate the advantage precisely:

- **Total parameters**: 27B
- **Active parameters per token**: 3.8B (14% of total)
- **Comparison**: a dense model at equivalent quality would require ~31.2B active parameters per token
- **Throughput advantage**: 5.1x faster token generation than an equivalent dense model

This means running Gemma 4 27B locally feels like running a 3.8B model in terms of speed and memory bandwidth, while producing quality comparable to a much larger dense model. On Apple Silicon with unified memory, this makes frontier-quality inference practical on consumer hardware.

The gating network learns which experts to activate through training — different experts specialize in different aspects of language processing, and the gating network learns to route tokens to the appropriate specialists. This learned specialization is why MoE models can produce high-quality outputs despite sparse activation: the right experts are activated for the right tokens.

The architecture is used by Gemma 4 (Google DeepMind), Qwen3-80B (Alibaba), Step-3.5-Flash (196B total parameters), and was pioneered at scale by Mixtral (Mistral AI). The pattern of frontier labs adopting MoE suggests it will be the dominant architecture for large local models going forward.

## Why It Matters

MoE is the technical enabler of [[local-hard-takeoff]]. Without MoE efficiency, running frontier-quality models on Apple Silicon would require far more hardware than is practical for most users. With MoE, a 27B-parameter model with 3.8B active parameters is runnable on an M4 MacBook Pro with 64GB unified memory at useful speeds.

The [[intelligence-arbitrage]] calculation changes significantly with MoE: the performance tier that previously required a cloud API call (27B+ parameter quality) is now achievable locally on consumer hardware. The cost structure shifts from "pay per token for frontier quality" to "buy the hardware once and run indefinitely." For high-volume use cases, the economics are decisive.

MoE also changes the distributed inference calculation. A 27B MoE model that activates 3.8B parameters per token is easier to distribute across multiple devices than a 27B dense model, because the per-token computation is smaller and the inter-device communication requirements are reduced.

## In Practice

From a practical deployment perspective, MoE models require careful framework support. Ollama handles MoE models transparently; vLLM has specialized MoE support for GPU inference; llama.cpp handles them efficiently on CPU. The main practical consideration is that total model weights still need to fit in memory (even if only a fraction is activated per token), so a 27B MoE model still requires roughly 27B × (bytes per parameter) of memory — though in 4-bit quantization this is approximately 14GB, manageable on most Apple Silicon hardware.

New benchmark reports in this corpus add another practical point: MoE viability on consumer hardware depends heavily on quantization method quality and low-level kernel engineering, not only on parameter count and architecture labels.

## Related Concepts

- [[wiki/concepts/local-ai-inference]] — the application context where MoE matters most
- [[wiki/concepts/local-hard-takeoff]] — MoE as the technical enabler
- [[wiki/concepts/distributed-inference]] — MoE models distribute efficiently
- [[wiki/concepts/intelligence-arbitrage]] — MoE changes the tier routing calculation
- [[wiki/concepts/local-first-ai-memory]] — infrastructure and deployment constraints around local operation

## Key Entities

- [[wiki/entities/google-deepmind]] — Gemma 4 27B MoE
- [[wiki/entities/qwen3]] — Qwen MoE family and local inference relevance
- [[wiki/entities/manjunath-janardhan]] — Apple Silicon MoE quantization benchmarks

## Sources

- [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]]
- [[wiki/sources/two-macs-80b-ai-cluster-exo]]
- [[wiki/sources/gemma-4-local-model-codex-cli]]
- [[wiki/sources/turboquant-moe-122b-macbook-apple-silicon]]
