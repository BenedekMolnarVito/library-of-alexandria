---
title: "GLM-5.1 Just Beat GPT-5.4 and Claude Opus (And It's Free and Open-Source)"
type: source
domain: ai
tags:
  - open-source-ai-models
  - swe-bench-pro
  - china-ai-development
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/GLM-5.1 Just Beat GPT-5.4 and Claude Opus (And It's Free and Open-Source).md]]"
---

# GLM-5.1 Just Beat GPT-5.4 and Claude Opus (And It's Free and Open-Source)

**Authors**: Ai studio (Medium)
**Date**: 2026-04
**Type**: article

## Summary

Z.ai (formerly Zhipu AI, a Tsinghua University spinout that IPO'd in Hong Kong in January 2026) released GLM-5.1 on April 7, 2026, scoring 58.4 on SWE-Bench Pro — topping GPT-5.4 (57.7) and Claude Opus 4.6 (57.3). Notably, it was trained entirely on ~100,000 Huawei chips without any American silicon, despite Z.ai being on the US Entity List. It is free under the MIT license and excels at long-horizon autonomous tasks (tested sustaining productive work across 1,700 steps). Limitations: no image processing, slow decode (~44 tok/s), and the benchmark is self-reported.

## Key Takeaways

- GLM-5.1 scored 58.4 on SWE-Bench Pro: #1 globally, above GPT-5.4 (57.7), Claude Opus 4.6 (57.3), and Gemini 3.1 Pro (54.2).
- Free and MIT-licensed — downloadable from HuggingFace, API at $1.40/$4.40 per million in/out tokens.
- Trained entirely on ~100,000 Huawei chips; Z.ai is on the US Entity List and cannot buy Nvidia GPUs.
- In an 8-hour autonomous test, ran 655+ self-testing rounds and achieved 7x speed optimization.
- Sustained productive work across 1,700+ steps — far beyond the 20–30 step limit of typical models.
- Uses a 'staircase pattern': recognizes when current approach is exhausted, shifts strategy, opens a new performance level.
- No image processing capability; Claude Opus 4.6 retains advantage on multimodal and aggregate coding benchmarks.
- Open-source AI gap vs closed models: from ~2 years behind (2023) to now tied at the frontier (April 2026).

## Entities Mentioned

- [[wiki/entities/z-ai]]
- [[wiki/entities/glm-5-1]]
- [[wiki/entities/gpt-5-4]]
- [[wiki/entities/claude-opus-4-6]]
- [[wiki/entities/gemini-3-1-pro]]
- [[wiki/entities/tsinghua-university]]
- [[wiki/entities/huawei]]
- [[wiki/entities/deepseek]]
- [[wiki/entities/qwen-alibaba]]
- [[wiki/entities/moonshot-ai]]
- [[wiki/entities/unsloth]]

## Concepts Covered

- [[wiki/concepts/swe-bench-pro]]
- [[wiki/concepts/open-source-ai-models]]
- [[wiki/concepts/ai-chip-export-controls]]
- [[wiki/concepts/coding-benchmarks]]
- [[wiki/concepts/long-horizon-autonomous-tasks]]
- [[wiki/concepts/china-ai-development]]
- [[wiki/concepts/self-improving-agents]]
- [[wiki/concepts/mit-license-ai]]

## Notable Quotes

> "A model trained entirely on non-American, domestically produced hardware just topped a globally respected benchmark."

> "Open-source AI gap vs closed models: from roughly two years behind (2023) to sitting at the top of one of the most respected coding benchmarks (April 2026)."

## Cross-Connections

Directly challenges the Anthropic/OpenAI frontier model duopoly narrative built across many other sources in this batch. The export controls angle connects to ongoing geopolitical AI policy debates. The long-horizon autonomous task performance (1,700+ steps) is the most extreme example of the agentic loop capability discussed in [[wiki/sources/from-ides-to-ai-agents-steve-yegge]] and [[wiki/sources/claude-code-paperclip-destroyed-openclaw]]. The self-reporting caveat connects to benchmark credibility discussions in [[wiki/sources/100-hours-claude-code-vs-antigravity]]. Pairs with [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]] as another open-source frontier model story.
