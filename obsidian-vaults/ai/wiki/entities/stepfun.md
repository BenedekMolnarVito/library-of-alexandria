---
title: "StepFun"
type: entity
domain: ai
tags:
  - org
  - chinese-ai
  - model-provider
  - moe
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/step-3-5-flash-196b-open-source-model]]"
---

# StepFun

StepFun is a Chinese AI startup that released Step-3.5-Flash — a 196 billion parameter Mixture of Experts model — as an open-source release that competes with GPT-5.4 Turbo on reasoning benchmarks, representing one of the most capable open-weight models in the corpus covered by this wiki.

## Background / History

StepFun (阶跃星辰) was founded in 2023 by Cheng Wei and other former Baidu and ByteDance AI researchers. The company has pursued an aggressive model development roadmap, releasing progressively larger and more capable models at a pace that has attracted attention in both Chinese and international AI communities. Its focus on large-scale MoE architectures reflects a broader Chinese AI lab trend toward efficient, deployment-optimized models rather than dense parameter counts.

## Key Contributions / Features

**Step-3.5-Flash (196B MoE)**: StepFun's flagship open-source release is a 196 billion parameter Mixture of Experts model that achieves competitive reasoning benchmark scores against GPT-5.4 Turbo. The MoE architecture means that not all 196B parameters are activated for each token — only the relevant "expert" subnetworks are engaged, keeping per-token compute and inference cost substantially lower than a fully dense 196B model would require. (Source: [[wiki/sources/step-3-5-flash-196b-open-source-model]])

**Open-Weight Release Strategy**: By releasing Step-3.5-Flash as open-weight, StepFun follows a strategy of using openness to build ecosystem adoption and credibility — similar to Meta's LLaMA releases and [[wiki/entities/google-deepmind]]'s Gemma releases. For practitioners who need frontier-quality reasoning at local inference cost, large open-weight MoE models like Step-3.5-Flash represent a meaningful alternative to proprietary APIs.

## Role in AI Landscape

StepFun's Step-3.5-Flash release is part of a broader pattern of Chinese AI labs producing large, capable open models that are competitive with Western frontier proprietary models. If this trend continues, the capability gap between open and closed models — which has historically favored proprietary models — may close faster than the Western-centric AI discourse typically assumes. StepFun specifically demonstrates that 200B-scale MoE models are entering the open-weight ecosystem, with implications for both enterprise on-premises deployment and consumer local inference.

## Connections

- **Related entities**: [[wiki/entities/step-3-5-flash]], [[wiki/entities/google-deepmind]], [[wiki/entities/zhipuai]], [[wiki/entities/openai]]
- **Key concepts**: [[wiki/concepts/mixture-of-experts]], [[wiki/concepts/local-ai]], [[wiki/concepts/open-weight-models]]
- **Sources**: [[wiki/sources/step-3-5-flash-196b-open-source-model]]
