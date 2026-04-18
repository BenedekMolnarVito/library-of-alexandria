---
title: "Andrej Karpathy Killed RAG. Or Did He? The LLM Wiki Pattern"
type: source
domain: ai
tags:
  - llm-wiki
  - rag
  - knowledge-compounding
  - personal-knowledge-management
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Andrej Karpathy Killed RAG. Or Did He The LLM Wiki Pattern.md]]"
---

# Andrej Karpathy Killed RAG. Or Did He? The LLM Wiki Pattern

**Authors**: Mandar Karhade, MD PhD
**Date**: 2026-04
**Type**: article

## Summary

A detailed analysis of Andrej Karpathy's 'LLM Wiki' GitHub Gist (5,000 stars in 48 hours), which describes a pattern where the LLM builds and maintains a persistent, compounding markdown knowledge base instead of re-retrieving documents at query time as in traditional RAG. The article explains the three-layer architecture (raw sources, wiki, schema), three core operations (ingest/query/lint), and frames the pattern as solving Vannevar Bush's 80-year-old maintenance problem. It critically examines community reactions, enterprise scalability gaps (no RBAC, no ACID, no audit trails), and a provocative future direction: using the wiki as synthetic training data to fine-tune a personal model.

## Key Takeaways

- LLM Wiki architecture: three layers — raw sources (immutable), wiki (LLM-maintained structured markdown with cross-references), schema (CLAUDE.md config directing agent behavior).
- Three operations: Ingest (read source → write source page → update entity/concept pages → update index), Query (search wiki → synthesize from pre-compiled knowledge → optionally save as new wiki page), Lint (health check for orphans, contradictions, missing pages).
- The key difference from RAG: RAG is a retrieval operation at query time (stateless, every query is day one); LLM Wiki is a compilation operation at ingest time (knowledge pre-compiled, cross-referenced before queries).
- The analogy: RAG is a search engine; LLM Wiki is an encyclopedia.
- Karpathy explicitly references Vannevar Bush's 1945 Memex — the problem Bush couldn't solve was maintenance. LLMs don't get bored, don't forget to update indexes, don't skip cross-referencing on Friday afternoons.
- Current scale: works best at ~100 articles / 400K words. Enterprise gaps are real: no RBAC, no ACID guarantees, no tamper-proof audit trail, no concurrency control for simultaneous agents.
- Fine-tuning endgame: the wiki can generate synthetic training data → fine-tune a model → knowledge moves from context window to model weights → your wiki becomes a personal model.
- Community split: enthusiasts see it as the future of knowledge work; skeptics say it's a renamed cache layer; pragmatists say RAG and LLM Wiki are tools for different scales.

## Entities Mentioned

- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/mandar-karhade]]
- [[wiki/entities/vannevar-bush]]
- [[wiki/entities/openai]]
- [[wiki/entities/obsidian]]

## Concepts Covered

- [[wiki/concepts/llm-wiki]]
- [[wiki/concepts/rag]]
- [[wiki/concepts/knowledge-compounding]]
- [[wiki/concepts/ingest-query-lint]]
- [[wiki/concepts/chunking-problem]]
- [[wiki/concepts/vannevar-bush-memex]]
- [[wiki/concepts/personal-knowledge-management]]
- [[wiki/concepts/fine-tuning]]
- [[wiki/concepts/knowledge-graphs]]

## Notable Quotes

> "The metaphor he uses is perfect: Obsidian is the IDE. The LLM is the programmer. The wiki is the codebase."

> "Karpathy didn't just build a better RAG. He solved Bush's 80-year-old maintenance problem."

> "RAG is the search engine. LLM Wiki is the encyclopedia. Both useful. Fundamentally different architectures solving fundamentally different problems."

> "Most RAG implementations are over-engineered for what users actually need, and under-engineered for what users actually want. Users don't want retrieval. They want knowledge."

> "Karpathy didn't release software. He released a pattern."

## Cross-Connections

This article directly inspired the Library of Alexandria project — this very wiki is a live implementation of the LLM Wiki pattern described here. The three-layer architecture maps precisely to this project's raw/wiki/schema structure. Connects to [[wiki/sources/building-claude-code-boris-cherny]] (Claude Code as the agent executing the wiki pattern); to [[wiki/sources/300-dollars-auto-research-karpathy-loop]] (same Karpathy, different paradigm shift); the fine-tuning endgame connects to discussions of AI self-improvement in [[wiki/sources/300-dollars-auto-research-karpathy-loop]].
