---
title: "Tobi Lütke"
type: entity
domain: ai
tags:
  - person
  - ceo
  - shopify
  - tools
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]"
---

# Tobi Lütke

Tobi Lütke is the CEO of Shopify and a prolific builder of personal tools who appears in the AI knowledge management corpus in connection with `qmd` — a hybrid BM25 and vector search tool he built for personal knowledge management that addresses a key limitation of pure vector search systems.

## Background / History

Lütke co-founded Shopify in 2006 and has led it to become one of the dominant global e-commerce platforms. He is known in the technology community not only as a business leader but as a hands-on technical thinker who builds his own tools and shares them publicly. His involvement in the personal knowledge management discussion reflects a broader pattern among technical CEOs who engage seriously with their own information systems rather than delegating cognitive infrastructure entirely to commercial products.

## Key Contributions / Features

**qmd — Hybrid BM25 + Vector Search**: Lütke built `qmd`, a local search tool that combines BM25 (traditional keyword-based full-text search) with vector (semantic) search for personal knowledge bases. The hybrid approach addresses the well-known weaknesses of pure vector search — which can miss exact-match queries and specific terminology — while retaining the semantic similarity capabilities that make vector search useful for conceptual queries. In the context of [[wiki/entities/andrej-karpathy]]'s LLM wiki discussion, Lütke's tool was highlighted as an example of the kind of retrieval infrastructure that makes large personal knowledge bases practically navigable. (Source: [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]])

**Personal Knowledge Infrastructure**: Lütke's engagement with the personal search problem signals that even at the CEO level of major tech companies, the limitations of available knowledge management tools are felt acutely. His decision to build rather than buy is consistent with his broader engineering culture at Shopify.

## Role in AI Landscape

Lütke's qmd tool is a data point in the broader conversation about how LLM-based knowledge wikis scale — as they grow beyond 200 pages, pure LLM context injection becomes impractical and retrieval infrastructure becomes necessary. His hybrid search approach represents one answer to this problem, and his willingness to share it publicly makes it a reference implementation for others building personal AI-assisted knowledge systems.

## Connections

- **Related entities**: [[wiki/entities/andrej-karpathy]], [[wiki/entities/obsidian]]
- **Key concepts**: [[wiki/concepts/llm-wiki-pattern]], [[wiki/concepts/vector-search]], [[wiki/concepts/knowledge-retrieval]]
- **Sources**: [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]
