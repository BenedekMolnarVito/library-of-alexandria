---
title: "Software 3.0"
type: concept
domain: ai
tags:
  - software-paradigms
  - llm
  - agentic-coding
  - software-architecture
  - karpathy
created: 2026-04-21
updated: 2026-04-21
sources:
  - "[[wiki/sources/software-stack-1-0-2-0-3-0]]"
---

# Software 3.0

Software 3.0 is Andrej Karpathy's framing for systems programmed through natural language on top of large language models. In this view, traditional code remains Software 1.0, learned model weights remain Software 2.0, and language-directed agent behavior becomes a third layer. The important question is not which layer wins, but which layer is in control and how the others are composed around it. (Source: [[wiki/sources/software-stack-1-0-2-0-3-0]])

## Definition

- **Software 1.0**: explicit procedural code
- **Software 2.0**: learned behavior encoded in model weights
- **Software 3.0**: natural-language control over general-purpose model intelligence

Software 3.0 does not replace the other layers. It orchestrates them.

## How It Works

The central pattern is an LLM in the driver's seat using tools:

- APIs and codebases as Software 1.0 capabilities
- narrow models as Software 2.0 capabilities
- other agents as Software 3.0 capabilities

Once the LLM controls tool choice, sequence, and adaptation, the system moves from workflow to agent.

## Why It Matters

This framing resolves a common confusion in AI coding discourse: when an agent writes a file, the resulting artifact is still Software 1.0. What changed is who produced it and how the system was directed.

It also clarifies why agents feel like a genuine platform shift. Natural language is no longer just UI sugar over software; it is a control plane for composing code, models, and tools.

## In Practice

Software 3.0 works best when:

- goals are specified clearly
- the model is given a constrained but useful tool surface
- verification remains outside the model where possible
- humans decide where determinism is required and where autonomy is acceptable

## Related Concepts

- [[wiki/concepts/agentic-coding]] — the practical frontier of Software 3.0
- [[wiki/concepts/skill-md]] — one way to package Software 3.0 behavior
- [[wiki/concepts/agent-native-infrastructure]] — infrastructure pressure created by Software 3.0 systems

## Key Entities

- [[wiki/entities/andrej-karpathy]] — coined the Software 2.0 and 3.0 framing

## Sources

- [[wiki/sources/software-stack-1-0-2-0-3-0]]
