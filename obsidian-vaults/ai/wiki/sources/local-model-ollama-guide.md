---
title: "Ön a következőt mondta: I want to use my local mod..."
type: source
domain: ai
tags:
  - local-models
  - ollama
  - qwen
  - claude-code
  - litellm
created: 2026-04-27
updated: 2026-04-27
raw: "[[raw/Ön a következőt mondta I want to use my local mod.md]]"
---

# Local Model Setup: Ollama + Claude Code Integration

**Type**: Technical conversation / troubleshooting guide
**Source**: Gemini conversation on running local Qwen models with Claude Code

## Summary

A troubleshooting dialogue on integrating Ollama-hosted Qwen2.5-Coder (7B) with Claude Code via a LiteLLM proxy. Includes solutions for API dialect mismatches, Docker containerization of LiteLLM proxy, and comparison of local-first agentic CLIs (Aider, Goose, Roo Code, OpenCode).

## Key Takeaways

- **API dialect mismatch** — Claude Code speaks Anthropic API; Ollama speaks OpenAI-compatible. LiteLLM bridges the gap.
- **LiteLLM proxy solution** — Maps Anthropic model names to Ollama backend; transparently translates API calls
- **Docker containerization** — `litellm-prox-local` container on Windows via Docker Desktop; uses `host.docker.internal` to access Windows Ollama
- **7B model limitations** — Qwen 7B struggles with complex JSON/XML formatting required by Claude Code; simpler edit formats work better (Aider's diff-based approach)
- **Recommended alternative**: Aider preferred for local models; uses repo maps and simpler edit formats for 7B compatibility
- **Context window tuning** — 32K+ needed for agentic workflows; default 4K-8K insufficient

## Entities Mentioned

- [[wiki/entities/ollama]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/qwen3]]

## Concepts Covered

- [[wiki/concepts/local-ai-inference]]
- [[wiki/concepts/api-integration]]
- [[wiki/concepts/litellm]]
- [[wiki/concepts/containerization]]
- [[wiki/concepts/model-quantization]]

## Setup Notes

- **LiteLLM Docker command** — `docker run -d --name litellm-prox-local -v /path/to/config.yaml:/app/config.yaml -p 4000:4000 ghcr.io/berriai/litellm:main-latest`
- **CLAUDE.md environment** — Point `ANTHROPIC_BASE_URL = "http://localhost:4000"` and set API key
- **Troubleshooting** — Check Docker logs, verify host access on Ollama, test proxy with curl

## Personal Notes

Practical guide for Windows-based local model setup. The containerization approach is cleaner than native installation. Honest assessment of 7B limitations for agentic workflows; Aider recommended as pragmatic alternative for constrained models.
