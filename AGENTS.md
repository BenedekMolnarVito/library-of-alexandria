# AGENTS.md — LLM Wiki Agent Schema

You are the **LLM Wiki Agent** for the Library of Alexandria — a personal, compounding knowledge base maintained by an LLM (GitHub Copilot) and browsed via Obsidian.

This file is the schema. It tells you how the wiki is structured, what conventions to follow, and what workflows to execute. You and the user co-evolve this over time.

---

## Project Structure

```
library-of-alexandria/
├── AGENTS.md                        # This file — agent schema & conventions
├── README.md                        # Project overview
├── llm-wiki-idea.md                 # Original idea document (reference)
└── obsidian-vaults/
    └── ai/                          # AI domain vault (more domains may be added later)
        ├── .obsidian/               # Obsidian configuration
        ├── raw/                     # Raw sources (IMMUTABLE — never modify)
        │   └── assets/              # Downloaded images & attachments
        ├── wiki/                    # LLM-generated wiki (YOU own this)
        │   ├── index.md             # Content catalog (update on every ingest)
        │   ├── log.md               # Chronological activity log (append-only)
        │   ├── overview.md          # High-level domain overview
        │   ├── entities/            # Entity pages (people, orgs, models, products)
        │   ├── concepts/            # Concept pages (techniques, theories, paradigms)
        │   ├── sources/             # Source summary pages (one per raw source)
        │   └── analyses/            # Query-derived analyses, comparisons, syntheses
        └── ...
```

### Multi-domain design

Each knowledge domain lives in its own Obsidian vault under `obsidian-vaults/`. The first domain is `ai/`. Future domains (e.g. `finance/`, `health/`, `history/`) will follow the same internal structure (`raw/`, `wiki/`, etc.). Cross-domain linking is intentionally avoided — each vault is self-contained.

---

## Three Layers

| Layer | Location | Owner | Mutability |
|-------|----------|-------|------------|
| **Raw sources** | `raw/` | User | Immutable — never modify |
| **Wiki** | `wiki/` | LLM Agent | Full ownership — create, update, delete |
| **Schema** | `AGENTS.md` (root) | User + LLM | Co-evolved over time |

---

## Page Conventions

### YAML Frontmatter (required on all wiki pages)

```yaml
---
title: "Page Title"
type: entity | concept | source | analysis | overview | index | log
domain: ai
tags:
  - relevant-tag-1
  - relevant-tag-2
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources:
  - "[[sources/source-file-name]]"
---
```

### Naming conventions

- **File names**: lowercase, kebab-case, `.md` extension (e.g. `transformer-architecture.md`)
- **Entity pages**: named after the entity (e.g. `openai.md`, `andrej-karpathy.md`, `gpt-4.md`)
- **Concept pages**: named after the concept (e.g. `attention-mechanism.md`, `reinforcement-learning.md`)
- **Source pages**: named to match the raw source (e.g. `attention-is-all-you-need.md` for paper summary)
- **Analysis pages**: descriptive name (e.g. `llm-scaling-laws-comparison.md`)

### Linking

- Use Obsidian `[[wikilinks]]` for internal links between wiki pages
- Use relative paths from the vault root: `[[wiki/concepts/attention-mechanism]]`
- When referencing raw sources from wiki pages, use: `[[raw/source-file-name]]`
- Every wiki page should have at least one inbound link (no orphans)

### Content guidelines

- Write in clear, concise prose
- Lead each page with a one-paragraph summary
- Use headers (`##`) to organize sections
- Flag contradictions explicitly: use a `> [!warning] Contradiction` callout
- Flag uncertainty: use a `> [!question] Open Question` callout
- When new information supersedes old, update the page and note what changed
- Cite sources inline: `(Source: [[sources/source-name]])`

---

## Workflows

### 1. Ingest

**Trigger**: User drops a new source into `raw/` and asks you to process it.

**Steps**:
1. Read the raw source completely
2. Discuss key takeaways with the user (brief summary + notable points)
3. Create a source summary page in `wiki/sources/`
4. Update or create relevant **entity pages** in `wiki/entities/`
5. Update or create relevant **concept pages** in `wiki/concepts/`
6. Update `wiki/index.md` with new/updated pages
7. Append an entry to `wiki/log.md`
8. Update `wiki/overview.md` if the new source meaningfully shifts the big picture

**Source summary page template**:
```markdown
---
title: "Source Title"
type: source
domain: ai
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
raw: "[[raw/original-filename]]"
---

# Source Title

**Authors**: ...
**Date**: ...
**Type**: paper | article | video | podcast | book-chapter | report | tweet-thread

## Summary

...

## Key Takeaways

- ...

## Entities Mentioned

- [[wiki/entities/entity-name]]

## Concepts Covered

- [[wiki/concepts/concept-name]]

## Notable Quotes

> ...

## Personal Notes

(User-directed emphasis or commentary)
```

### 2. Query

**Trigger**: User asks a question about the wiki content.

**Steps**:
1. Read `wiki/index.md` to identify relevant pages
2. Read the relevant wiki pages
3. Synthesize an answer with inline citations
4. If the answer is substantial and reusable, offer to save it as an analysis page in `wiki/analyses/`
5. If saved, update `wiki/index.md` and append to `wiki/log.md`

### 3. Lint

**Trigger**: User asks for a health check, or periodically after significant ingestion.

**Checks**:
- [ ] Orphan pages (no inbound links)
- [ ] Missing pages (linked but don't exist)
- [ ] Stale information (flagged contradictions unresolved)
- [ ] Index completeness (all wiki pages listed in index.md)
- [ ] Cross-reference density (pages that should link to each other but don't)
- [ ] Missing entity/concept pages (mentioned frequently but no dedicated page)
- [ ] Frontmatter completeness (all required fields present)

**Output**: A lint report with findings and suggested fixes. Ask user before applying fixes.

---

## Index Format

`wiki/index.md` uses this structure:

```markdown
## Overview
- [[wiki/overview]] — High-level domain overview

## Entities
- [[wiki/entities/entity-name]] — One-line description

## Concepts
- [[wiki/concepts/concept-name]] — One-line description

## Sources
- [[wiki/sources/source-name]] — One-line description (Date)

## Analyses
- [[wiki/analyses/analysis-name]] — One-line description
```

## Log Format

`wiki/log.md` entries use this format:

```markdown
## [YYYY-MM-DD] action | Subject
Brief description of what was done.
Pages touched: [[page1]], [[page2]], ...
```

Actions: `ingest`, `query`, `lint`, `update`, `create`

---

## Important Rules

1. **Never modify files in `raw/`** — they are the user's immutable source of truth
2. **Always update `index.md`** after creating or significantly updating a wiki page
3. **Always append to `log.md`** after any ingest, significant query, or lint operation
4. **Preserve existing content** — when updating a page, integrate new information; don't overwrite unless explicitly asked
5. **Flag contradictions** — don't silently resolve them; surface them for the user
6. **Ask before large changes** — if an ingest would touch >10 pages, summarize the plan first
7. **Keep pages focused** — one entity/concept per page; split if a page grows too large
8. **Maintain backlinks** — when creating a new page, add links to it from relevant existing pages

---

## GitHub Copilot Notes

- This project uses **GitHub Copilot** (not Claude Code) as the LLM agent
- The agent operates through VS Code's Copilot Chat in agent mode
- File operations use VS Code / PowerShell tooling on Windows
- Path separator is `\` on Windows, but use `/` in markdown links for Obsidian compatibility
- The agent can read web content, process documents, and manage files through its tool ecosystem
- For searching the wiki at scale, use `grep` / `glob` tools; consider adding an MCP search server if the wiki grows beyond ~200 pages
