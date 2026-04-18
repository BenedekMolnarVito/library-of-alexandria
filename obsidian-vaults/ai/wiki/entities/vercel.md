---
title: "Vercel"
type: entity
domain: ai
tags:
  - org
  - developer-infrastructure
  - ai-native-tooling
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/vercel-v0-d0-agent-lessons]]"
---

# Vercel

Vercel is a developer infrastructure company best known for its frontend hosting platform and the Next.js framework, which is rearchitecting its developer tooling stack around AI agents as primary users and builders — most concretely through its v0 (AI UI generation) and d0 (agent-native execution) products.

## Background / History

Vercel was founded in 2015 (originally as ZEIT) by Guillermo Rauch and grew to become one of the dominant platforms for deploying frontend web applications, particularly React and Next.js applications. The company created and maintains Next.js, the most widely used React framework, giving it deep influence over the developer tooling ecosystem. With CTO [[wiki/entities/malte-ubl]] (formerly of Google/AMP) leading technical strategy, Vercel has positioned itself as the infrastructure layer for the next generation of AI-native web development.

## Key Contributions / Features

**v0 (AI UI Generation)**: Vercel's v0 product generates complete, deployable React UI components from natural language descriptions. Unlike code-suggestion tools, v0 produces runnable, immediately previewable output hosted on Vercel infrastructure — closing the loop between idea, implementation, and deployment. v0 represents Vercel's bet that AI will become the primary author of frontend code, and that the company which controls the generation-to-deployment pipeline will capture significant value in that transition.

**d0 (Agent-Native Execution)**: Vercel is building d0 as infrastructure designed from the ground up for agent execution workloads — recognizing that agents have fundamentally different resource consumption patterns than human-driven applications (high parallelism, variable duration, tool-calling loops, non-linear execution paths). d0 aims to provide the execution substrate that makes agentic applications practical at scale.

**Lessons from Building Agent Tools**: Malte Ubl and the Vercel team have shared publicly the hard-won insights from building v0 and d0 — including the importance of fast feedback loops for agent-generated code, the difficulty of evaluating agent output quality programmatically, and the infrastructure changes required to serve agent workloads cost-effectively. (Source: [[wiki/sources/vercel-v0-d0-agent-lessons]])

## Role in AI Landscape

Vercel's strategic bet is that the shift from human-authored to AI-authored web applications will be the biggest infrastructure transition of the 2020s, and that by owning both the generation layer (v0) and the execution layer (d0), it can maintain its relevance and market position through the transition. This represents one of the clearest examples of an established developer infrastructure company reinventing itself around AI agents rather than treating AI as an additive feature.

## Connections

- **Related entities**: [[wiki/entities/malte-ubl]], [[wiki/entities/claude-code]], [[wiki/entities/codex-cli]]
- **Key concepts**: [[wiki/concepts/agent-first-development]], [[wiki/concepts/ai-native-infrastructure]], [[wiki/concepts/agentic-coding]]
- **Sources**: [[wiki/sources/vercel-v0-d0-agent-lessons]]
