---
title: "Manjunath Janardhan"
type: entity
domain: ai
tags:
  - person
  - practitioner
  - distributed-inference
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/two-macs-80b-ai-cluster-exo]]"
---

# Manjunath Janardhan

Manjunath Janardhan is a practitioner who demonstrated the use of [[wiki/entities/exo]] to pool two consumer Mac machines into a distributed 80B parameter AI inference cluster — providing one of the most concrete public demonstrations of Exo's capability for hobbyist and small-team AI deployments.

## Background / History

Janardhan operates as an independent practitioner and content creator in the local AI space. His work sits at the intersection of the self-hosted AI movement and the distributed systems capabilities that tools like Exo enable. His demonstration of the two-Mac cluster became a reference point for practitioners evaluating whether distributed local inference is practically achievable without specialized hardware.

## Key Contributions / Features

**Two-Mac 80B Cluster with Exo**: Janardhan configured two consumer Mac computers to work together as a single 80B parameter inference cluster using the Exo distributed inference tool. The configuration achieved 70–80 tokens per second running [[wiki/entities/qwen3]] Qwen3-Next-80B — a throughput that makes large-model inference practically usable for interactive tasks, not just batch processing. The demonstration was significant because it showed that 80B models, which typically require expensive dedicated GPU infrastructure, can be run on consumer hardware through device pooling. (Source: [[wiki/sources/two-macs-80b-ai-cluster-exo]])

**Practical Distributed Inference Guide**: By documenting the specific setup — hardware, configuration, performance metrics — Janardhan's work provides a reproducible template for others who want to achieve similar results with available consumer hardware.

## Role in AI Landscape

Janardhan's two-Mac cluster demonstration is a data point in the larger narrative about local AI capability — specifically, the question of whether open models can match cloud AI performance on consumer hardware. By achieving 70–80 tok/s on an 80B model with two Macs, his work helps establish the practical ceiling for hobbyist distributed inference and demonstrates that the gap between cloud and local is closing for inference workloads.

## Connections

- **Related entities**: [[wiki/entities/exo-labs]], [[wiki/entities/exo]], [[wiki/entities/qwen3]], [[wiki/entities/ollama]]
- **Key concepts**: [[wiki/concepts/distributed-inference]], [[wiki/concepts/local-ai]], [[wiki/concepts/self-hosted-ai]]
- **Sources**: [[wiki/sources/two-macs-80b-ai-cluster-exo]]
