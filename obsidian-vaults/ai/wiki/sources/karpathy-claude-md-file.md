---
title: "What Is Andrej Karpathy's CLAUDE.md File?"
type: source
domain: ai
tags:
  - karpathy
  - claude-md
  - claude-code
  - agent-instructions
  - workflow
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/What Is Andrej Karpathy's CLAUDE.md File.md]]"
---

# What Is Andrej Karpathy's CLAUDE.md File?

**Authors**: Ai Studio
**Date**: 2026-04
**Type**: article

## Summary

This article explains how Andrej Karpathy shifted from 80% manual to 80% agent-driven coding in late 2025, and how his CLAUDE.md file encodes the specific failure modes he identified in LLM coding agents. Developer Forrest Chang distilled Karpathy's observations into a 60-line downloadable CLAUDE.md with four principles: surface uncertainty, write minimum code, touch only what you must, and define success criteria. The file got 3,500+ GitHub stars and spawned VS Code/Cursor extensions. CLAUDE.md is the meta-document that governs all Karpathy-inspired AI toolchains — the LLM wiki, autoresearch, and code memory systems all use CLAUDE.md/AGENTS.md variants.

## Key Takeaways

- Karpathy called the shift to 80% agent-driven coding 'the biggest change to his workflow in roughly two decades' — happened in December 2025
- CLAUDE.md loads automatically at every Claude Code session — it's a standing instruction document placed in the project root
- Karpathy's identified failure modes: silent wrong assumptions, not flagging confusion, overcomplicating solutions, touching adjacent code, not cleaning up dead code
- Forrest Chang's 4 principles from Karpathy observations: (1) ask when uncertain, surface tradeoffs; (2) minimum code, nothing speculative; (3) touch only what was asked; (4) define done, loop until verified
- Repository: andrej-karpathy-skills — 3,500+ stars, VS Code extension, Cursor extension
- One-command install: `curl -o CLAUDE.md [url]`
- Context window constraint: frontier models handle ~150-200 instructions; Claude Code's own prompt uses ~50 of those — shorter CLAUDE.md is better
- Karpathy admitted even with CLAUDE.md the problems don't fully go away, and he hadn't figured out a good way to keep it updated

## Entities Mentioned

- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/forrest-chang]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/anthropic]]

## Concepts Covered

- [[wiki/concepts/claude-md]]
- [[wiki/concepts/ai-coding-configuration]]
- [[wiki/concepts/llm-failure-modes]]
- [[wiki/concepts/agent-instructions]]
- [[wiki/concepts/context-window-management]]
- [[wiki/concepts/coding-agent-workflow]]

## Notable Quotes

> "Not a gradual drift. A phase shift."

> "CLAUDE.md is a way of encoding the corrections you'd make anyway. Instead of catching the same class of mistake on every session, you write it once and it applies automatically."

## Cross-Connections

CLAUDE.md is the meta-document that governs the entire Karpathy-inspired toolchain. The LLM wiki ([[wiki/sources/karpathy-10x-claude-code-llm-wiki]]), autoresearch ([[wiki/sources/karpathy-autoresearch-universal-skill]]), and code memory systems ([[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]) all use CLAUDE.md/AGENTS.md variants. The failure modes Karpathy identified (overcomplication, adjacent code touching) directly motivate the Caveman plugin ([[wiki/sources/cut-claude-code-output-tokens-75-percent]]) and the dark code discussion ([[wiki/sources/amazon-fired-engineers-ai-dark-code]]). The discovery in [[wiki/sources/claude-code-source-leaked-worth-learning]] that CLAUDE.md is reinserted on every turn change gives this file even more weight than Karpathy realized.
