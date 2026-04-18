---
title: "The Most Important Employee at a Japanese Firm Was a Markdown File"
type: source
domain: ai
tags:
  - claude-md
  - context-engineering
  - agentic-workflows
  - solo-founder
  - operational-translation
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/The Most Important Employee at a Japanese Firm Was a Markdown File.md]]"
---

# The Most Important Employee at a Japanese Firm Was a Markdown File

**Authors**: Kaitai Dong
**Date**: 2026-04
**Type**: article

## Summary

A Japanese tax accountant with no programming background runs a solo firm serving 60 clients, leaving work at 5pm, by using a single CLAUDE.md file to define an AI agent's role, constraints, tool access, and security rules. The article dissects the four-block CLAUDE.md structure: (1) role definition, (2) hard limits ("AI must never make tax judgments"), (3) tool usage rules specifying when and how to use freee, Calendar, Notion, and Gmail, and (4) security design with risk principles.

The setup follows a four-step process: define the workspace folder structure first (output/, reference/, clients/, tools/, work-log/), then write CLAUDE.md, then configure MCP connections, then create Skills/commands. Multi-step workflows are compressed into single-word triggers: "Good morning" generates the daily schedule; "Accounting" triggers batch processing for all 60 clients. The nightly runtime at 21:00 retrieves transactions, normalizes descriptions via keyword dictionary, uses LLM as fallback classifier, and holds low-confidence cases for human review.

The article frames "operational translation" — decomposing real work into steps, exceptions, handoffs, and review points — as the scarce skill, not programming. CLAUDE.md is not a prompt file; it is a compressed org chart, playbook, and control policy simultaneously.

## Key Takeaways

- One-person firm, 60 clients, leaves at 5pm — enabled entirely by a well-written CLAUDE.md, not custom code
- CLAUDE.md structure: (1) AI role definition, (2) hard boundary rules, (3) tool usage rules per integration, (4) security design with risk principles
- Workspace structure is prerequisite: define folder hierarchy first before writing any prompts
- Skills/commands compress multi-step workflows: "Good morning" → daily schedule; "Accounting" → batch processing for all 60 clients
- Nightly runtime: retrieve transactions → normalize descriptions → apply keyword dictionary → LLM fallback classifier → hold low-confidence cases for human review
- The scarce skill is "operational translation" — decomposing real work into steps, exceptions, handoffs, and review points
- CLAUDE.md is not a prompt file; it is a compressed org chart, playbook, and control policy

## Entities Mentioned

- [[wiki/entities/kaitai-dong]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/mcp]]
- [[wiki/entities/freee]]
- [[wiki/entities/notion]]

## Concepts Covered

- [[wiki/concepts/context-engineering]]
- [[wiki/concepts/claude-md]]
- [[wiki/concepts/agentic-workflows]]
- [[wiki/concepts/operational-translation]]
- [[wiki/concepts/human-in-the-loop]]
- [[wiki/concepts/domain-expert-as-system-designer]]
- [[wiki/concepts/model-context-protocol]]
- [[wiki/concepts/skills-commands]]

## Notable Quotes

> "The most important employee in the office was not a person. It was a markdown file."

> "Increasingly, the edge belongs to whoever can decompose real work into steps, exceptions, handoffs, and review points."

> "Rules first, model second, and human last."

> "The hard part is learning to write your own work down so clearly that another intelligence — human or machine — can reliably carry part of it."

## Cross-Connections

Directly illustrates the CLAUDE.md memory pattern analyzed architecturally in [[wiki/sources/markdown-file-beats-vector-database]]. Demonstrates the "tacit knowledge translation" problem raised in [[wiki/sources/real-problem-ai-agents-clarity-of-intent]] — this accountant successfully externalized tacit expert knowledge. The "selectively autonomous" pipeline design (rules → model → human) is architecturally identical to the workflow patterns in [[wiki/sources/death-of-traditional-etl-ai-agents]]. The security boundary ("AI must never make tax judgments") directly instantiates the liability governance moat discussed in [[wiki/sources/five-safe-places-to-build-in-ai]].
