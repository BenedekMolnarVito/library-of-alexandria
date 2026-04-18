---
title: "Andrej Karpathy Just 10x'd Everyone's Claude Code"
type: source
domain: ai
tags:
  - karpathy
  - llm-wiki
  - claude-code
  - knowledge-base
  - obsidian
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Andrej Karpathy Just 10x'd Everyone's Claude Code.md]]"
---

# Andrej Karpathy Just 10x'd Everyone's Claude Code

**Authors**: Nate Herk | AI Automation
**Date**: 2026-04
**Type**: video-transcript

## Summary

Nate Herk demonstrates how Andrej Karpathy's LLM wiki pattern can be applied using Claude Code and Obsidian to turn raw source documents (YouTube transcripts, articles, PDFs) into a self-organizing, compounding knowledge base. The system replaces ephemeral AI chat with a persistent, indexed wiki of markdown files that gets smarter with every source added. One power user reduced token usage by 95% by consolidating 383 scattered files into a compact wiki. This video is one of several that popularized Karpathy's original idea, and is directly ancestral to the Library of Alexandria project. The key insight is that traditional RAG re-derives knowledge from scratch on every query, while the LLM wiki pre-compiles and compounds it.

## Key Takeaways

- Karpathy's core insight: instead of querying raw docs every time (traditional RAG), let the LLM incrementally build and maintain a persistent wiki — knowledge compounds rather than resets
- Architecture: raw/ folder (immutable source documents) + wiki/ folder (LLM-generated, with index.md and log.md) + CLAUDE.md schema — no vector database needed
- One source ingested = 10–15 wiki pages updated in a single pass, with cross-links automatically built and contradictions flagged
- The Obsidian graph view is primarily aesthetic ('node porn') — the real value is efficient token-compressed querying, not visual navigation
- Token efficiency: 383 files + 100 meeting transcripts → compact wiki → 95% token reduction when querying
- Karpathy left the original prompt 'vague' intentionally — Claude Code is meant to interpret and customize the schema for the specific project domain
- The pattern is domain-agnostic: works for YouTube knowledge systems, personal second brain, business wikis, research deep dives

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/obsidian]]

## Concepts Covered

- [[wiki/concepts/llm-wiki]]
- [[wiki/concepts/knowledge-base]]
- [[wiki/concepts/compounding-knowledge]]
- [[wiki/concepts/context-efficiency]]
- [[wiki/concepts/second-brain]]
- [[wiki/concepts/obsidian-rag]]
- [[wiki/concepts/index-driven-retrieval]]

## Notable Quotes

> "Normal AI chats are ephemeral, meaning the knowledge disappears after the conversation. But this method, using Karpathy's LLM wiki, makes knowledge compound like interest in a bank."

> "One X user turned 383 scattered files and over 100 meeting transcripts into a compact wiki and dropped token usage by 95% when querying with Claude."

## Cross-Connections

This video covers nearly identical ground to [[wiki/sources/claude-code-karpathy-obsidian-new-meta]] (Jack Roberts) — both are tutorial implementations of Karpathy's LLM wiki idea. The LLM wiki pattern is the direct conceptual ancestor of this Library of Alexandria project. Connects to Claude Code's memory architecture in the source leak ([[wiki/sources/claude-code-source-leaked-worth-learning]]) — Karpathy's approach converges independently on the same design. For the self-evolving memory extension, see [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]].
