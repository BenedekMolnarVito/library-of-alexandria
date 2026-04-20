---
title: "Resident Eval: Mila Jovovich’s MemPalace A First Glimpse"
source: "https://medium.com/@balajibal/resident-eval-mila-jovovichs-mempalace-a-first-glimpse-20898be701fb"
author:
  - "[[balaji bal]]"
published: 2026-04-07
created: 2026-04-20
description: "Resident Eval: Mila Jovovich’s MemPalace A First Glimpse Resident Evil star Milla Jovovich teaming up with an engineer(Ben Sigman) to build a memory system for AI was not on my 2026 bingo card. A …"
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*inBUdDBjCD0qspZbiuR9Kg.png)

Resident Evil star Milla Jovovich teaming up with an engineer([Ben Sigman](https://github.com/bensig)) to build a memory system for AI was not on my 2026 bingo card.

A Hollywood actor and an engineer building an AI memory system sounds like the setup to a joke. Instead, it produced MemPalace: a local-first memory architecture that claims benchmark-beating retrieval while running entirely on-device.

I started taking it for a spin to understand whether the architecture is as interesting as the claims. It comes timely, since I was working on a similar problem.

I’ll report back with deeper impressions soon, but even before that, **one thing stands out: it works completely locally, which means zero token use. That alone is worth paying attention to.**

AI tools are getting better at generating code, explaining systems, and helping us debug. But they still suffer from one glaring limitation: they forget.

Not in the dramatic sci-fi sense. In the practical, deeply annoying engineering sense. They forget why you rejected an architecture last week. They forget the nuance in a long debugging session. They forget the tradeoff behind a product decision. They forget the context buried in dozens of chat threads, docs, notes, and half-finished plans.

MemPalace is not just another “AI memory” feature bolted onto a chatbot. It is a local-first memory system designed to preserve raw context, organize it structurally, compress it intelligently, and make it retrievable by both humans and AI agents.

For software developers, that makes it interesting. Because the hard part of AI memory is not storing text. It is preserving reasoning.

## The problem MemPalace is built to solve

In most AI workflows, the most valuable information is not the final answer. It is the path that led there.

A typical engineering conversation with an assistant might include:

- competing implementation options
- rejected approaches
- assumptions that turned out to be wrong
- debugging hypotheses
- architecture tradeoffs
- team preferences and constraints
- “why” behind the eventual decision

Most memory systems flatten this into a summary. That sounds useful, but summaries are lossy by definition. They preserve conclusions better than rationale.

MemPalace takes the opposite stance. Instead of summarising first and discarding the rest, it tries to **store everything and then make it usable**.

That single design decision shapes the whole system.

## What MemPalace is

At a high level, MemPalace is a local memory layer for AI-assisted work. It ingests conversations, project files, notes, and other artefacts, then organises them into a structured system that supports retrieval, compression, knowledge extraction, and agent access.

The README positions it as a memory substrate for:

- developer workflows
- long-running projects
- AI chat histories
- team knowledge
- specialist agents
- local-first, privacy-sensitive use cases

It is meant to run on your machine, not as a cloud dependency. That matters more than it first appears. If memory is supposed to capture sensitive design discussions, product plans, architecture reasoning, and code-adjacent conversations, local-first is not a bonus feature. It is often a requirement.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*IRl1hOyVet85feLZ_yKaIQ.png)

## The big idea: memory needs structure, not just search

A lot of AI memory tooling defaults to the same architecture:

1. chunk text
2. generate embeddings
3. retrieve semantically similar chunks later

That works to a point. But it treats all memory as a flat space.

MemPalace argues that memory retrieval improves when information is organized before retrieval happens. Instead of searching one giant undifferentiated archive, it arranges knowledge into a hierarchical “palace.”

The structure includes concepts like:

- **Wings** for broad domains
- **Halls** for memory types
- **Rooms** for narrower topics
- **Closets** for compressed recall
- **Drawers** for original verbatim source material

This is a clever idea because it mirrors something developers already understand well: indexes matter.

If you search a massive table without narrowing scope, results get noisy. If you partition the data intelligently first, retrieval improves. MemPalace applies the same intuition to AI memory.

This structural narrowing has led to measurable retrieval gains on a large memory dataset. The implication is important: memory quality is not only an embedding problem. It is also an information architecture problem.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Khj7QXs5T4QSBjqfqXDBEA.png)

## How MemPalace works

The system appears to combine several layers of memory handling rather than relying on a single retrieval strategy.

### 1\. Ingestion and mining

MemPalace begins by ingesting source material. That includes project artifacts and conversations. The examples in the README suggest workflows like:

```c
mempalace init ~/projects/myapp
mempalace mine ~/projects/myapp
mempalace mine ~/chats --mode convos
mempalace search "why did we switch auth providers"
```

The key concept here is “mining.” MemPalace is not just storing files. It is extracting structure from them.

That likely includes:

- categorizing information into the palace hierarchy
- generating compressed forms
- extracting entities and relationships
- preserving original source references

This matters because developers rarely need a generic blob of memory. They need navigable memory.

### 2\. Layered memory

One of the more technically sound ideas in the README is the layered memory stack. Instead of treating all memory as equally important, MemPalace separates it into levels.

The layers are described roughly as:

- **L0**: identity or core context for the AI
- **L1**: essential facts, preferences, project anchors
- **L2**: active topical recall
- **L3**: deep retrieval from the broader archive

This is exactly the kind of hierarchy you would expect from a system designed by someone thinking about context windows as a scarce resource.

A model does not need every memory loaded all the time. It needs:

- a small set of always-hot context
- a medium layer of currently relevant memory
- a large cold layer retrievable on demand

That is a much better fit for LLMs than a naive “stuff more history into the prompt” strategy.

### 3\. Compression with AAAK

One of the most distinctive features in the README is AAAK, a compressed shorthand format for memories.

The idea is unusual but compelling: instead of compressing memory into vectors or opaque latent forms, compress it into structured text that LLMs can still read directly.

MemPalace claims significant compression while keeping the result model-readable and decoder-free. That is important. If the compressed representation is still plain text, then any reasonably capable language model can use it.

That makes AAAK appealing for a few reasons:

- it is model-agnostic
- it preserves interoperability
- it works in local-first settings
- it treats token budget as a real systems constraint

In other words, AAAK is not just summarisation. It is prompt-efficient representation design.

For developers, that is the interesting part. It is an attempt to build a practical intermediate memory format for LLM systems.

## 4\. Retrieval through structure plus semantics

MemPalace does not seem to reject semantic search. It combines semantic retrieval with structural narrowing.

That is an important distinction.

Rather than querying the entire archive flat, the system can:

- identify the likely wing or room
- narrow the retrieval space
- search within that smaller context
- surface compressed memory that links back to verbatim source material

This hybrid approach is more robust than relying on embeddings alone. Semantic search is powerful, but it is often too eager. It finds things that are similar, not necessarily things that belong to the right context.

MemPalace tries to solve that by adding a higher-level taxonomy.

## Why verbatim storage matters

A standout theme is that compressed memory does not replace the original source.

A lot of AI memory tools effectively convert rich conversations into simplified facts. But rich conversations often contain the hard part: ambiguity, disagreement, sequence, justification, and changing assumptions.

If you compress too early, you preserve outcomes while losing reasoning.

MemPalace keeps the original “drawer” alongside more compact “closet” representations. That means the system can retrieve efficiently without permanently discarding the source material.

For software development, this is exactly right. We often do not just need to know what decision was made. We need to know why it was made, what alternatives were considered, and what constraint forced the tradeoff.

## The temporal knowledge graph

Another technically interesting aspect is the built-in temporal knowledge graph. (I am a big fan of temporal knowledge graphs!)

MemPalace stores facts and relationships in a time-aware graph backed by SQLite(“like Zep’s Graphiti, but SQLite instead of Neo4j.”). This allows the system to represent statements that change over time rather than pretending all facts are permanent.

That is useful for real project memory because many facts are temporal:

- who owns a service
- what sprint a task belongs to
- whether a migration is in progress or complete
- which recommendation later became policy
- what was true last month but no longer is

The temporal element makes the graph much more useful than a static fact store. It also opens up timeline queries and contradiction detection.

That last part is especially important. If new information conflicts with existing stored knowledge, the system can flag it rather than silently accumulating inconsistent memory.

That pushes MemPalace beyond simple retrieval. It starts to look like a coherence layer for long-running AI workflows.

## MCP integration turns memory into infrastructure

If MemPalace were only a CLI and a local index, it would already be useful, but MCP integration is a major part of the design.

That means external AI assistants can access the memory system through tools rather than through manual copy-paste.

This is what turns it from a storage utility into agent infrastructure.

An assistant connected through MCP can potentially:

- search relevant memories
- inspect the taxonomy
- query the knowledge graph
- traverse related concepts
- read or write specialist diaries
- detect duplicates or contradictions

This matters because the future of AI tooling is not just “chat with a model.” It is systems of tools, state, workflows, and specialized agents. In that world, memory cannot just be an archive. It has to be operational.

MemPalace seems designed for exactly that.

## Specialist agents and persistent diaries

Another smart idea is that of specialist agents with their own persistent memory streams.

Instead of storing all memory in one giant undifferentiated assistant context, MemPalace supports role-specific memory. An architect agent can maintain architectural context. A reviewer agent can remember recurring code quality issues. An ops agent can accumulate incident knowledge.

Each specialist can have its own diary and part of the palace.

This is a much cleaner pattern than bloating a single assistant prompt with every possible responsibility. It mirrors a good software design principle: separate concerns, preserve interfaces, keep context local to the role that needs it.

## Why software developers should care

MemPalace is interesting because it treats AI memory as a systems design problem rather than a product feature.

It assumes a few things that many developer-facing AI tools still ignore:

- raw reasoning is worth preserving
- token budgets are architectural constraints
- retrieval quality depends on structure
- memory should be layered
- facts change over time
- local-first matters
- agents need operational access to memory, not just passive storage

That combination makes it feel much closer to real engineering infrastructure than to a note-taking wrapper around embeddings.

If you are building long-running agent systems, working heavily with local models, or using AI tools across large projects, these ideas matter. Stateless assistants are fine for single-turn tasks. They break down when continuity becomes the real product.

## Final thought

The most compelling thing about MemPalace is not that it remembers more. It is that it appears to remember in the right shape.

It keeps original material. It adds structure before retrieval. It compresses for prompt efficiency without becoming opaque. It models time. It exposes memory through tools. And it does all of this in a local-first architecture. That is quite a lot packed into a single library.

[![balaji bal](https://miro.medium.com/v2/resize:fill:96:96/0*k-4QkwCAlzMLp_GZ.jpeg)](https://medium.com/@balajibal?source=post_page---post_author_info--20898be701fb---------------------------------------)

[![balaji bal](https://miro.medium.com/v2/resize:fill:128:128/0*k-4QkwCAlzMLp_GZ.jpeg)](https://medium.com/@balajibal?source=post_page---post_author_info--20898be701fb---------------------------------------)

[514 following](https://medium.com/@balajibal/following?source=post_page---post_author_info--20898be701fb---------------------------------------)

Founder @ [HeadGym.com](http://headgym.com/) where we are building The AI Workspace. I write mainly about Applied AI, Software Architecture and DevOps.