---
title: "Wall Street Just Bet $285 Billion on AI Agents. The Best One Barely Works."
type: source
domain: ai
tags:
  - outcome-agents
  - agent-evaluation
  - persistent-memory
  - saas-disruption
  - computer-use
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Wall Street Just Bet $285 Billion on AI Agents. The Best One Barely Works.md]]"
---

# Wall Street Just Bet $285 Billion on AI Agents. The Best One Barely Works.

**Authors**: Nate B Jones (AI News & Strategy Daily)
**Date**: 2026-04
**Type**: video-transcript

## Summary

Anthropic's Claude Co-Work triggered a $285B+ SaaS stock selloff when it demonstrated computer-use AI agents doing real work autonomously. Yet even Co-Work scores only approximately 1.25 out of 3 on the author's three evaluation criteria: persistent memory, editable artifact production, and compounding context over time. The disconnect — massive market reaction to a product with fundamental architectural gaps — is the article's central observation.

The author reviews four lesser-known "outcome agents" (Lindy, Sauna/Wordware, Google Opal, Obvious) against the same three-criterion framework. None fully satisfy all three, for different reasons: Lindy has good persistent memory but opaque artifacts; Sauna/Wordware has the strongest conceptual memory architecture ("memory as substrate, not feature") but is early and unproven; Google Opal is free and community-driven but won't scale; Obvious is too new to evaluate. The author closes with a three-layer architecture for building one's own competent outcome agent: knowledge store (Postgres + MCP connections), agent recipes (pre-wired workflows), and scheduling loop (compounding over time).

## Key Takeaways

- Co-Work caused a $285B+ SaaS selloff — but still scored only ~1.25/3 on the evaluation framework; cannot function if the laptop is closed
- Three evaluation criteria: (1) Does the agent have persistent memory? (2) Does it produce inspectable, editable artifacts? (3) Does context compound over time?
- Code agents worked first because code is a verifiable domain — you can objectively confirm if it runs
- Lindy (~2.4/5 Trustpilot): good persistent memory, opaque artifacts, credits burn unpredictably — targets executives but hides the editing surface
- Sauna/Wordware: strongest conceptual memory architecture ("memory as substrate, not feature"); very early, unproven in production
- Google Opal: free, Gemini 3 Flash-powered, good community remix energy; memory is "spreadsheet-simple" which won't scale
- Obvious: most ambitious (SQL workbooks, live charts, cross-artifact relationships) but too new to evaluate
- Three-layer architecture: knowledge store + agent recipes + scheduling loop

## Entities Mentioned

- [[wiki/entities/nate-b-jones]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-co-work]]
- [[wiki/entities/microsoft]]
- [[wiki/entities/lindy]]
- [[wiki/entities/flo-crello]]
- [[wiki/entities/sauna-wordware]]
- [[wiki/entities/philip-kazera]]
- [[wiki/entities/google]]
- [[wiki/entities/google-opal]]
- [[wiki/entities/obvious]]
- [[wiki/entities/openai]]

## Concepts Covered

- [[wiki/concepts/outcome-agents]]
- [[wiki/concepts/persistent-memory]]
- [[wiki/concepts/artifact-production]]
- [[wiki/concepts/context-compounding]]
- [[wiki/concepts/verifiable-domains]]
- [[wiki/concepts/agent-evaluation]]
- [[wiki/concepts/computer-use]]
- [[wiki/concepts/saas-disruption]]
- [[wiki/concepts/agent-architecture]]

## Notable Quotes

> "The agent that caused all of this chaos is still in research preview, is still being very cautiously rolled out, and still frankly has problems that we would consider laughable for any kind of dependable software."

> "Memory needs to be built into the architecture. It can't just be a bolt-on feature."

> "If you want your agent to be able to do useful work, then you need the agent to produce outcomes you can edit on a surface that is easily visible."

## Cross-Connections

The three evaluation criteria (memory / artifacts / compounding context) are the product-side articulation of the same architectural principles analyzed technically in [[wiki/sources/markdown-file-beats-vector-database]]. The SaaS disruption narrative directly connects to [[wiki/sources/five-safe-places-to-build-in-ai]] — the $285B selloff is the market pricing the middleware trap. Sauna's "memory as substrate" thesis is the highest-fidelity product implementation of the SOUL.md/heartbeat.md patterns from [[wiki/sources/real-problem-ai-agents-clarity-of-intent]]. The verifiable domain insight (code agents worked first because code can be run and checked) connects to the AutoCover test generation quality argument in [[wiki/sources/uber-agentic-engineering-shift]].
