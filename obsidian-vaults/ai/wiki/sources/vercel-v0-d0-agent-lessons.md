---
title: "Lessons from Building Vercel v0 and the d0 Agent"
type: source
domain: ai
tags:
  - vercel
  - agent-simplification
  - product-engineering
  - coding-agents
  - text-to-sql
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Lessons from building Vercel v0 and the d0 agent - The Pragmatic Summit.md]]"
---

# Lessons from Building Vercel v0 and the d0 Agent

**Authors**: Malte Ubl (speaker); The Pragmatic Engineer (host/channel)
**Date**: 2026-03
**Type**: video-transcript

## Summary

Malte Ubl, CTO of Vercel, recounts lessons from building two AI products: d0 (an internal text-to-SQL Snowflake agent) and v0 (a public UI and app generation product). The central lesson from d0 was that simplicity wins — they deleted a complex multi-tool LangGraph-style agent and replaced it with just two tools, bash and a SQL executor (approximately 50 lines of code), letting the model's emergent behavior do the heavy lifting. The rewrite performed better than the original complex architecture.

v0 evolved from a frontend-engineer tool in 2023 during the GPT-3.5 era to a full-stack app generator as model capability improved, requiring Vercel to treat each model step-change as a product pivot rather than an iteration. The serendipitous unlock in 2023 was including "Tailwind" in the prompt — because Tailwind CSS was densely represented in training data, the model suddenly generated usable UI. The target market also surprised them: backend engineers adopted v0 first because they could fix errors, not the frontend engineers originally intended.

## Key Takeaways

- The first d0 architecture was a traditional tools-in-a-loop agent; the rewrite used only 2 tools (bash + SQL) and performed better
- "All you need is the filesystem and bash" — framing tasks as coding tasks leverages the model's training distribution disproportionately
- More intelligent models allow architectures to simplify: less hard-coding, more reliance on emergent behavior
- v0's initial target market (frontend engineers) was wrong — backend engineers adopted it first because they could fix the errors
- Each major model release constituted a product pivot, not just a model swap — the product had to change to match new capabilities
- Business users can now ship apps without writing code using v0; Malte identifies this as the emerging market
- Malte's personal stack at time of recording: Claude Sonnet 4.6 for fast coding, Codex 5.3 for code review

## Entities Mentioned

- [[wiki/entities/malte-ubl]]
- [[wiki/entities/vercel]]
- [[wiki/entities/v0]]
- [[wiki/entities/d0-dzero]]
- [[wiki/entities/the-pragmatic-engineer]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-sonnet-4-6]]
- [[wiki/entities/codex-5-3]]
- [[wiki/entities/snowflake]]
- [[wiki/entities/tailwind-css]]

## Concepts Covered

- [[wiki/concepts/text-to-sql]]
- [[wiki/concepts/agent-simplification]]
- [[wiki/concepts/emergent-behavior]]
- [[wiki/concepts/coding-agent-pattern]]
- [[wiki/concepts/model-capability-driven-pivots]]
- [[wiki/concepts/filesystem-as-agent-memory]]
- [[wiki/concepts/business-users-shipping-code]]

## Notable Quotes

> "In the world of agents, you have to be humble... just because something was best practice in the summer of 2025 means quite little today."

> "If you can make things look like a coding task even though they're not, you get disproportionately good results."

> "It's not really a pivot... when Anthropic ships Sonnet 3.5 and suddenly the same prompt can build full-stack apps — you cannot keep your product the same because the world is different."

## Cross-Connections

The "simplify down to bash + filesystem" insight directly parallels [[wiki/sources/langchain-deep-agents]] and [[wiki/sources/stop-vibe-coding-4-file-system]] — all point toward minimal, well-described toolsets over complex orchestration. The v0 product-pivoting story connects to [[wiki/sources/product-minded-engineers-ai-native]] about how AI changes the engineer/PM boundary. The rewrite from complexity to simplicity is the same arc described in [[wiki/sources/multi-agent-architecture-patterns]] where patterns transfer but frameworks are disposable.
