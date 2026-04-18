---
title: "Why Andrej Karpathy's \"LLM Wiki\" is the Future of Personal Knowledge"
type: source
domain: ai
tags:
  - karpathy
  - llm-wiki
  - knowledge-management
  - rag-alternative
  - ecosystem
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Why Andrej Karpathy's \"LLM Wiki\" is the Future of Personal Knowledge.md]]"
---

# Why Andrej Karpathy's "LLM Wiki" is the Future of Personal Knowledge

**Authors**: evoailabs
**Date**: 2026-04
**Type**: article

## Summary

A conceptual deep-dive into why the LLM wiki pattern solves a fundamental problem that RAG cannot: knowledge accumulation. RAG searches raw documents on every query with no persistent compilation; the LLM wiki pre-compiles documents into an evolving, interlinked structure that compounds over time. The article covers the three-layer architecture, three core operations, diverse use cases, and surveys five related ecosystem projects (Waykee Cortex, Sage-Wiki, Thinking-MCP, ELF, qmd) that address adjacent knowledge management problems. This is the strongest theoretical framing of the LLM wiki concept in the vault.

## Key Takeaways

- RAG's critical flaw: no accumulation — every query starts from scratch, re-deriving the same synthesis from raw documents
- Human wikis fail because maintenance burden (cross-references, tags, contradiction-noting) grows faster than value
- Karpathy's frame: 'Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase'
- Three operations: ingest (one source touches 10-15 wiki pages), query (insights saved back as analysis pages), lint (find contradictions/orphans)
- Ecosystem survey: Waykee (team hierarchical context), Sage-Wiki (strict compiler-like 5-step pipeline), Thinking-MCP (captures how you think, not just facts), ELF (scientific research + base-delta protocol), qmd (hybrid BM25+vector local search by Shopify CEO Tobi Lütke)
- Shift in framing: from LLMs as search engines/text generators → to 'tireless librarians and system maintainers'
- Use cases: personal growth, academic research, book tracking, business team knowledge

## Entities Mentioned

- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/tobi-lutke]]
- [[wiki/entities/evoailabs]]
- [[wiki/entities/waykee]]
- [[wiki/entities/sage-wiki]]
- [[wiki/entities/thinking-mcp]]
- [[wiki/entities/elf]]
- [[wiki/entities/qmd]]
- [[wiki/entities/obsidian]]

## Concepts Covered

- [[wiki/concepts/llm-knowledge-base]]
- [[wiki/concepts/rag-vs-wiki]]
- [[wiki/concepts/knowledge-accumulation]]
- [[wiki/concepts/personal-knowledge-management]]
- [[wiki/concepts/second-brain]]
- [[wiki/concepts/knowledge-graph]]
- [[wiki/concepts/hybrid-search]]
- [[wiki/concepts/zettelkasten]]

## Notable Quotes

> "Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase."

> "We are moving away from treating LLMs purely as search engines or text generators, and finally starting to use them as tireless librarians and system maintainers."

## Cross-Connections

This is the theoretical companion to the three practical implementation articles: [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]] (Cole Medin's Claude Code memory), [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]] (Balu Kosuri's implementation), and [[wiki/sources/karpathy-10x-claude-code-llm-wiki]] (Nate Herk's tutorial). The Thinking-MCP project (captures mental models with node decay) is a fascinating cognitive science application of the pattern. Tobi Lütke's qmd connects to the broader developer tool ecosystem (also mentioned in [[wiki/sources/dhh-new-way-writing-code-agent-first]]). The RAG critique directly informs design choices in the LLM wiki articles — why markdown + index beats embeddings for personal knowledge.
