---
title: "Nick Saraev"
type: entity
domain: ai
tags:
  - person
  - practitioner
  - content-creator
  - prompt-optimization
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
---

# Nick Saraev

Nick Saraev is a practitioner who applied [[wiki/entities/andrej-karpathy]]'s autoresearch pattern to text-to-image prompt optimization, achieving a striking result — improving a prompt score from 32/40 to 40/40 in just 12 minutes — and then documented the experience as a case study in the pattern's generalizability.

## Background / History

Saraev operates as an independent AI practitioner and content creator. His application of the autoresearch pattern to text-to-image generation is notable because it moved the pattern from Karpathy's original domain (research/knowledge synthesis) into creative media generation — demonstrating the pattern's domain-agnosticism and making it more accessible to a broader range of practitioners.

## Key Contributions / Features

**Autoresearch Applied to Text-to-Image**: Saraev ran the autoresearch loop — iterative LLM-scored generation with keep/discard selection — on text-to-image prompts, using an LLM as the evaluation judge. Starting from a baseline score of 32/40 against a rubric, the loop converged to 40/40 in approximately 12 minutes. This result is significant for several reasons: (1) it demonstrates the pattern works outside text tasks, (2) the convergence speed (12 minutes) is fast enough to be practically useful, and (3) using an LLM as the quality judge worked even for a creative/visual task where ground truth is subjective. (Source: [[wiki/sources/karpathy-autoresearch-universal-skill]])

**Cross-Domain Generalization Evidence**: Saraev's experiment, alongside [[wiki/entities/balu-kosuri]]'s universal skill formulation, is one of the key data points supporting the claim that the autoresearch pattern is truly a universal optimization primitive rather than a domain-specific technique.

## Role in AI Landscape

Saraev's contribution is as a practitioner-validator for the autoresearch pattern — someone who tried it in an unexpected domain and found it worked, then shared the result. In a field where many ideas are claimed to be universal but few are empirically tested outside their origin domain, this kind of cross-domain validation is genuinely valuable.

## Connections

- **Related entities**: [[wiki/entities/andrej-karpathy]], [[wiki/entities/balu-kosuri]]
- **Key concepts**: [[wiki/concepts/autoresearch-loop]], [[wiki/concepts/prompt-optimization]], [[wiki/concepts/llm-as-judge]]
- **Sources**: [[wiki/sources/karpathy-autoresearch-universal-skill]]
