---
title: "Gemma-4-E4B-it and Qwen3.5–4B Comparison"
type: source
domain: ai
tags:
  - model-comparison
  - local-inference-llamacpp
  - code-generation-quality
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Gemma-4-E4B-it and Qwen3.5–4B comparison.md]]"
---

# Gemma-4-E4B-it and Qwen3.5–4B Comparison

**Authors**: jon allen
**Date**: 2026-04
**Type**: article

## Summary

Jon Allen compares Gemma 4 E4B and Qwen 3.5 4B on C++, Pascal algorithm generation, and a logic test, running both via llama.cpp on a 16GB MacBook Pro. Gemma 4 wins clearly on C++ — producing modern C++11-style code with zero compilation errors vs Qwen's one failure and competitive-programming-style shortcuts. Qwen 3.5 4B is described as better at reasoning but at 2–5x the reasoning token cost, making responses 2–3x longer for complex problems. Pascal is unreliable for both models (~20–50% compilation success).

## Key Takeaways

- Gemma 4 E4B: 10/10 C++ files compiled and ran without error; Qwen 3.5 4B: 9/10 (one logical error in quicksort).
- Gemma 4 produces modern C++11 conventions (vectors, const references, clean structure); Qwen writes competitive-programming-style C (raw arrays, `using namespace std`).
- Qwen 3.5 4B is better at reasoning tasks but costs 2–5x more reasoning tokens — responses can be 2–3x longer.
- Both models fit on a 16GB MacBook Pro when run via llama.cpp.
- Pascal code generation is unreliable for both — only 20–50% compiles without corrections.
- Gemma 4 is faster for agentic workflows and code generation; Qwen 3.5 better for pure reasoning.
- Judge models used: Mistral Large and Gemini Pro 3.1 (plus author review and actual compilation tests).

## Entities Mentioned

- [[wiki/entities/jon-allen]]
- [[wiki/entities/google]]
- [[wiki/entities/gemma-4-e4b]]
- [[wiki/entities/alibaba]]
- [[wiki/entities/qwen-3-5-4b]]
- [[wiki/entities/mistral-large]]
- [[wiki/entities/gemini-pro-3-1]]
- [[wiki/entities/llama-cpp]]

## Concepts Covered

- [[wiki/concepts/model-comparison]]
- [[wiki/concepts/local-inference-llamacpp]]
- [[wiki/concepts/code-generation-quality]]
- [[wiki/concepts/reasoning-tokens]]
- [[wiki/concepts/model-evaluation]]
- [[wiki/concepts/c-plus-plus-code-generation]]
- [[wiki/concepts/agentic-workflow-performance]]

## Notable Quotes

> "Gemma4 is newer and is quicker in most cases for agentic workflows. Better at code generation. Qwen 3.5 4B is better at reasoning — but the cost is 2 to 5 times the number of reasoning tokens."

> "The comparison isn't quite apples to apples. Maybe a 'Fuji' to a 'Granny Smith'."

## Cross-Connections

Directly paired with [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]] — same model family on different hardware and with different focus. The Qwen 3.5 series also appears in [[wiki/sources/best-llms-opencode-qwen-gemma-tested-locally]] as the local champion. Connects to the broader open-source small-model ecosystem alongside [[wiki/sources/glm-5-1-beats-gpt-5-4-claude-opus]]. The reasoning token cost trade-off here echoes the advisor strategy's insight in [[wiki/sources/claude-advisor-strategy-stop-using-opus]] — knowing when to use expensive reasoning vs fast generation is fundamental to agentic cost management.
