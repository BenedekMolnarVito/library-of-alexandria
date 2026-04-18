---
title: "Distributed Inference"
type: concept
domain: ai
tags:
  - local-models
  - inference
  - distributed-systems
  - exo
  - apple-silicon
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/two-macs-80b-ai-cluster-exo]]"
---

# Distributed Inference

Distributed inference is the technique of running a single large language model across multiple physical devices, pooling their memory and compute to enable model sizes that exceed what any single device could hold. Where [[local-ai-inference]] is bounded by the memory of a single machine, distributed inference removes that bound by splitting the model across a cluster of local devices. The practical result is that consumer hardware clusters (two MacBook Pros, a Raspberry Pi farm, a mixed device collection) can run 80B+ parameter models that would otherwise require expensive server-class GPU hardware.

## Definition

A distributed inference system distributes the model's layers across devices: device A holds layers 1–20, device B holds layers 21–40, and so on (pipeline parallelism). Alternatively, each layer is split across devices (tensor parallelism), with each device holding a fraction of each weight matrix. In both cases, activations (the intermediate computations) pass between devices during each forward pass.

The key challenge is inter-device communication latency. If devices are connected via WiFi (several hundred megabits per second, high variable latency), the communication overhead may dominate inference time, negating the benefit of distribution. If devices are connected via RDMA-capable high-bandwidth links (Thunderbolt 5 on Apple M4 Pro/Max hardware), the latency drops dramatically.

## How It Works

**Exo** is the primary tool for consumer-hardware distributed inference. Its key design features:

- **Topology-aware tensor parallelism**: Exo analyzes the actual network topology between devices and optimizes the distribution accordingly. It doesn't assume uniform bandwidth between all device pairs — it places high-communication-frequency layer pairs on devices that are physically close or connected by high-bandwidth links.
- **Automatic device discovery**: devices on the same network are discovered automatically via mDNS. No manual configuration of cluster topology required.
- **OpenAI-compatible API**: the cluster exposes a standard OpenAI-compatible endpoint, meaning any tool that works with the OpenAI API (Claude Code with API compatibility mode, LM Studio, most open-source tools) can use the distributed cluster without modification.
- **Heterogeneous hardware support**: Exo supports mixed-device clusters — M1, M2, M3, M4 Macs, iPhones, iPads, NVIDIA GPUs, and Raspberry Pis can participate in the same cluster, each contributing its available memory and compute.

**RDMA over Thunderbolt 5**: Apple's M4 Pro and M4 Max chips support RDMA (Remote Direct Memory Access) over Thunderbolt 5, enabling 99% reduction in inter-node latency compared to WiFi. Two M4 Pro MacBook Pros connected via Thunderbolt 5 can run distributed inference with near-LAN latency, making the distribution overhead negligible for large models.

A concrete example: two M4 MacBook Pros with 64GB each, connected via Thunderbolt 5 RDMA, can run an 80B-parameter MoE model like Qwen3-80B. Either device alone would be insufficient (80B parameters at 4-bit quantization ≈ 40GB, plus KV cache and runtime overhead exceeds 64GB). Together, they provide 128GB of effective memory with sub-millisecond inter-device latency.

## Why It Matters

Distributed inference changes the economics of local large-model capability. Instead of requiring a single expensive workstation with a large GPU, users can cluster existing hardware. For many developers and researchers, the relevant comparison is: "I already own two MacBooks — should I buy an expensive GPU server, or can I cluster what I have?"

The combination of Exo's topology awareness, Thunderbolt 5 RDMA, and [[mixture-of-experts]] architecture makes the answer increasingly practical. A two-device M4 cluster running a 80B MoE model provides frontier-tier reasoning quality at near-zero marginal inference cost — once the hardware is owned.

This capability tier — 80B+ parameters, local, zero marginal cost — is qualitatively different from what was available to individual developers even in 2023. It enables research-scale model experiments, privacy-preserving large-model deployment, and [[karpathy-loop]] optimization at frontier quality levels without API cost constraints.

## In Practice

Exo clusters work best with devices on the same high-bandwidth local network. WiFi-based clustering is functional but slower — suitable for large batch jobs where latency matters less than throughput. Thunderbolt/Ethernet clustering is necessary for interactive inference quality.

The Raspberry Pi cluster case is worth noting: dozens of Raspberry Pi 4/5 devices, each contributing 4–8GB of memory, can aggregate to run surprisingly large models. The latency is higher than Apple Silicon clusters, making this more suitable for batch inference than interactive use. But it demonstrates the architectural generality of distributed inference — almost any hardware can participate.

## Related Concepts

- [[wiki/concepts/local-ai-inference]] — the single-device foundation
- [[wiki/concepts/mixture-of-experts]] — enables larger models at lower per-token compute
- [[wiki/concepts/local-hard-takeoff]] — distributed inference accelerates the quality convergence
- [[wiki/concepts/intelligence-arbitrage]] — distributed local clusters as the low-cost tier
- [[wiki/concepts/agent-native-infrastructure]] — infrastructure designed for agent-scale concurrency

## Key Entities

- [[wiki/entities/apple]] — Apple Silicon hardware with RDMA over Thunderbolt 5
- [[wiki/entities/exo-labs]] — Exo distributed inference tool

## Sources

- [[wiki/sources/two-macs-80b-ai-cluster-exo]]
