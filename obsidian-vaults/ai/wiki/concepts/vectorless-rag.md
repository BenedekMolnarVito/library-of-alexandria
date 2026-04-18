---
title: "Vectorless RAG"
type: concept
domain: ai
tags:
  - retrieval
  - rag
  - bm25
  - knowledge-management
  - markdown
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/vectorless-rag-reasoning-based-retrieval]]"
  - "[[wiki/sources/markdown-file-beats-vector-database]]"
  - "[[wiki/sources/japanese-firm-markdown-employee]]"
---

# Vectorless RAG

Vectorless RAG is retrieval-augmented generation without vector databases — using structured markdown indexing, BM25 keyword search, or reasoning-based retrieval to identify relevant context rather than embedding-based nearest-neighbor search. The motivation is both pragmatic (eliminating vector database infrastructure costs and operational complexity) and principled (in many personal and small-team knowledge management contexts, well-structured text outperforms vector similarity for identifying relevant content). The [[llm-wiki]] uses vectorless RAG as its standard retrieval model: the index.md file is the navigation structure, and an LLM reads it to find relevant pages.

## Definition

Vectorless RAG encompasses several distinct retrieval approaches that share the property of not requiring embeddings or vector similarity search:

**Index-based navigation**: a comprehensive markdown index (like llm-wiki's index.md) provides a human-readable, LLM-readable catalog of all knowledge. Retrieval is the LLM reading the index and identifying relevant entries. This works well up to hundreds of pages — the full index fits in a single context window.

**BM25 keyword search**: the classical information retrieval ranking function that scores documents by term frequency/inverse document frequency. Fast, requires no embeddings or specialized infrastructure, works on plain text files with `ripgrep` or a simple search library. BM25 is often surprisingly competitive with vector search for keyword-rich queries.

**Hybrid BM25 + vector**: Tobi Lütke's qmd system uses this approach — BM25 for keyword recall, vector reranking for semantic relevance. This captures most of vector search's semantic benefit while reducing dependence on purely vector-based retrieval. A middle ground between pure vectorless and pure vector approaches.

**Reasoning-based retrieval**: the LLM reasons about which documents are likely to be relevant before retrieving them, using metadata (tags, dates, entity lists from frontmatter) rather than semantic similarity. This is the most expensive approach (requires multiple LLM calls) but produces the highest precision for complex queries.

## How It Works

The Japanese firm case study provides the strongest empirical evidence for vectorless approaches. Employees maintained plain markdown "employee wikis" encoding their expertise, project history, and domain knowledge. When tested against vector search over the same content, the markdown wiki retrieval (using keyword search and index navigation) achieved higher task-relevant recall. The explanation: the wiki's structure encoded human-meaningful organization (explicit sections, deliberate categorization, cross-references) that embeddings flattened into uniform semantic proximity. "Linear algebra in animation" and "linear algebra in financial modeling" are semantically close in embedding space; they're in completely different sections of a well-organized wiki.

In the llm-wiki context, vectorless retrieval works through a simple protocol:
1. The agent reads index.md (one page, ~1000-3000 tokens for a moderate wiki)
2. The agent identifies relevant pages from the index descriptions
3. The agent reads those pages directly
4. The agent synthesizes an answer with page references

This adds at most two context-reading steps before synthesis. For a well-maintained index, it is remarkably accurate — the index entries were written by the same LLM that will use them, optimized for navigability.

## Why It Matters

The elimination of vector database infrastructure matters most for personal and small-team knowledge systems where operational overhead is borne by the same person who does the knowledge work. Running and maintaining a Chroma, Pinecone, or Weaviate instance requires: keeping the service running, managing embedding costs, handling index updates, and dealing with service failures. For an individual building a personal knowledge base, this overhead is a significant barrier.

Vectorless RAG removes all of this: the knowledge base is a directory of markdown files, retrieval is grep or LLM index navigation, and there's nothing to maintain beyond the files themselves. This aligns with [[markdown-first-architecture]]'s broader argument: the format that eliminates infrastructure dependencies while maintaining quality is the right format for personal knowledge work.

For large-scale enterprise knowledge management (millions of documents, thousands of users, high-latency tolerance is unacceptable), vector search provides genuine advantages. The vectorless argument is specifically calibrated to personal and small-team contexts where those conditions don't apply.

## In Practice

The practical implementation for an llm-wiki scale knowledge base (50–500 pages): maintain a comprehensive index.md, ensure consistent YAML frontmatter with tags and descriptions, and use standard grep/glob for text search. No additional infrastructure required. At 500+ pages, consider adding BM25 search (ripgrep with keyword queries works well) or a local embedding model for semantic search over the index entries only (not the full documents).

The transition point from vectorless to hybrid approaches depends on: query complexity (highly semantic queries benefit more from vector search), corpus size (>500 pages starts to strain LLM index navigation), and query volume (high-frequency retrieval at latency-sensitive applications may need BM25 or vector indexes for speed).

## Related Concepts

- [[wiki/concepts/rag-vs-llm-wiki]] — the broader comparison context
- [[wiki/concepts/markdown-first-architecture]] — why plain text is the storage format
- [[wiki/concepts/llm-wiki]] — the primary implementation of vectorless retrieval
- [[wiki/concepts/knowledge-accumulation]] — the compounding property that indexes support

## Sources

- [[wiki/sources/vectorless-rag-reasoning-based-retrieval]]
- [[wiki/sources/markdown-file-beats-vector-database]]
- [[wiki/sources/japanese-firm-markdown-employee]]
