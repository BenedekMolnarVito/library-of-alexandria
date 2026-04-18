# Library of Alexandria

A personal, compounding knowledge base powered by an LLM agent — inspired by [Andrej Karpathy's LLM Wiki idea](https://github.com/karpathy/llm-wiki).

## How it works

Instead of RAG-style retrieval, the LLM **incrementally builds and maintains a persistent wiki** — a structured, interlinked collection of markdown files that sits between you and the raw sources. When a new source is added, the LLM reads it, extracts key information, and integrates it into the existing wiki — updating entity pages, revising topic summaries, flagging contradictions, and strengthening the evolving synthesis.

**You curate sources and ask questions. The LLM does all the bookkeeping.**

## Architecture

| Layer | Description |
|-------|-------------|
| **Raw sources** (`raw/`) | Your curated source documents — immutable, never modified by the LLM |
| **Wiki** (`wiki/`) | LLM-generated markdown — summaries, entity pages, concept pages, analyses |
| **Schema** (`AGENTS.md`) | Instructions that make the LLM a disciplined wiki maintainer |

## Knowledge Domains

Each domain lives in its own [Obsidian](https://obsidian.md/) vault under `obsidian-vaults/`:

- **`ai/`** — Artificial Intelligence: models, research, companies, trends, tools

More domains can be added following the same structure.

## Usage

1. Open the Obsidian vault for browsing (`obsidian-vaults/ai/`)
2. Drop raw sources (articles, papers, notes) into `raw/`
3. Ask the LLM Wiki Agent (GitHub Copilot) to **ingest** them
4. **Query** the wiki — ask questions, get cited answers
5. **Lint** periodically — let the agent health-check the wiki

## Tools

- **[Obsidian](https://obsidian.md/)** — for browsing the wiki, graph view, and real-time reading
- **[Obsidian Web Clipper](https://obsidian.md/clipper)** — for clipping web articles into `raw/`
- **GitHub Copilot** — the LLM agent that maintains the wiki
