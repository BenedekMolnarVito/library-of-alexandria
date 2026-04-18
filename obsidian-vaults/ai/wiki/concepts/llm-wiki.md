---
title: "LLM Wiki"
type: concept
domain: ai
tags:
  - knowledge-management
  - llm
  - obsidian
  - markdown
  - personal-knowledge
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]"
  - "[[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]"
  - "[[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]"
  - "[[wiki/sources/karpathy-10x-claude-code-llm-wiki]]"
  - "[[wiki/sources/claude-code-karpathy-obsidian-new-meta]]"
---

# LLM Wiki

An LLM wiki is a markdown-based knowledge base where a human curates sources and asks questions while a large language model handles all bookkeeping — cross-referencing, tagging, updating, finding contradictions, and maintaining the index. The system is divided into three immutable layers: raw sources the human collects, a wiki the LLM writes and maintains, and a schema file (AGENTS.md or equivalent) that encodes the rules both parties follow. The intellectual breakthrough is that the hardest part of maintaining a personal knowledge base — the ongoing curation and cross-linking — is precisely what LLMs excel at.

## Definition

An LLM wiki is a co-owned knowledge system with strict role separation. The human is responsible for two things only: dropping new source material into a `raw/` directory, and asking questions. The LLM is responsible for everything else: reading the source, writing a summary page, updating every relevant entity and concept page, maintaining the index, and logging each action. Neither party encroaches on the other's domain — the raw sources are immutable (the LLM never edits them), and the wiki pages are fully owned by the LLM (the human doesn't hand-edit them unless explicitly correcting the agent).

Andrej Karpathy framed this relationship memorably: "Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase." This analogy is precise. Obsidian provides the graph-navigation and visualization layer. The LLM is the engineer who writes, refactors, and cross-links. The wiki files are the living artifact — version-controlled, portable, inspectable at any time.

## How It Works

The system operates through three distinct workflows:

**Ingest** is triggered when a new source lands in `raw/`. The LLM reads it completely, discusses key takeaways, then creates or updates 10–15 pages: one source summary, several entity pages (people, organizations, models), several concept pages (techniques, ideas), updates to the index, and a log entry. The ingest workflow is the growth engine — each new source doesn't just add one page, it enriches a web of existing pages with new connections.

**Query** is triggered when the human asks a question. The LLM reads `index.md` to locate relevant pages, reads those pages, and synthesizes a cited answer. If the answer is substantial and reusable, the LLM offers to save it as an analysis page in `wiki/analyses/` — turning a one-off question into a permanent asset.

**Lint** is a health check: the LLM scans for orphan pages (no inbound links), missing pages (linked but nonexistent), stale contradictions, and gaps in the index. Unlike ingest and query, lint produces a report for the human to review before any fixes are applied.

## Why It Matters

The LLM wiki solves two simultaneous problems that have defeated personal knowledge management for decades. The first is the bookkeeping problem: maintaining cross-references, keeping pages current, and finding contradictions is crushing work for a human doing it manually. Human wikis fail because the maintenance burden grows faster than the value extracted. The second is the accumulation problem: [[rag-vs-llm-wiki|RAG systems]] re-derive the same synthesis from scratch on every query, never accumulating insight. The LLM wiki has both: maintenance is automated, and knowledge compounds with each ingest.

The system also requires no specialized infrastructure. There is no vector database, no embedding pipeline, no cloud service. The `index.md` file serves as the navigation map for hundreds of pages, and standard grep/glob tools can search it. At very large scale (>200 pages), a BM25 or hybrid search tool can augment the index, but the basic system is just files — which is the point. See [[markdown-first-architecture]] and [[vectorless-rag]] for the technical argument.

## In Practice

The historical antecedent is Vannevar Bush's 1945 Memex concept — a hypothetical device for storing and retrieving knowledge via "associative trails," foreshadowing hyperlinks and personal knowledge management by decades. The LLM wiki is the practical realization of what Bush imagined: a system that maintains its own associative trails automatically.

The three-layer architecture maps cleanly to software engineering best practices. `raw/` is like an append-only event log — immutable, the source of truth. `wiki/` is the derived state — computed from raw, always rebuildable. `AGENTS.md` is the schema — the contract between the human operator and the LLM agent. This separation means the system is resilient: if the LLM makes a mistake, the raw sources remain intact and the wiki can be rebuilt.

Practically, the system works well with any Obsidian-compatible vault and any LLM with file-writing capability (Claude Code, GitHub Copilot in agent mode, etc.). The key discipline is trusting the LLM to own the wiki layer — fighting the urge to manually edit pages defeats the automation.

## Related Concepts

- [[wiki/concepts/rag-vs-llm-wiki]] — why LLM wiki beats RAG for personal knowledge
- [[wiki/concepts/second-brain]] — the knowledge philosophy this realizes
- [[wiki/concepts/personal-knowledge-management]] — broader PKM context
- [[wiki/concepts/markdown-first-architecture]] — why plain files work
- [[wiki/concepts/vectorless-rag]] — how retrieval works without vectors
- [[wiki/concepts/knowledge-accumulation]] — the compounding property
- [[wiki/concepts/claude-md]] — the schema file pattern
- [[wiki/concepts/context-portability]] — portability advantage of plain files

## Key Entities

- [[wiki/entities/andrej-karpathy]] — coined the framing, pioneered the pattern
- [[wiki/entities/obsidian]] — the IDE in Karpathy's analogy

## Sources

- [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]
- [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]
- [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]
- [[wiki/sources/karpathy-10x-claude-code-llm-wiki]]
- [[wiki/sources/claude-code-karpathy-obsidian-new-meta]]
