---
title: "Vectorless RAG: How I Built a RAG System Without Embeddings, Databases, or Vector Similarity"
type: source
domain: ai
tags:
  - rag
  - retrieval
  - document-intelligence
  - langgraph
  - reasoning-based-retrieval
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Vectorless RAG How I Built a RAG System Without Embeddings, Databases, or Vector Similarity.md]]"
---

# Vectorless RAG: How I Built a RAG System Without Embeddings, Databases, or Vector Similarity

**Authors**: Alpha Iterations
**Date**: 2026-04
**Type**: article

## Summary

Traditional RAG retrieves text by vector similarity ("what looks similar to the query?"). Vectorless RAG replaces this with reasoning-based navigation ("where should I go next?") by first building a hierarchical document tree (title → chapter → section → subsection), then asking an LLM to reason over the tree structure and select relevant sections before retrieving full context. The article includes a complete Python implementation using LangGraph, PyMuPDF4LLM, and OpenAI, demonstrated on the Google Bigtable paper.

The author clarifies that the only fundamental limitation of traditional RAG is retrieval based on similarity rather than reasoning — structure loss, fragmentation, and cost are engineering problems with solutions, not inherent flaws. Vectorless RAG trades higher latency and per-query LLM cost for better handling of structured documents requiring multi-step reasoning, cross-section synthesis, and navigation rather than lookup. Traditional vector RAG retains advantages for search at scale, large unstructured corpora, and low-latency requirements.

## Key Takeaways

- Traditional RAG's only fundamental limitation is that retrieval is based on similarity, not reasoning — structure loss and fragmentation are solvable engineering problems
- Vectorless RAG: one-time document tree generation → at query time, LLM reasons over tree structure → selects relevant sections → retrieves full section text → generates answer
- Document tree nodes contain: title, summary, page boundaries, and optional full text — enables navigation without scanning the full document
- Best for: documents with clear structure, questions requiring section navigation, context spread across related subsections
- Trade-offs: higher latency (multiple LLM calls per query), higher per-query cost, dependent on structure quality
- Traditional RAG is better for: search at scale, large unstructured corpora, low-latency requirements
- Implementation stack: LangGraph, OpenAI, PyMuPDF, pymupdf4llm, PageIndex concept

## Entities Mentioned

- [[wiki/entities/alpha-iterations]]
- [[wiki/entities/openai]]
- [[wiki/entities/langgraph]]
- [[wiki/entities/pymupdf]]
- [[wiki/entities/google]]

## Concepts Covered

- [[wiki/concepts/rag]]
- [[wiki/concepts/vectorless-rag]]
- [[wiki/concepts/reasoning-based-retrieval]]
- [[wiki/concepts/document-tree]]
- [[wiki/concepts/embeddings]]
- [[wiki/concepts/vector-databases]]
- [[wiki/concepts/hybrid-rag]]
- [[wiki/concepts/agentic-rag]]
- [[wiki/concepts/context-fragmentation]]
- [[wiki/concepts/reranking]]

## Notable Quotes

> "Vector search answers the question: 'What text looks similar to the query?' But many real-world queries require causal understanding, multi-step reasoning, synthesizing information across sections."

> "Traditional RAG retrieves based on similarity, not reasoning."

## Cross-Connections

Directly challenges the default assumption in [[wiki/sources/death-of-traditional-etl-ai-agents]] that vector stores are required for RAG pipelines. Complements [[wiki/sources/markdown-file-beats-vector-database]] — both argue files and structure beat vectors for many agent memory use cases. The document tree concept is architecturally similar to how CLAUDE.md's hierarchical loading in [[wiki/sources/japanese-firm-markdown-employee]] provides progressive disclosure of context. The upstream dependency on document parsing quality connects to [[wiki/sources/chandra-ocr-2-benchmark]] — poor OCR limits the structure quality that Vectorless RAG depends on.
