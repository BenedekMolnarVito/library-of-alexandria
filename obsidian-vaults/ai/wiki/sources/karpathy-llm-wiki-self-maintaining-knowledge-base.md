---
title: "I used Karpathy's LLM Wiki to build a knowledge base that maintains itself with AI"
type: source
domain: ai
tags:
  - karpathy
  - llm-wiki
  - obsidian
  - knowledge-management
  - open-source
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/I used Karpathy’s LLM Wiki to build a knowledge base that maintains itself with AI.md]]"
---

# I used Karpathy's LLM Wiki to build a knowledge base that maintains itself with AI

**Authors**: Balu Kosuri
**Date**: 2026-04
**Type**: article

## Summary

Balu Kosuri built a working implementation of Karpathy's LLM wiki pattern using Cursor and Obsidian in three prompts, then open-sourced it as a ready-to-clone repository. The article explains the three-layer architecture (raw/immutable, wiki/LLM-owned, CLAUDE.md/schema), three operations (ingest, query, lint), and provides a detailed technical writer use case showing how the system evolves over a working week. Kosuri frames the core insight with the Vannevar Bush/Memex lineage — the idea of associative trails between documents as the natural shape of human knowledge — and argues that AI finally makes this vision practical by automating the bookkeeping that human wikis always fail on.

## Key Takeaways

- Built a complete LLM wiki system in 3 Cursor prompts: 'What is this?', 'Make a plan and create', 'Set up Obsidian'
- Three layers: raw/ (user's immutable sources), wiki/ (AI owns and writes), CLAUDE.md (rules for the AI)
- Ingest touches 10–15 wiki pages per source; query answers are saved back as analysis pages; lint finds contradictions, orphans, stale claims
- No vector databases or embeddings needed — index.md works as a map for hundreds of pages
- Key insight: 'The hard part of a knowledge base was never the reading or the thinking. It was always the bookkeeping. Bookkeeping is exactly what AI is best at.'
- Repo includes pre-configured Obsidian vault (graph view colors, hotkeys, sidebar)
- Open-source repo: github.com/balukosuri/llm-wiki-karpathy
- Vannevar Bush's 1945 Memex vision — 'associative trails' between documents — as historical antecedent

## Entities Mentioned

- [[wiki/entities/balu-kosuri]]
- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/vannevar-bush]]
- [[wiki/entities/cursor]]
- [[wiki/entities/obsidian]]
- [[wiki/entities/claude]]

## Concepts Covered

- [[wiki/concepts/llm-knowledge-base]]
- [[wiki/concepts/personal-knowledge-management]]
- [[wiki/concepts/obsidian-vault]]
- [[wiki/concepts/rag-alternative]]
- [[wiki/concepts/knowledge-graph]]
- [[wiki/concepts/second-brain]]
- [[wiki/concepts/memex]]
- [[wiki/concepts/ai-maintenance]]

## Notable Quotes

> "The hard part of a knowledge base was never the reading or the thinking. It was always the bookkeeping. And bookkeeping is exactly what AI is best at."

> "Don't write wiki pages yourself. Resist the temptation. Your job is to find good sources and ask good questions. The AI's job is the summarizing, cross-referencing, filing, and bookkeeping."

## Cross-Connections

Directly implements the same pattern described in [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]] and is the technical writer's version of what [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]] built for codebases. The no-vector-database approach contrasts sharply with traditional RAG and directly responds to the RAG critique in [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]. The Vannevar Bush/Memex connection provides deep historical context for the second-brain movement. Also by [[wiki/entities/balu-kosuri]] — see [[wiki/sources/karpathy-autoresearch-universal-skill]] for a complementary implementation of Karpathy-inspired ideas.
