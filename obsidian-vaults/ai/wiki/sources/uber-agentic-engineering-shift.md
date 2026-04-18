---
title: "Uber: Leading Engineering Through an Agentic Shift — The Pragmatic Summit"
type: source
domain: ai
tags:
  - uber
  - background-agents
  - developer-productivity
  - enterprise-ai
  - code-automation
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Uber Leading engineering through an agentic shift - The Pragmatic Summit.md]]"
---

# Uber: Leading Engineering Through an Agentic Shift — The Pragmatic Summit

**Authors**: The Pragmatic Engineer (Ty Smith and Anshu Chada, Uber Dev Platform)
**Date**: 2026-03
**Type**: video-transcript

## Summary

Uber's developer platform team describes their production-scale agentic engineering infrastructure deployed across a monorepo with thousands of engineers. The central shift is from "pair programming" (GitHub Copilot, IDE-level, 10–15% diff velocity gain) to "peer programming" (async background agents that developers direct as tech leads). The key products built internally are: Minion (background agent platform running Claude on Uber's CI infrastructure), AutoCover (5,000 AI-generated unit tests merged per month at 3x quality vs. generic agents), AutoMigrate/Shepherd (campaign management for large-scale code migrations), and a central MCP gateway with auth and telemetry.

70% of developer workloads submitted to the agentic system are toil tasks (migrations, cleanup, docs), which have well-defined start and end states that enable higher accuracy and create a virtuous adoption cycle. AI costs have increased 6x since 2024, and converting agent activity metrics to business outcomes remains an unsolved measurement problem — the current approach is instrumenting feature pipeline time-to-production.

## Key Takeaways

- Shift from pair programming (IDE inline suggestions) to peer programming (async background agents) — developers act as tech leads directing multiple simultaneous agents
- Minion: background agent platform; runs Claude on Uber's CI infrastructure, not vendor cloud; integrated with Slack, GitHub PRs, CLI; includes prompt quality scorer and per-monorepo defaults
- 70% of agentic workloads are toil tasks — higher accuracy on well-defined tasks creates a virtuous adoption cycle
- AutoCover: custom LangChain agent generating ~5,000 unit tests/month merged; 3x quality vs. generic agents; critic engine + independent test validator
- Shepherd: large-scale migration campaign management — generates PRs, refreshes on cadence, handles notifications, integrates with Code Inbox
- Central MCP gateway: tiger team built a proxy for internal/external MCPs with auth, telemetry, and sandbox for developer discovery
- Cost challenge: AI costs 6x higher since 2024; CFO demands business outcome metrics beyond activity counts
- Adoption insight: top-down mandates had modest impact; peer-to-peer win-sharing by engineer promoters drove the real adoption spike

## Entities Mentioned

- [[wiki/entities/uber]]
- [[wiki/entities/ty-smith]]
- [[wiki/entities/anshu-chada]]
- [[wiki/entities/the-pragmatic-engineer]]
- [[wiki/entities/michelangelo]]
- [[wiki/entities/claude]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/github-copilot]]
- [[wiki/entities/cursor]]
- [[wiki/entities/langchain]]
- [[wiki/entities/openrewrite]]

## Concepts Covered

- [[wiki/concepts/background-agents]]
- [[wiki/concepts/developer-productivity]]
- [[wiki/concepts/agentic-engineering]]
- [[wiki/concepts/model-context-protocol]]
- [[wiki/concepts/code-review-automation]]
- [[wiki/concepts/test-generation]]
- [[wiki/concepts/large-scale-migrations]]
- [[wiki/concepts/toil-automation]]
- [[wiki/concepts/multi-agent-orchestration]]
- [[wiki/concepts/ai-cost-management]]

## Notable Quotes

> "When we push some of the boring stuff to it — upgrades, migrations, bug fixes — not only does it result in much higher satisfaction from our engineers, they're able to push our product and create features for end users in ways we didn't even think was possible."

> "The tech we're building will likely be replaced with something better in the industry. It's really important for us to not be married to the tech that we're building."

## Cross-Connections

Uber's Minion platform is a real-world, at-scale implementation of the "peer programming" / background agent model discussed abstractly in [[wiki/sources/multi-agent-architecture-patterns]]. The AutoCover test generation and 3x quality claim connects to verifiability as the reason coding agents succeeded first — a theme in [[wiki/sources/wall-street-285b-ai-agents-review]]. The 6x cost increase is the enterprise-scale version of the inference cost concerns in [[wiki/sources/step-3-5-flash-196b-open-source-model]] and [[wiki/sources/markdown-file-beats-vector-database]]. The 70% toil automation figure is a concrete data point for the role-elevation argument in [[wiki/sources/death-of-traditional-etl-ai-agents]].
