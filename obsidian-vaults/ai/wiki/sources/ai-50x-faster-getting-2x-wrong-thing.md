---
title: "Your AI Is 50x Faster. You're Getting 2x. You're Fixing the Wrong Thing."
type: source
domain: ai
tags:
  - agent-infrastructure
  - future-of-work
  - tool-calls
  - agentic-primitives
  - bitter-lesson
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Your AI Is 50x Faster. You're Getting 2x. You're Fixing the Wrong Thing.md]]"
---

# Your AI Is 50x Faster. You're Getting 2x. You're Fixing the Wrong Thing.

**Authors**: Nate B Jones
**Date**: 2026-04
**Type**: video-transcript

## Summary

Nate B Jones argues that the reason developers get only 2-3x productivity gains despite AI being 50x faster is that the bottleneck has shifted from model inference to the human-designed infrastructure surrounding it — file systems, APIs, databases, compilers, and ERPs all designed for human speed. He outlines three layers of the coming 'agentic infrastructure rebuild' (faster existing tools, agent-native primitives replacing human interfaces, bitter lesson applied to the full stack) and defines four future human roles in an agent-native economy. This is a systems-level companion to the Amazon dark code article by the same author.

## Key Takeaways

- In agentic loops, the majority of wall-clock time is tool calls — not inference; the trillion-dollar compute investment is bottlenecked by human-speed APIs
- TypeScript 7 being rewritten in Go for 10x speed; Rust + strict compiler acts as natural verification for AI-written code
- Three rebuild layers: (1) faster existing tools, (2) agent-native primitives (persistent containers, serverside compaction, branchFS, shared KV cache for multi-agent), (3) bitter lesson — general agent-native methods beat human-engineered scaffolding over time
- MCP as a stopgap: 'agents make do with human-friendly APIs wrapped in MCP, but you eat wall-clock time on pagination'
- Tools designed for today's model become drag on tomorrow's model — optimizing existing frameworks is 'structurally incorrect'
- Four future human roles above the loop: (1) tool-using generalist / vibe coder, (2) pipeline engineer (infra/security), (3) business dealer (relationship-driven commerce), (4) adult in the room (judgment, ethics, direction), (5) creative (Steve Jobs chair)
- Amazon's Kira built spec-driven development after December outage — supports the dark code article's prescriptions
- branchFS: copy-on-write filesystem enabling sub-second branch creation for agent iteration

## Entities Mentioned

- [[wiki/entities/nate-b-jones]]
- [[wiki/entities/aaron-levy]]
- [[wiki/entities/lee-robinson]]
- [[wiki/entities/openai]]
- [[wiki/entities/amazon]]
- [[wiki/entities/microsoft]]
- [[wiki/entities/salesforce]]

## Concepts Covered

- [[wiki/concepts/agent-native-infrastructure]]
- [[wiki/concepts/tool-call-bottleneck]]
- [[wiki/concepts/human-speed-apis]]
- [[wiki/concepts/agentic-primitives]]
- [[wiki/concepts/branchfs]]
- [[wiki/concepts/shared-kv-cache]]
- [[wiki/concepts/bitter-lesson]]
- [[wiki/concepts/future-of-work]]
- [[wiki/concepts/mcp-limitations]]
- [[wiki/concepts/spec-driven-development]]

## Notable Quotes

> "We spent a trillion dollars on these agents. We made the sand think. Now we're bottlenecking them on tool calls that were designed for humans."

> "The only durable response is to start to invest in agent-native scaffolding so fast it does not matter how quick and smart the agents get."

> "This is a promotion to the hardest and most valuable job in computing."

## Cross-Connections

Directly extends [[wiki/sources/amazon-fired-engineers-ai-dark-code]] by Nate B Jones — same author, complementary analysis. The agent-native primitives discussion (persistent containers, shared KV cache) connects to OpenAI Codex's background execution model described in [[wiki/sources/codex-and-claude-side-by-side]]. The MCP critique ('makes do, but you eat wall-clock time') connects to the framework comparison's note on MCP support quality in [[wiki/sources/comparing-6-python-ai-agent-frameworks]]. The four future roles framework is the human-side counterpart to the agentic infrastructure discussion. The shared KV cache for multi-agent connects to the Coordinator Mode in [[wiki/sources/claude-code-source-leaked-worth-learning]].
