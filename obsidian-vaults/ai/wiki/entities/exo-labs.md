---
title: "Exo Labs"
type: entity
domain: ai
tags:
  - org
  - open-source
  - distributed-inference
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/two-macs-80b-ai-cluster-exo]]"
---

# Exo Labs

Exo Labs is the open-source project and organization behind Exo — a distributed inference tool that enables pooling multiple consumer devices (Macs, Linux machines, Raspberry Pis) into a single AI inference cluster with a unified, OpenAI-compatible API.

## Background / History

Exo Labs operates primarily as an open-source project, with contributors from the AI systems and distributed computing communities. The project emerged from the observation that while individual consumer devices lack the memory and compute to run large language models efficiently, multiple devices working together can achieve aggregate specifications that rival or exceed what a single consumer device can do. The project's design philosophy emphasizes ease of use — automatic device discovery, automatic workload distribution — over the manual configuration required by earlier distributed inference approaches.

## Key Contributions / Features

**Distributed Consumer-Hardware Inference**: Exo's core capability is topology-aware tensor parallelism across heterogeneous consumer devices. Rather than requiring matching hardware or manual partition configuration, Exo automatically discovers available devices on a local network, measures their capabilities, and distributes the model's layers accordingly. A user with two Macs, or a Mac and a Linux machine, or any combination of compatible devices, can run models that neither device could run alone. (Source: [[wiki/sources/two-macs-80b-ai-cluster-exo]])

**OpenAI-Compatible API**: Exo exposes an OpenAI-compatible API endpoint from the device cluster, meaning any software that can talk to OpenAI's API — including [[wiki/entities/openclaw]], [[wiki/entities/cline]], and other agent tools — can use an Exo cluster as a drop-in local inference backend without modification.

**80B Model Demonstration**: [[wiki/entities/manjunath-janardhan]] demonstrated Exo running [[wiki/entities/qwen3]] Qwen3-Next-80B across two Mac machines at 70–80 tokens per second — a throughput sufficient for interactive agentic coding tasks.

**Broad Device Support**: Exo supports Apple Silicon Macs, NVIDIA GPUs, AMD GPUs, and even Raspberry Pi units as cluster nodes, making it relevant across the full spectrum of consumer hardware from hobbyist to prosumer.

## Role in AI Landscape

Exo Labs represents the infrastructure layer of the local AI movement — enabling the scale of model deployment that would otherwise require expensive dedicated AI hardware. As open models like [[wiki/entities/gemma-4]] and [[wiki/entities/qwen3]] approach proprietary model quality on relevant tasks, and as Exo makes 80B-scale inference practical on consumer hardware clusters, the case for cloud-dependent proprietary models weakens for privacy-sensitive and cost-sensitive use cases. Exo is one of the clearest expressions of the "AI should run on hardware you own" philosophy.

## Connections

- **Related entities**: [[wiki/entities/exo]], [[wiki/entities/manjunath-janardhan]], [[wiki/entities/qwen3]], [[wiki/entities/ollama]], [[wiki/entities/openclaw]]
- **Key concepts**: [[wiki/concepts/distributed-inference]], [[wiki/concepts/local-ai]], [[wiki/concepts/self-hosted-ai]], [[wiki/concepts/tensor-parallelism]]
- **Sources**: [[wiki/sources/two-macs-80b-ai-cluster-exo]]
