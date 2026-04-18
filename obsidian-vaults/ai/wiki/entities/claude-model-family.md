---
title: "Claude Model Family"
type: entity
domain: ai
tags:
  - model
  - anthropic
  - claude
  - haiku
  - sonnet
  - opus
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/building-claude-code-boris-cherny]]"
  - "[[wiki/sources/codex-and-claude-side-by-side]]"
  - "[[wiki/sources/100-hours-claude-code-vs-antigravity]]"
---

# Claude Model Family

The Claude model family is [[wiki/entities/anthropic]]'s suite of large language models, organized into three capability tiers — Haiku, Sonnet, and Opus — that span fast/cheap to powerful/expensive. Claude models are the backbone of [[wiki/entities/claude-code]] and are the most widely used inference backend for the agentic coding workflows documented in this wiki.

## Background / History

Anthropic released the first Claude model in 2023, following the company's founding in 2021 by ex-OpenAI researchers. The naming convention (Haiku/Sonnet/Opus) was introduced with the Claude 3 generation, replacing numeric versioning with a tier metaphor borrowed from poetry forms — small/medium/large in terms of both parameter count and poetic elaboration. Claude models were developed with Anthropic's Constitutional AI training methodology, which uses self-critique and human feedback to improve helpfulness and reduce harm.

By Claude 3.7, Sonnet had become the flagship model for coding tasks, introducing "extended thinking" — visible chain-of-thought reasoning where the model works through complex problems step by step before responding. This capability, combined with strong instruction-following and large context windows, made Claude 3.7 Sonnet the dominant model choice for agentic coding tools that require reliable multi-step task execution.

## Key Contributions / Features

**Haiku**: The fast, low-cost tier — designed for applications requiring high throughput, low latency, or constrained budgets. Haiku is used for tasks where response speed matters more than capability ceiling, such as rapid iteration loops, high-frequency agent sub-tasks, or cost-sensitive production deployments.

**Sonnet**: The balanced tier — combining substantial capability with manageable cost. Claude 3.7 Sonnet, with extended thinking, became the primary model for serious agentic coding use — capable enough to handle complex multi-file programming tasks while remaining cost-viable for heavy users. [[wiki/entities/nate-herk]]'s Polymarket trading bot and most of the Claude Code workflows documented in the corpus used Sonnet as the primary model. (Source: [[wiki/sources/100-hours-claude-code-vs-antigravity]])

**Opus**: The flagship capability tier — highest performance, highest cost. Used for the most demanding reasoning tasks, complex architectural decisions, and cases where output quality is worth the premium.

**Extended Thinking (Claude 3.7+)**: The introduction of visible step-by-step reasoning in Claude 3.7 Sonnet marked a qualitative change in what the model could reliably accomplish on multi-step coding and reasoning tasks. Extended thinking allows the model to "think out loud" before committing to an answer, catching errors earlier and producing more reliable results on complex problems.

**Strong Instruction Following**: Across the practitioner community, Claude models are consistently praised for their instruction-following reliability — staying within specified constraints, respecting formatting requirements, and honoring negative instructions ("don't do X") more reliably than competing models. This property is particularly valuable for agentic tasks where following complex, multi-part instructions over long contexts is essential.

## Role in AI Landscape

The Claude family's dominance in the agentic coding space is not merely a product of Anthropic's marketing — practitioners who have tested both Claude and [[wiki/entities/openai]]'s GPT models for coding tasks frequently report Claude's reliability advantage on instruction following and multi-step code generation. The side-by-side comparison of Claude and Codex CLI (Source: [[wiki/sources/codex-and-claude-side-by-side]]) provides practitioner-generated evidence on relative strengths. As [[wiki/entities/gemma-4]] and other open models improve, Claude's position as the default agentic coding backend will be increasingly contested, but as of April 2026 it remains the reference standard.

## Connections

- **Related entities**: [[wiki/entities/anthropic]], [[wiki/entities/claude-code]], [[wiki/entities/openai]], [[wiki/entities/boris-cherny]], [[wiki/entities/nate-herk]]
- **Key concepts**: [[wiki/concepts/extended-thinking]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/constitutional-ai]], [[wiki/concepts/large-language-models]]
- **Sources**: [[wiki/sources/building-claude-code-boris-cherny]], [[wiki/sources/codex-and-claude-side-by-side]], [[wiki/sources/100-hours-claude-code-vs-antigravity]]
