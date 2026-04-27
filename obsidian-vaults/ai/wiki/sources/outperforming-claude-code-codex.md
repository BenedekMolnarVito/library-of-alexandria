---
title: "Outperforming Claude Code and Codex for Local LLM Workflows"
type: source
domain: ai
tags:
  - local-llm
  - claude-code
  - codex
  - benchmarks
  - performance-comparison
created: 2026-04-27
updated: 2026-04-27
raw: "[[raw/Outperforming Claude Code and Codex for Local LLM Workflows.md]]"
---

# Outperforming Claude Code and Codex for Local LLM Workflows

**Type**: Benchmark / Technical comparison
**Source**: Performance testing of local LLM agents vs. cloud alternatives

## Summary

Compares local LLM inference (via Ollama, vLLM, llama.cpp) against Claude Code and Codex. When running models locally, certain approaches and configurations outperform cloud-based agents on latency, cost, and control. Examines quantization, batch processing, and tool-call efficiency.

## Key Takeaways

- **Local inference latency can beat cloud** — Lower RTT + no queue wait; offset by slower inference on consumer hardware
- **Quantization sweet spots identified** — Q5_K_M and Q6_K balance quality and VRAM
- **Context window tuning essential** — Default 4K-8K insufficient for agentic workflows; 32K+ needed
- **Tool-call format matters** — Smaller models struggle with complex JSON; simpler formats (diff-based, structured text) work better
- **Cost advantage** — No per-token billing; electricity is marginal cost

## Entities Mentioned

- [[wiki/entities/claude-code]]
- [[wiki/entities/codex-cli]]
- [[wiki/entities/ollama]]
- [[wiki/entities/vllm]]
- [[wiki/entities/llama-cpp]]

## Concepts Covered

- [[wiki/concepts/local-ai-inference]]
- [[wiki/concepts/quantization]]
- [[wiki/concepts/tool-call-bottleneck]]
- [[wiki/concepts/context-window-management]]

## Personal Notes

Bridges gap between cloud agent simplicity and local model control. Important for understanding tradeoffs between convenience and customization.
