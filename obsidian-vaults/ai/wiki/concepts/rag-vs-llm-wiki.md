---
title: "RAG vs LLM Wiki"
type: concept
domain: ai
tags:
  - rag
  - knowledge-management
  - retrieval
  - llm-wiki
  - vector-databases
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]"
  - "[[wiki/sources/markdown-file-beats-vector-database]]"
  - "[[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]"
  - "[[wiki/sources/vectorless-rag-reasoning-based-retrieval]]"
---

# RAG vs LLM Wiki

Retrieval-Augmented Generation (RAG) and the LLM wiki are two fundamentally different philosophies for augmenting an LLM with persistent knowledge. RAG retrieves relevant chunks from a corpus at query time and injects them into context; the LLM wiki maintains a curated, pre-synthesized knowledge graph that an LLM reads directly. The critical distinction is that RAG cannot accumulate knowledge — every query starts from scratch, re-deriving syntheses the system has already computed. The LLM wiki accumulates: each ingest enriches existing pages, and insights from previous queries persist as analysis pages.

## Definition

**Retrieval-Augmented Generation** uses a vector database (or BM25 index) to find semantically similar chunks from a document corpus and injects them into the LLM's prompt at query time. The classic pipeline is: embed query → nearest-neighbor search → inject top-k chunks → generate answer. RAG is powerful for querying large static corpora where no pre-synthesis is possible, but it has a fundamental architectural limitation: the retrieval layer has no memory of previous queries or accumulated insights.

An **LLM wiki** (see [[llm-wiki]]) is a different approach: rather than storing raw chunks and retrieving them at query time, the LLM pre-synthesizes knowledge into structured wiki pages that are directly readable. The index is human-inspectable markdown, not a high-dimensional vector space. Retrieval is navigation (read index → follow links → read pages), not similarity search.

## How It Works

The contrast becomes sharp when you consider what happens with repeated queries. In a RAG system, if you ask "what are the relationships between transformer attention and mixture-of-experts?" today and again in six months after ingesting twenty new papers, the system performs the same retrieval both times — it has no way to remember that it already derived this synthesis. Every query is cold.

In an LLM wiki, the first time that question is answered, the result can be saved as an analysis page. The next time the question (or a related one) is asked, the agent finds the analysis page in the index and builds on it. The synthesis compounds. This is the [[knowledge-accumulation]] property that RAG fundamentally lacks.

**Human wikis** (Wikipedia, Confluence, Notion) have the accumulation property but fail on maintenance cost. Keeping hundreds of pages cross-referenced, current, and contradiction-free is crushing work for humans doing it manually. The maintenance burden grows superlinearly with page count. Human wikis succeed at organizational scale (hundreds of contributors) but fail for individuals and small teams.

The LLM wiki solves both problems simultaneously: AI handles maintenance (making it sustainable at individual scale), and the architecture accumulates knowledge (unlike RAG).

## Why It Matters

The "Markdown File That Beat a $50M Vector Database" thesis captures the practical implication: for personal knowledge at scale, a well-structured markdown index navigated by an LLM outperforms vector search in retrieval quality, cost, and portability. Vector databases require infrastructure, ongoing embedding costs, and specialized tooling. A markdown index requires a text editor.

A Japanese firm case study (see [[wiki/sources/japanese-firm-markdown-employee]] and [[markdown-first-architecture]]) demonstrated this empirically: employees maintained plain markdown "employee wikis" — structured documents encoding their expertise, project history, and lessons learned. Retrieval quality for task-relevant knowledge exceeded what vector search over the same content produced, because the markdown structure encoded human-meaningful organization that vectors flattened away.

This doesn't mean RAG is wrong — for querying large, unstructured document corpora (legal discovery, academic literature search, customer support knowledge bases) RAG remains the right tool. The comparison is specifically about **personal knowledge management** at the scale of hundreds to low thousands of documents, where the LLM wiki's maintenance automation is practical and the accumulation benefit is substantial.

## In Practice

The hybrid approach is also viable: [[vectorless-rag]] uses BM25 keyword search or a comprehensive markdown index instead of vectors, capturing much of RAG's retrieval flexibility without the infrastructure cost. Tobi Lütke's qmd system used a hybrid BM25+vector approach for local knowledge management, suggesting the practical optimum is somewhere between pure vector RAG and pure wiki navigation for some use cases.

The index.md file serves as the LLM wiki's retrieval mechanism: a flat, human-readable catalog of all pages with one-line descriptions. For hundreds of pages, the LLM can read the full index in a single context window, navigate to relevant pages, and synthesize an answer without any embedding or vector search. This is the simplest possible retrieval system, and it works remarkably well precisely because the index was written by the same LLM that will use it.

## Related Concepts

- [[wiki/concepts/llm-wiki]] — the full architecture of the alternative
- [[wiki/concepts/knowledge-accumulation]] — the compounding property RAG lacks
- [[wiki/concepts/vectorless-rag]] — retrieval without vectors
- [[wiki/concepts/markdown-first-architecture]] — why plain files work for retrieval
- [[wiki/concepts/second-brain]] — the PKM philosophy both systems try to realize
- [[wiki/concepts/personal-knowledge-management]] — the broader context

## Key Entities

- [[wiki/entities/andrej-karpathy]] — primary advocate for LLM wiki approach

## Sources

- [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]
- [[wiki/sources/markdown-file-beats-vector-database]]
- [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]
- [[wiki/sources/vectorless-rag-reasoning-based-retrieval]]
