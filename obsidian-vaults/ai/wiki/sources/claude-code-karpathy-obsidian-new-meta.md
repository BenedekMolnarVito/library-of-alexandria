---
title: "Claude Code + Karpathy's Obsidian = New Meta"
type: source
domain: ai
tags:
  - karpathy
  - llm-wiki
  - claude-code
  - obsidian
  - memory-systems
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Claude Code + Karpathy's Obsidian = New Meta.md]]"
---

# Claude Code + Karpathy's Obsidian = New Meta

**Authors**: Jack Roberts
**Date**: 2026-04
**Type**: video-transcript

## Summary

Jack Roberts presents a practical implementation guide for Andrej Karpathy's LLM wiki / Obsidian memory system, while critically noting the '90% of coverage is node porn' problem — most videos show the visual graph but ignore significant limitations. He explains how the system solves Claude's core amnesia/context-loss problem by adding a fourth memory layer (persistent wiki), demonstrates setup with Claude Code and Obsidian Web Clipper, and discusses a key limitation he claims no one else is talking about (context-length degradation in long sessions and 1–10% hallucination rate). This source is notable for its critical stance — while most LLM wiki content is promotional, Roberts explicitly flags the failure modes that make the system dangerous if treated as a source of truth.

## Key Takeaways

- The Karpathy LLM wiki adds a 'fourth memory system' to Claude Code: (1) in-context window, (2) system prompt, (3) CLAUDE.md, (4) persistent Obsidian wiki — addressing the core amnesia problem
- Key difference from traditional RAG: RAG retrieves the same chunks fresh each query; the LLM wiki compounds — one new source updates 10–15 wiki pages, and the updated knowledge is available in every future query
- Three layers, no database: raw/ (sources you feed), wiki/ (Claude writes), schema file (CLAUDE.md rules) — 'you create it, it maintains, the wiki compounds'
- Critical limitation acknowledged: the system has 'several huge limitations' that 90% of coverage ignores — context loss and hallucination still occur (1–10% error rate), especially in long sessions; skeptical verification is needed
- Obsidian Web Clipper workflow: browser extension clips articles directly to raw/ folder; Claude Code ingests and creates ~23 wiki pages from a single long article
- Linting (Karpathy's term): periodic maintenance to find contradictions, orphan pages, stale claims — the compounding value degrades without it
- Practical use cases demonstrated: personal life OS, YouTube knowledge base, business wiki, book companion

## Entities Mentioned

- [[wiki/entities/jack-roberts]]
- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/obsidian]]
- [[wiki/entities/obsidian-web-clipper]]

## Concepts Covered

- [[wiki/concepts/llm-wiki]]
- [[wiki/concepts/compounding-knowledge]]
- [[wiki/concepts/context-loss]]
- [[wiki/concepts/memory-systems]]
- [[wiki/concepts/obsidian-rag]]
- [[wiki/concepts/skeptical-memory]]
- [[wiki/concepts/knowledge-linting]]

## Notable Quotes

> "90% of the coverage I've seen on this I would describe realistically as node porn."

> "The Karpathy LLM wiki makes knowledge compound like interest in a bank — one source updates 15 files in a single pass."

> "Claude has amnesia — it can be confidently incorrect 1-10% of the time, and we don't know when."

## Cross-Connections

Closely parallel to [[wiki/sources/karpathy-10x-claude-code-llm-wiki]] (Nate Herk) — both implement the same pattern, targeting the same audience, at roughly the same time. Jack Roberts adds a critical perspective on the limitations that Nate Herk's video omits. The 'skeptical memory' concern Roberts raises maps directly to the `autoDream` and verification systems in the Claude Code source leak ([[wiki/sources/claude-code-source-leaked-worth-learning]]). This Library of Alexandria project is a direct implementation of the architecture described in both videos. The knowledge-linting operation described here is implemented as the Lint workflow in AGENTS.md.
