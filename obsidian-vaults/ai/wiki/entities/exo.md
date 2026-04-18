---
title: "Exo"
type: entity
domain: ai
tags:
  - product
  - open-source
  - distributed-inference
  - local-ai
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/two-macs-80b-ai-cluster-exo]]"
---

# Exo

Exo is an open-source distributed inference tool that enables pooling multiple consumer devices — Macs, Linux machines, Raspberry Pis, any combination — into a single AI inference cluster that presents a unified OpenAI-compatible API. It is the primary product of [[wiki/entities/exo-labs]] and the infrastructure behind [[wiki/entities/manjunath-janardhan]]'s two-Mac 80B model demonstration.

## Background / History

Exo was developed by the Exo Labs team as an open-source project with the goal of democratizing large model inference by making it possible on hardware that individuals already own. The key insight is that while a single consumer Mac might not have enough unified memory to load a 70B parameter model, two Macs together almost certainly do — and with topology-aware tensor parallelism, the computational work can be distributed across both devices with acceptable communication overhead.

The project draws on academic research in distributed deep learning (tensor parallelism, pipeline parallelism) and makes it accessible through a high-level tool that handles device discovery and workload distribution automatically.

## Key Contributions / Features

**Topology-Aware Tensor Parallelism**: Exo's core technical capability is distributing model layers across multiple devices in a way that accounts for the actual network topology — minimizing communication overhead by understanding which devices are on the same local network segment, connected via Thunderbolt, or linked via higher-bandwidth connections. This makes the distribution genuinely efficient rather than naive layer-splitting.

**Automatic Device Discovery**: Exo discovers available devices on the local network automatically via mDNS/Bonjour, so a user does not need to manually configure which machines participate in the cluster. Devices announce themselves and Exo coordinates the workload distribution.

**OpenAI-Compatible API**: The cluster presents a single OpenAI-compatible API endpoint, making Exo a drop-in replacement for cloud API calls in any compatible tool. [[wiki/entities/openclaw]], [[wiki/entities/cline]], and [[wiki/entities/ollama]]-compatible tools can all route inference to an Exo cluster without modification.

**Broad Device Support**: Exo supports Apple Silicon (Mac), NVIDIA GPUs (Linux/Windows), AMD GPUs, and even Raspberry Pi as cluster nodes — with graceful degradation for slower nodes. This makes it relevant across a wide range of hardware configurations.

**80B Model Demonstration**: The benchmark demonstration by [[wiki/entities/manjunath-janardhan]] running [[wiki/entities/qwen3]] Qwen3-Next-80B at 70–80 tok/s across two Macs established Exo's capability at a size class previously considered impractical for consumer hardware. (Source: [[wiki/sources/two-macs-80b-ai-cluster-exo]])

## Role in AI Landscape

Exo extends the local AI frontier upward — while [[wiki/entities/ollama]] makes it easy to run models that fit on a single machine, Exo removes the single-machine constraint for users who have multiple devices. As models grow larger and more capable, Exo ensures that the most capable open models remain accessible to practitioners who don't have cloud budgets or dedicated GPU infrastructure. It is a key piece of the infrastructure that makes "local AI that rivals cloud API capability" achievable.

## Connections

- **Related entities**: [[wiki/entities/exo-labs]], [[wiki/entities/manjunath-janardhan]], [[wiki/entities/qwen3]], [[wiki/entities/ollama]], [[wiki/entities/openclaw]], [[wiki/entities/gemma-4]]
- **Key concepts**: [[wiki/concepts/distributed-inference]], [[wiki/concepts/local-ai]], [[wiki/concepts/self-hosted-ai]], [[wiki/concepts/tensor-parallelism]]
- **Sources**: [[wiki/sources/two-macs-80b-ai-cluster-exo]]
