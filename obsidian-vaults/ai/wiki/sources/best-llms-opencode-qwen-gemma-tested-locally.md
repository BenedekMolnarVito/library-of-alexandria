---
title: "Best LLMs for OpenCode — From Qwen 3.5 to Gemma 4, Tested Locally"
type: source
domain: ai
tags:
  - local-llm
  - agentic-coding
  - llm-benchmarking
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Best LLMs for OpenCode — From Qwen 3.5 to Gemma 4, Tested Locally.md]]"
---

# Best LLMs for OpenCode — From Qwen 3.5 to Gemma 4, Tested Locally

**Authors**: Rost Glukhov
**Date**: 2026-03
**Type**: article

## Summary

Rost Glukhov runs a head-to-head empirical test of locally-hosted LLMs (via Ollama and llama.cpp) and some cloud models through OpenCode on two real tasks: building an IndexNow protocol CLI tool in Go, and generating a website migration map. The clear local winner is Qwen 3.5 27b at IQ3_XXS quantization on llama.cpp — complete tool with 8 passing tests at 34 tokens/sec on 16GB VRAM. Key finding: in agentic coding mode, instruction-following and tool-calling quality matters far more than raw speed or parameter count.

## Key Takeaways

- Clear local winner: Qwen 3.5 27b IQ3_XXS on llama.cpp — complete Go project, 8 unit tests passing, full README, 34 tokens/sec on 16GB VRAM, 1m12s build time.
- Bigpicle (OpenCode Zen cloud model) was the standout for methodology: it used Exa Code Search to look up the IndexNow protocol spec before writing a single line of code — the only model to do this.
- GPT-OSS 20b in default mode fails; in high-thinking mode it becomes genuinely capable — flag parsing, batching, passing tests. Mode matters as much as model.
- Qwen 3 14b shows classic hallucination under pressure: fabricated confident-sounding wrong API endpoints and documentation rather than admitting it couldn't find information.
- Devstral-small-2:24b confused at basic level — tried to write shell commands into go.mod file. Produced a binary but with no practical flag handling.
- NVIDIA Nemotron-Cascade-2-30B printed code and told the user to compile it manually — a failure of agentic loop completion.
- Key insight: for agentic coding, instruction-following and tool-calling quality matters far more than raw speed or parameter count. Hallucination is the most dangerous failure mode.
- Qwen 3.5 122b at IQ3S produced the largest set of supported engines (8 endpoints) but took 8m18s — best quality but slowest.

## Entities Mentioned

- [[wiki/entities/rost-glukhov]]
- [[wiki/entities/opencode]]
- [[wiki/entities/qwen-3-5]]
- [[wiki/entities/gemma-4]]
- [[wiki/entities/gpt-oss-20b]]
- [[wiki/entities/bigpicle]]
- [[wiki/entities/devstral]]
- [[wiki/entities/nvidia-nemotron-cascade-2]]
- [[wiki/entities/ollama]]
- [[wiki/entities/llama-cpp]]

## Concepts Covered

- [[wiki/concepts/local-llm]]
- [[wiki/concepts/quantization]]
- [[wiki/concepts/agentic-coding]]
- [[wiki/concepts/tool-calling]]
- [[wiki/concepts/llm-benchmarking]]
- [[wiki/concepts/hallucination]]
- [[wiki/concepts/instruction-following]]
- [[wiki/concepts/gguf]]

## Notable Quotes

> "For OpenCode specifically, instruction-following and tool-calling quality matters far more than raw speed."

> "Bigpicle: Before writing a single line of code, it used Exa Code Search to actually research the IndexNow protocol. It found all the correct endpoints on the first try."

> "Classic hallucination under pressure [Qwen 3 14b]: it fabricated a confident-sounding answer — wrong API endpoint, wrong authentication method."

## Cross-Connections

Directly comparable to [[wiki/sources/100-hours-claude-code-vs-antigravity]] and [[wiki/sources/building-claude-code-boris-cherny]] — all three are about evaluating agentic coding tools in practice. The hallucination pattern observed here connects to the agent reliability/eval discussion in [[wiki/sources/300-dollars-auto-research-karpathy-loop]] and [[wiki/sources/agentic-saas-playbook-2026]]. Local model focus complements the cloud-model focus of the other coding tool articles. The Gemma 4 models appear again in [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]] and [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]].
