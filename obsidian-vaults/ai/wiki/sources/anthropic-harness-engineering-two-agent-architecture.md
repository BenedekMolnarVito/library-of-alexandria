---
title: "Anthropic's Harness Engineering: Two Agents, One Feature List, Zero Context Overflow"
type: source
domain: ai
tags:
  - anthropic
  - claude-code
  - harness-engineering
  - context-management
  - agentic-coding
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Anthropic’s Harness Engineering Two Agents, One Feature List, Zero Context Overflow.md]]"
---

# Anthropic's Harness Engineering: Two Agents, One Feature List, Zero Context Overflow

**Authors**: Rick Hightower
**Date**: 2026-03
**Type**: article

## Summary

A detailed technical analysis of Anthropic's harness engineering patterns for long-running agentic coding tasks, based on Anthropic's published best practices and a thread by Rohit. The core claim: harness design drives agent performance more than model selection. The solution is a two-agent architecture (Initializer + Coding Agent) with a JSON feature list as cognitive anchor and disciplined git checkpointing — designed to prevent the two dominant failure modes: 'build everything at once' and 'premature completion.' This article is significant because it names and systematizes the engineering patterns that Claude Code implicitly implements, later confirmed by the source leak analysis.

## Key Takeaways

- The context window boundary is the #1 engineering challenge for long-running agentic coding — not model intelligence. At 128K–200K tokens, a serious coding session (codebase reads + errors + conversation) can exhaust the window before significant work is done
- Two failure patterns: (1) Building everything at once → combinatorial debugging explosion when something breaks; (2) Premature completion → happy path only, no edge cases, fails in production
- Two-agent split: Initializer (broad/shallow context: reads full spec + codebase, generates JSON feature list + skeleton tests + startup script) and Coding Agent (narrow/deep context: one feature at a time, anchored to feature list)
- JSON feature list over markdown: machine-readable, unambiguous status fields (complete/in_progress/pending), explicit requirements + tests + files per feature — prevents both failure modes simultaneously
- Git discipline: commit after each passing feature; subagents run `git stash` on startup to preserve progress; enables recovery from context collapse without losing work
- Startup script re-establishes context cheaply on session resume: reads feature list, identifies current position, loads only relevant files
- Test-first anchoring: skeleton tests written by Initializer define 'done' before coding begins — prevents premature completion

## Entities Mentioned

- [[wiki/entities/rick-hightower]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude]]
- [[wiki/entities/rohit]]
- [[wiki/entities/claude-code]]

## Concepts Covered

- [[wiki/concepts/context-window-management]]
- [[wiki/concepts/harness-engineering]]
- [[wiki/concepts/two-agent-architecture]]
- [[wiki/concepts/feature-list-as-anchor]]
- [[wiki/concepts/agentic-coding]]
- [[wiki/concepts/context-collapse]]
- [[wiki/concepts/git-checkpointing]]
- [[wiki/concepts/test-first-agents]]

## Notable Quotes

> "Harness design drives agent performance more than model selection."

> "The context window boundary is the single hardest problem in agentic coding today."

> "Anthropic identified this as the core engineering challenge. Not as a model limitation to be solved with bigger windows, but as an environmental constraint to be managed with better harness design."

## Cross-Connections

Directly describes the architectural patterns underneath Claude Code — confirmed and elaborated by the Claude Code source leak analysis ([[wiki/sources/claude-code-source-leaked-worth-learning]]). The JSON feature list pattern is isomorphic to the three-layer memory system in the Claude Code leak. The Initializer/Coding Agent split mirrors the Coordinator/Worker multi-agent pattern in the leaked source. Connects to DHH's agent-first workflow ([[wiki/sources/dhh-new-way-writing-code-agent-first]]) where he describes context management as the key bottleneck. The agent framework comparison ([[wiki/sources/comparing-6-python-ai-agent-frameworks]]) provides a broader view of how different frameworks handle context constraints.
