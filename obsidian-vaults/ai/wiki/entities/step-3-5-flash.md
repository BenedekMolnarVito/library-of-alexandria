---
title: "Step-3.5-Flash"
type: entity
domain: ai
tags:
  - model
  - stepfun
  - moe
  - open-weight
  - reasoning
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/step-3-5-flash-196b-open-source-model]]"
---

# Step-3.5-Flash

Step-3.5-Flash is a 196 billion parameter Mixture of Experts language model released by [[wiki/entities/stepfun]] as an open-weight model. It achieves competitive performance with GPT-5.4 Turbo on reasoning benchmarks, representing one of the most capable openly available models in the current landscape.

## Background / History

Step-3.5-Flash is part of StepFun's Step series, which the company has developed at an aggressive pace since its 2023 founding. The "Flash" designation likely refers to inference efficiency — the MoE architecture ensures that despite the 196B total parameter count, per-token compute is substantially lower than a dense model of equivalent total size. The model's open-weight release follows a pattern common to Chinese AI labs of using model openness as a distribution and credibility strategy.

## Key Contributions / Features

**196B Parameter MoE Architecture**: Step-3.5-Flash uses a Mixture of Experts design with 196B total parameters. In a typical MoE configuration, only a fraction of these parameters (perhaps 20–30B) are active for any given token, maintaining the efficiency benefits of a smaller model while retaining the knowledge capacity of a larger one. This architectural choice reflects the industry's convergence on MoE as the preferred approach for large efficient models — as seen also in [[wiki/entities/gemma-4]]'s 27B MoE.

**GPT-5.4 Turbo Competitive Benchmarks**: The model was benchmarked against GPT-5.4 Turbo on reasoning tasks, showing competitive results that position it as a viable open alternative to frontier proprietary models for reasoning-intensive workloads. For practitioners who need strong reasoning capability at local inference cost, this benchmark result is a signal worth evaluating independently. (Source: [[wiki/sources/step-3-5-flash-196b-open-source-model]])

**Open-Weight Availability**: Being open-weight means practitioners can run Step-3.5-Flash on their own hardware without API costs or data privacy concerns — a significant practical advantage for enterprise deployments with sensitive data or budget constraints.

## Role in AI Landscape

Step-3.5-Flash is a data point in the ongoing convergence of open and closed model capability. If 196B MoE models can match GPT-5.4 Turbo on reasoning benchmarks while being open-weight and locally deployable, the argument for cloud-only inference of proprietary models weakens substantially for reasoning workloads. The model is most relevant for practitioners who need strong reasoning capability (as opposed to frontier coding or instruction-following, where [[wiki/entities/gemma-4]] and [[wiki/entities/claude-model-family]] respectively lead) and want to deploy locally.

## Connections

- **Related entities**: [[wiki/entities/stepfun]], [[wiki/entities/gemma-4]], [[wiki/entities/glm-5-1]], [[wiki/entities/openai]], [[wiki/entities/vllm]]
- **Key concepts**: [[wiki/concepts/mixture-of-experts]], [[wiki/concepts/open-weight-models]], [[wiki/concepts/local-ai]], [[wiki/concepts/reasoning]]
- **Sources**: [[wiki/sources/step-3-5-flash-196b-open-source-model]]
