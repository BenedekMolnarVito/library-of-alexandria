---
title: "Obsidian"
type: entity
domain: ai
tags:
  - product
  - note-taking
  - knowledge-management
  - markdown
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]"
  - "[[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]"
  - "[[wiki/sources/claude-code-karpathy-obsidian-new-meta]]"
---

# Obsidian

Obsidian is a markdown-native note-taking application with a graph view, a rich plugin ecosystem, and local-first storage that has become the preferred knowledge management tool for the LLM wiki pattern pioneered by [[wiki/entities/andrej-karpathy]]. In Karpathy's formulation, "Obsidian is the IDE" — the environment in which the LLM-generated wiki lives and is navigated.

## Background / History

Obsidian was released in 2020 by Shida Li and Erica Xu, who built it as a local-first alternative to cloud-based note-taking apps like Notion and Roam Research. Its core design decisions — all data stored as local markdown files, bidirectional wikilinks, a visual graph of note connections, and an extensive plugin system — have made it particularly well-suited to knowledge management workflows that involve large numbers of interconnected notes. As of 2024, Obsidian has become one of the most popular tools in the personal knowledge management (PKM) community.

Obsidian's relevance to the AI knowledge management story comes from a convergence of design properties: it stores notes as plain text markdown (which LLMs can read and write natively), it supports wikilinks (which LLMs can generate naturally), its local storage makes it compatible with file-system-based AI tools like [[wiki/entities/claude-code]], and its graph view makes the structure of LLM-generated knowledge bases visible and navigable.

## Key Contributions / Features

**IDE Metaphor for LLM Wikis**: Karpathy's formulation places Obsidian as the "IDE" in the LLM wiki pattern — the environment where the programmer (LLM) writes and edits the codebase (wiki). This metaphor works because both IDEs and Obsidian provide: a file system for storing and organizing content, syntax highlighting and rendering, navigation tools (graph view ≈ file explorer + symbol navigator), and a way to see the whole structure at a glance. (Source: [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]])

**Wikilink Compatibility**: Obsidian's `[[wikilink]]` syntax is the standard internal linking mechanism for LLM-generated wiki content. Because the links are just text in markdown files, LLMs can generate them naturally as part of content creation, and Obsidian resolves them to actual file connections automatically.

**Graph View**: The Obsidian graph view renders all notes and their connections as an interactive force-directed graph — providing a visual overview of the knowledge base structure that is particularly useful for identifying gaps, clusters, and orphan notes. For LLM-maintained wikis, this provides a layer of human oversight over the AI-generated structure.

**Plugin Ecosystem**: Obsidian's plugin ecosystem includes tools for task management, Kanban boards, calendar views, database tables, code execution, and many others — extending its utility beyond pure note-taking. Relevant plugins include templating tools (for enforcing wiki page structure), dataview (for SQL-like queries over note metadata), and sync plugins for cross-device access.

**Future of Personal Knowledge**: The discussion of Obsidian in the context of [[wiki/entities/tobi-lutke]]'s qmd tool and other retrieval infrastructure represents the emerging question of how Obsidian-based wikis scale beyond hundreds of pages — where pure human navigation and LLM context injection become insufficient and retrieval infrastructure becomes necessary. (Source: [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]])

## Role in AI Landscape

Obsidian's role in the AI knowledge management ecosystem is that of the preferred substrate for LLM-maintained knowledge bases. Its combination of plain-text storage, wikilink support, local-first architecture, and visual graph navigation makes it uniquely well-suited to the LLM wiki pattern in ways that alternatives (Notion, Roam, Logseq) partially but not fully match. As the LLM wiki pattern proliferates, Obsidian is becoming the default infrastructure layer of choice for practitioners building personal AI-assisted knowledge systems.

## Connections

- **Related entities**: [[wiki/entities/andrej-karpathy]], [[wiki/entities/tobi-lutke]], [[wiki/entities/claude-code]], [[wiki/entities/balu-kosuri]], [[wiki/entities/cole-medin]]
- **Key concepts**: [[wiki/concepts/llm-wiki-pattern]], [[wiki/concepts/knowledge-management]], [[wiki/concepts/personal-knowledge-base]]
- **Sources**: [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]], [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]], [[wiki/sources/claude-code-karpathy-obsidian-new-meta]]
