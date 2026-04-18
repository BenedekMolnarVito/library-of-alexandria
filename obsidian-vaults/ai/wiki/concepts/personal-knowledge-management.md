---
title: "Personal Knowledge Management (PKM)"
type: concept
domain: ai
tags:
  - knowledge-management
  - second-brain
  - obsidian
  - productivity
  - information-management
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]"
  - "[[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]"
---

# Personal Knowledge Management (PKM)

Personal knowledge management (PKM) is the practice of capturing, organizing, connecting, and retrieving personal knowledge — information gathered through reading, research, experience, and conversation — in ways that make it useful for future thinking and work. The field has produced a rich ecosystem of tools (Obsidian, Notion, Roam Research, Logseq) and methodologies (Zettelkasten, Building a Second Brain, GTD). The AI augmentation of PKM — most fully realized in the [[llm-wiki]] pattern — addresses the field's defining problem: the bookkeeping cost of maintaining a high-quality knowledge base has historically been prohibitive for most practitioners.

## Definition

PKM encompasses four core activities:

**Capture**: the collection of new information — from sources read, ideas generated, conversations had, and experiences processed. Good capture systems minimize friction (the note is created before the insight is lost) while maintaining sufficient structure to be retrievable.

**Organize**: the arrangement of captured information so that related things are near each other and retrieval is possible. This includes tagging, filing, linking, and indexing. Organize is where most PKM systems struggle: the effort to maintain organization at scale typically overwhelms individual practitioners.

**Distill**: the synthesis of captured information into more refined, durable knowledge — rewriting notes in one's own words, extracting key insights, connecting new information to existing understanding. This is the intellectually valuable part of PKM, but it's crowded out by the time spent on organize.

**Express**: using the accumulated knowledge to produce new thinking, writing, decisions, and work. The test of a PKM system is whether the accumulated knowledge makes you measurably better at the things you care about.

## How It Works

The dominant tools in the PKM space reflect different philosophies about the organize problem:

**Obsidian**: local-first, markdown-based, graph navigation. No opinionated structure — the user creates their own. Maximum flexibility, maximum bookkeeping burden.

**Notion**: cloud-based, structured, database-oriented. More organizational scaffolding, more capture friction.

**Roam Research**: outliner with bidirectional links, daily notes as the organizing principle. Graph structure emerges from link patterns.

**Logseq**: open-source Roam alternative, also outline-based with bidirectional links.

All of these tools excel at capture and provide reasonable organize support. All struggle with the same fundamental problem: maintaining a large, well-organized, well-cross-linked knowledge base at individual scale requires more bookkeeping effort than most practitioners sustain over time.

"The hard part of a knowledge base was never the reading or the thinking. It was always the bookkeeping." This observation from Karpathy captures why PKM systems tend to degrade: the reading and thinking are intrinsically rewarding; the bookkeeping is not, and it accumulates as debt.

## Why It Matters

The AI augmentation of PKM addresses the bookkeeping problem directly. The [[llm-wiki]] pattern assigns bookkeeping (write pages, update cross-links, maintain index, flag contradictions) to an AI agent that performs it reliably and without complaint. The human retains the activities that require human judgment (find sources worth reading, ask questions worth answering, make decisions about priorities).

This division of labor makes a genuinely high-quality PKM system — one that a serious researcher would want — achievable for individuals who previously couldn't maintain one. The system doesn't degrade over time because AI bookkeeping doesn't experience fatigue, motivation dips, or competing priorities.

The PKM market implication: tools that integrate AI bookkeeping as a first-class feature (rather than bolt-on AI assistance) will likely displace or transform those that don't. The value of a PKM tool was always downstream of how well it solved the organize problem; LLMs solve the organize problem.

## In Practice

The practical progression for PKM practitioners moving toward AI-augmented systems:

1. Start with a capture-only system (Obsidian vault, or similar) to build the source collection habit
2. Add a schema file (AGENTS.md) that encodes the structure you want the AI to maintain
3. Begin ingest: drop sources into raw/ and let the AI build wiki pages from them
4. Ask questions: the AI synthesizes answers from the wiki and can save them as analysis pages
5. Lint periodically: the AI checks for orphans, missing pages, and contradictions

The key discipline remains human: the system is only as good as the sources put into it. AI can organize and synthesize brilliantly; it cannot determine which sources are worth capturing. Curation judgment remains irreducibly human.

## Related Concepts

- [[wiki/concepts/llm-wiki]] — the AI-augmented PKM realization
- [[wiki/concepts/second-brain]] — the PKM philosophy the LLM wiki realizes
- [[wiki/concepts/knowledge-accumulation]] — the compounding property that makes PKM worth the investment
- [[wiki/concepts/markdown-first-architecture]] — the format most PKM tools use natively
- [[wiki/concepts/rag-vs-llm-wiki]] — retrieval architectures for PKM systems

## Key Entities

- [[wiki/entities/andrej-karpathy]] — LLM wiki as PKM solution
- [[wiki/entities/obsidian]] — the primary tool for markdown-first PKM
- [[wiki/entities/tiago-forte]] — Building a Second Brain methodology

## Sources

- [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]
- [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]
