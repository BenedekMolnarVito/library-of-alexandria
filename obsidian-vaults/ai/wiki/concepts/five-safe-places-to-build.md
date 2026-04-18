---
title: "Five Safe Places to Build in AI"
type: concept
domain: ai
tags:
  - business-strategy
  - ai-resistant
  - market-analysis
  - frameworks
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/five-safe-places-to-build-in-ai]]"
---

# Five Safe Places to Build in AI

The five safe places framework, developed by Nate B Jones, identifies business categories that are structurally resistant to AI agent substitution. While [[saas-disruption]] threatens a wide range of software middleware businesses, these five categories have properties that make them difficult or impossible for general-purpose agents to replace — either because human certification remains legally or practically required, because physical-world integration is essential, or because the value is in accumulated relationships and trust rather than workflow execution.

## Definition

The framework emerged from the observation that "safe" means different things in different contexts. Some categories are safe because agents can't technically do the work; some are safe because agents aren't legally permitted to do the work; some are safe because the value isn't in the work at all but in the relationship around it. All five categories are safe for distinct structural reasons.

## How It Works

**Category 1: Verifiable domains (legal, medical, financial compliance)**
These fields require human certification and carry legal liability. An AI agent can draft a legal brief, analyze a medical image, or flag a financial compliance issue — but a licensed professional must certify the output before it has legal standing. The certification function cannot be delegated to an agent because the legal and professional accountability system requires a human to be responsible. AI becomes a force multiplier for professionals in these domains, not a replacement. The business opportunity is in building the tools that make the certified professional more productive, not in eliminating the professional.

**Category 2: Hardware integration**
Physical-world interfaces — industrial control systems, medical devices, robotics, sensor networks — require integration with hardware that agents cannot access through software APIs. An agent can optimize a manufacturing schedule, but it cannot physically adjust the machine. Businesses that sit at the software/hardware interface have a moat that pure software agents cannot cross. The opportunity is in the agent-native control layer that bridges software AI capability and physical hardware execution.

**Category 3: Relationship capital**
Some business value is entirely in trust networks: the venture capitalist who knows which founders are exceptional before their public record reflects it, the consultant whose value is in a decade of client relationships, the recruiter whose value is in knowing who is actually available and for what. Agents cannot accumulate authentic trust relationships — they can simulate the forms of relationship building but cannot deliver the reciprocal trust that comes from shared history. Businesses whose moat is genuine relationship capital are safe from agent substitution.

**Category 4: Synthetic data and evaluation**
As AI training becomes a larger fraction of AI value creation, the demand for high-quality training data and rigorous evaluation grows. Generating synthetic data that is both realistic and correctly labeled, and building evaluation systems that accurately measure AI capability, require deep domain expertise combined with AI capability. This is a meta-layer business: building the inputs and measurements that other AI systems depend on. It is structurally safer because it sits above the capability being disrupted, not within it.

**Category 5: Orchestration and governance**
Managing agents — deciding what tasks to assign, monitoring execution, handling failures, ensuring compliance, auditing decisions — is itself a function that requires human judgment and accountability. As agent adoption grows, the management layer (who is in charge of the agents?) becomes increasingly valuable. Businesses providing orchestration infrastructure, compliance tooling, and governance frameworks for agentic systems sit in a defensible position precisely because agent proliferation is their tailwind, not their threat.

## Why It Matters

The framework is a planning tool for founders and product teams deciding where to build in the AI era. The tempting but dangerous move is to build a product that an AI agent will replace within 18 months. The strategic move is to build where the agent creates demand for your product rather than substituting it.

The framework also clarifies why some businesses are more defensible than their technical function suggests. A legal research SaaS might seem exposed to AI substitution, but if it operates in the verifiable domain category (certified professional workflow, liability-aware output), it is not. The analysis requires distinguishing what the product does (legal research — substitutable) from how the value is created and captured (certified professional workflow — not substitutable).

## In Practice

For existing businesses, apply the framework as a vulnerability audit: which of these five categories does your current business touch? How central are those characteristics to your value proposition? A business deeply embedded in hardware integration is safer than one that happens to sell hardware as a distribution channel for software.

For new products, the framework suggests five design questions: Can I build this as a tool for verifiable-domain professionals? Can I require hardware integration? Can I structure the product to accumulate relationship capital? Can I build in the data/evaluation layer? Can I provide orchestration/governance for other AI systems?

## Related Concepts

- [[wiki/concepts/saas-disruption]] — the threat this framework provides defense against
- [[wiki/concepts/agentic-saas]] — new product categories in some of these safe spaces
- [[wiki/concepts/intelligence-arbitrage]] — relevant for Category 4 (evaluation/data)
- [[wiki/concepts/outcome-agents]] — the agent design that makes Category 5 valuable

## Key Entities

- [[wiki/entities/nate-b-jones]] — developed the framework

## Sources

- [[wiki/sources/five-safe-places-to-build-in-ai]]
