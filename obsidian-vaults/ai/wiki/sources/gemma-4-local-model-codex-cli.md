---
title: "I ran Gemma 4 as a local model in Codex CLI"
type: source
domain: ai
tags:
  - gemma-4
  - local-ai
  - codex-cli
  - benchmark
  - mixture-of-experts
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/I ran Gemma 4 as a local model in Codex CLI.md]]"
---

# I ran Gemma 4 as a local model in Codex CLI

**Authors**: Daniel Vaughan
**Date**: 2026-04
**Type**: article

## Summary

Daniel Vaughan conducts a practical benchmark of Gemma 4 as a local inference backend for Codex CLI, testing both a 26B MoE variant on a 24GB M4 Pro MacBook (via llama.cpp) and a 31B Dense variant on a Dell GB10 NVIDIA Blackwell machine (via Ollama). The key finding: the Mac generates tokens 5.1x faster but produces significantly more errors (dead code, 10 tool calls vs. 3), while the GB10's slower but higher-quality model finished 30% later but required no repair pass. Model quality dominates raw speed for agentic coding tasks — a nuanced finding that challenges the intuition that faster inference equals better agent performance.

## Key Takeaways

- Gemma 4 tool-calling jumped from 6.6% (Gemma 3) to 86.4% on tau2-bench — the gap that makes local agentic coding practical
- Mac (26B MoE, Q4_K_M, llama.cpp): 52 tok/s, 10 tool calls, dead code left in output, 5 failed test writes
- Dell GB10 (31B Dense, Ollama): 10 tok/s, 3 tool calls, clean first-pass output, passed tests on first attempt
- MoE advantage: only 3.8B active params per token vs. Dense's full 31.2B — same 273 GB/s bandwidth, 5.1x speed difference
- Cloud baseline (GPT-5.4): fastest, fewest tokens, zero repair needed — 65 seconds vs. 7 min (GB10) vs. 4m42s (Mac)
- Critical llama.cpp flags for Gemma 4 on Apple Silicon: `--jinja` (required), `-ctk q8_0 -ctv q8_0` (KV cache quantization), `web_search=disabled`
- Ollama v0.20.3 has a streaming bug on Apple Silicon with Gemma 4; Ollama v0.20.5 works on NVIDIA
- Conclusion: local is viable, but first-pass reliability matters more than token speed for agentic coding

## Entities Mentioned

- [[wiki/entities/daniel-vaughan]]
- [[wiki/entities/google]]
- [[wiki/entities/gemma-4]]
- [[wiki/entities/gpt-5-4]]
- [[wiki/entities/codex-cli]]
- [[wiki/entities/ollama]]
- [[wiki/entities/llama-cpp]]
- [[wiki/entities/dell-pro-max-gb10]]

## Concepts Covered

- [[wiki/concepts/local-ai-inference]]
- [[wiki/concepts/mixture-of-experts]]
- [[wiki/concepts/agentic-coding]]
- [[wiki/concepts/tool-calling]]
- [[wiki/concepts/model-quantization]]
- [[wiki/concepts/kv-cache]]
- [[wiki/concepts/local-vs-cloud-tradeoffs]]
- [[wiki/concepts/codex-cli]]

## Notable Quotes

> "The Mac generated tokens 5.1 times faster. It still finished only 30 per cent sooner. The time went into retries."

> "Going from 'broken' to 'works' is the step that makes local agentic coding practical."

## Cross-Connections

Directly benchmarks the same MoE efficiency discussed in [[wiki/sources/two-macs-80b-ai-cluster-exo]]. The tool-calling benchmark connects to agent framework discussions — a model that fails tool calls 93% of the time (Gemma 3) is useless for LangGraph/PydanticAI agentic tasks ([[wiki/sources/comparing-6-python-ai-agent-frameworks]]). The privacy/cost motivation mirrors [[wiki/sources/glm-5-1-free-claude-subscription-replacement]] and [[wiki/sources/two-macs-80b-ai-cluster-exo]]. Highlights an important nuance: faster inference doesn't mean better agent performance if reliability suffers — relevant to the harness engineering discussion in [[wiki/sources/anthropic-harness-engineering-two-agent-architecture]].
