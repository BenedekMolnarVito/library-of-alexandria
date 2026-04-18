---
title: "Google DeepMind"
type: entity
domain: ai
tags:
  - org
  - research-lab
  - model-provider
  - google
  - gemma
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]]"
  - "[[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]]"
  - "[[wiki/sources/gemma-4-open-source-ai-drop]]"
  - "[[wiki/sources/gemma-4-local-model-codex-cli]]"
  - "[[wiki/sources/openclaw-gemma4-free-private-ai]]"
---

# Google DeepMind

Google DeepMind is the AI research organization formed by the merger of Google Brain and DeepMind in 2023, operating as Alphabet's primary AI research and development arm. It is the creator of the Gemma open model family, among many other research and commercial AI systems.

## Background / History

Google Brain was Google's internal AI research lab, responsible for TensorFlow, the transformer architecture (published in "Attention Is All You Need"), and numerous breakthroughs in natural language processing and computer vision. DeepMind was the London-based AI lab acquired by Google in 2014, responsible for AlphaGo, AlphaFold, and foundational reinforcement learning research. Their merger into Google DeepMind in 2023 combined two of the most consequential AI research organizations in the world under a single organizational structure, with the goal of accelerating progress and eliminating duplication.

Google DeepMind's commercial relevance extends beyond research: it develops the AI systems that power Google Search, Google Assistant, Gmail smart compose, and numerous other Google products. Its research publishes widely and its models — both proprietary (Gemini family) and open-source (Gemma family) — are widely deployed.

## Key Contributions / Features

**Transformer Architecture**: Google Brain researchers (Vaswani et al.) published "Attention Is All You Need" in 2017, introducing the transformer architecture that became the foundation of virtually all modern large language models. This contribution is arguably the most consequential single paper in the AI explosion covered throughout this wiki.

**Gemma 4 Open Model Family**: Released in April 2026, Gemma 4 represents a major leap in open-source model capability — particularly for agentic tasks. The family includes a 4B embedded variant, a 12B dense model, and a 27B MoE (Mixture of Experts) model, all of which are multimodal (image + text). The 27B MoE variant activates only approximately 3.8B parameters per token, achieving inference speed roughly 5x faster than an equivalent dense model at the same memory bandwidth. The critical advancement is tool-calling capability: Gemma 3 scored 6.6% on the tau2-bench tool-calling benchmark; Gemma 4 scored 86.4% — a 13x improvement that makes local agentic coding practical for the first time with open models. (Sources: [[wiki/sources/gemma-4-open-source-ai-drop]], [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]])

**AlphaFold**: DeepMind's protein structure prediction system, which solved a 50-year-old biology grand challenge and demonstrated AI's capability to produce scientific breakthroughs in domains far from natural language.

## Role in AI Landscape

Google DeepMind occupies a unique position: it is simultaneously a frontier research lab (producing transformative papers), a commercial AI provider (Gemini family), and an open-source contributor (Gemma family). The Gemma 4 release is particularly significant in the context of this wiki because it materially changes the calculus for local AI deployment — practitioners who previously had to choose between cloud API capability and local privacy/cost can now achieve near-frontier agentic performance with open models on consumer hardware.

## Connections

- **Related entities**: [[wiki/entities/gemma-4]], [[wiki/entities/openai]], [[wiki/entities/anthropic]], [[wiki/entities/vllm]], [[wiki/entities/ollama]], [[wiki/entities/openclaw]]
- **Key concepts**: [[wiki/concepts/mixture-of-experts]], [[wiki/concepts/local-ai]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/tool-calling]]
- **Sources**: [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]], [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]], [[wiki/sources/gemma-4-open-source-ai-drop]], [[wiki/sources/gemma-4-local-model-codex-cli]], [[wiki/sources/openclaw-gemma4-free-private-ai]]
