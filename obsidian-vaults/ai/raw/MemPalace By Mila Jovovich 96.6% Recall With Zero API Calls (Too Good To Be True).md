---
title: "MemPalace By Mila Jovovich: 96.6% Recall With Zero API Calls (Too Good To Be True?)"
source: "https://ai.gopubby.com/mempalace-by-mila-jovovich-96-6-recall-with-zero-api-calls-too-good-to-be-true-bebcf26271d0"
author:
  - "[[Mandar Karhade]]"
  - "[[MD. PhD.]]"
published: 2026-04-08
created: 2026-04-20
description: "MemPalace By Mila Jovovich: 96.6% Recall With Zero API Calls (Too Good To Be True?) How a spatial memory system built on raw verbatim text is quietly outperforming every AI memory product on the …"
tags:
  - "clippings"
---
[Sitemap](https://ai.gopubby.com/sitemap/sitemap.xml)

[Mastodon](https://me.dm/@ithinkbot)

## [AI Advances](https://ai.gopubby.com/?source=post_page---publication_nav-3fe99b2acc4-bebcf26271d0---------------------------------------)

[![AI Advances](https://miro.medium.com/v2/resize:fill:76:76/1*R8zEd59FDf0l8Re94ImV0Q.png)](https://ai.gopubby.com/?source=post_page---post_publication_sidebar-3fe99b2acc4-bebcf26271d0---------------------------------------)

Democratizing access to artificial intelligence

## How a spatial memory system built on raw verbatim text is quietly outperforming every AI memory product on the market. For free.

**TLDR**

- MemPalace achieves 96.6% R@5 on LongMemEval with zero API calls, zero LLM in the retrieval loop, and zero subscription fees; the result has been independently reproduced on third-party hardware.
- The core thesis is radical and simple: store raw conversation text verbatim and let modern embeddings do the retrieval.
- No summarization, no extraction, no distillation. The signal stays intact.
- A five-stage hybrid retrieval pipeline layers keyword overlap, temporal boosting, and preference extraction on top of semantic search, pushing accuracy to 99.4% R@5 for under $0.001 per query.
- The spatial “palace” architecture organizes millions of tokens into navigable wings, rooms, halls, and tunnels; think of it as a file system for your AI conversation history.
- The open-source community stress-tested every claim, the authors corrected what needed correcting, and the project is stronger for it. This is collaborative intelligence at its best.

[**Free Link**](https://medium.com/ai-advances/mempalace-by-mila-jovovich-96-6-recall-with-zero-api-calls-too-good-to-be-true-bebcf26271d0?sk=d7f0810a1ba83fddc5732dcefc5fcc5d) for everyone: **Clap 50, Subscribe.** Follow the **publication**. Join Medium to support other writers too! Cheers

***Please subscribe to my new profile*** [***https://medium.com/@ThisWorld***](https://medium.com/@ThisWorld) *where I am covering* ***Health tech, Global tech, and AI Governance*** *through multi-part deep investigative articles.*

### Here’s a number that should make you stop scrolling.

96.6%.

> My Upfront Opinion. The Numbers look too good to be true…. That said, lets continue as this story has good things too.

That’s the Recall@5 score MemPalace achieves on LongMemEval, a 500-question benchmark designed to test whether a memory system can find the right conversation in a haystack of past sessions. Raw verbatim text. ChromaDB embeddings. No language model in the retrieval loop. No cloud calls. No API key.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*fGwWHIOLS3FbS8EgWmMOkQ.png)

For context, Mastra scores 94.87%. Hindsight lands at 91.4%. Supermemory in production hovers around 85%. Mem0, the system most people actually use? On ConvoMem with 75,000+ QA pairs, it manages 30 to 45%.

Those aren’t small gaps. In retrieval, the difference between 85% and 96.6% is the difference between “useful sometimes” and “I can actually rely on this.” In practical terms: 85% means roughly one in seven queries misses. 96.6% means maybe one or two misses per fifty questions.

But here’s the thing: The number isn’t even the interesting part. The *architecture* that produces it is.

## The Raw Text Thesis: Why Keeping Everything Wins

The core bet of MemPalace is almost embarrassingly simple. Don’t summarize. Don’t compress. Don’t distill. Just store the raw conversation verbatim and let modern embedding models handle retrieval.

This isn’t the usual incremental optimization. This flies in the face of what the entire AI memory industry has been building toward. Mem0, Zep, every LLM-based memory system assumes you need to extract, summarize, and compress conversations before storing them. The reasoning feels obvious: raw conversations are messy, full of filler, and expensive to search at scale.

### MemPalace says that reasoning is wrong.

And 96.6% R@5 with zero extraction says they might be right.

The insight is subtle but profound. Every time you summarize a conversation, you lose information. Maybe it’s a nuance in how the user phrased a preference. Maybe it’s a specific tool name mentioned in passing. Maybe it’s the temporal context of when something was discussed. Summarization is lossy compression applied to natural language, and those compression artifacts surface as retrieval failures downstream.

Think of it this way. You’re a tech lead managing three projects across Claude Code, ChatGPT, and Cursor. Six months in, you’ve accumulated thousands of conversation sessions.

Somewhere in month two, you discussed a database schema decision with your AI assistant. The exact reasoning, the tradeoffs you weighed, the specific migration approach you chose; it’s all in that conversation.

A summarization-based system would have distilled that into: “User decided on PostgreSQL for the backend database.”

### Technically correct But Useless Otherwise

Completely useless when you need to remember *why*, or what the rejected alternative was, or what edge case you were worried about.

> MemPalace kept the entire conversation. Raw. Verbatim. Every word. And when you search six months later, the embedding model finds it because the full signal is still there.

Raw verbatim storage preserves everything. The embedding model handles the semantic matching. ChromaDB handles the vector search. And because you never threw away the original signal, the retrieval has more to work with.

==This is the thesis: raw text with good embeddings is a stronger baseline than anyone realized, because it doesn’t lose information.==

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/0*96dEXrh9-B4PL5G-)

## Inside the Palace: A Spatial Architecture for AI Memory

The metaphor is charming, but the implementation is what matters. MemPalace organizes your conversation history into a spatial hierarchy inspired by the ancient memory palace technique:

### Wings

Are top-level categories: a project you’re working on, a person you collaborate with, a domain you’re learning about. Think of them as namespaces.

### Rooms

Sit inside wings. Each room represents a specific topic. A “Python Migration” room inside your “Backend” wing, for instance. The room detector uses pattern matching via `room_detector_local.py` to auto-classify incoming conversations.

### Drawers

Hold the actual content; your raw verbatim conversation files. Every conversation goes into a drawer, unmodified. This is where retrieval happens.

### Closets

Closets save summaries that point back to drawers. They exist for quick human scanning and navigation, not for retrieval accuracy. The retrieval engine hits drawers directly.

### Halls

Connect related rooms within the same wing. If your “Python Migration” room and your “Database Schema” room share context, a hall links them so BFS traversal in `palace_graph.py` can find multi-hop connections. **Tunnels** do the same thing across wings; linking, say, an "API Design" room in your collaborator's wing to the "Database Schema" room in your backend wing.

This hierarchy serves navigation, not retrieval accuracy. The authors have been transparent about this: the palace structure helps you *browse* 19.5 million tokens of conversation history. The retrieval accuracy comes from raw embeddings against drawer contents.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*mM1QWiG3YtnrIbJHCk1Bzg.png)

### The Knowledge Graph Layer

Underneath the palace sits a SQLite-based knowledge graph with temporal entity-relationships. Unlike Zep’s cloud-based Neo4j approach, MemPalace keeps everything local at zero cost.

The `entity_detector.py` module extracts entities from conversations; people, tools, projects; and `knowledge_graph.py` tracks relationships between them with validity windows. An entity relationship that was true in January might not be true in April. The temporal dimension matters.

The `entity_registry.py` module maps entities to short codes (more on this in the AAAK section below) and handles the bookkeeping of who-knows-what-about-whom across your entire conversation corpus.

### The Preference Wing

One of the more clever features: MemPalace maintains a dedicated preference wing populated at ingest time. Sixteen regex patterns in `general_extractor.py` scan incoming conversations for preference expressions and generate synthetic documents. "User has mentioned: prefers TypeScript over JavaScript; allergic to peanuts; uses vim bindings."

These synthetic preference docs become first-class searchable entities in ChromaDB. When a future query touches on preferences, the system can match against these concentrated signals rather than hoping the embedding finds the right sentence buried in a 2,000-word conversation.

## The Five-Stage Hybrid Retrieval Pipeline

Where MemPalace gets genuinely clever is the hybrid retrieval mode. The pipeline evolved through five documented versions, each adding a targeted fix for a specific class of retrieval failure. The progression is documented in meticulous detail in `HYBRID_MODE.md`, and it reads like an engineering postmortem in real time.

### Stage 1: Widen the Funnel (Baseline)

Raw mode retrieves ChromaDB’s top 10 results. The hybrid pipeline starts by widening this to top 50 candidates. More candidates means higher recall at the cost of precision; the subsequent stages handle the precision problem.

This baseline alone achieves 96.6% R@5. In practical terms, that means 483 out of 500 test questions return the correct conversation in the top five results. Seventeen misses.

### Stage 2: Keyword Overlap Re-ranking (v1, +1.2pp)

Semantic search is powerful but has a known blind spot: it can miss exact keyword matches. If you ask “What did I say about GraphQL?” and the relevant conversation uses the exact word “GraphQL” twelve times, a pure embedding search might still rank a semantically-similar-but-different conversation higher.

Hybrid v1 fixes this with a simple fused distance formula:

`fused_dist = dist × (1.0 − 0.30 × overlap)`

The system extracts non-stop-words from the query (filtering against 40+ stop words like “what”, “when”, “where”, “how”), computes keyword overlap with each candidate document, and reduces the distance score proportionally. Up to 30% distance reduction for strong keyword matches.

Result: 97.8% R@5.

Six more questions answered correctly. Six conversations that would have been lost, found.

### Stage 3: Temporal Date Boost (v2, +0.6pp)

Here’s a failure mode that only shows up in real-world usage: time-based questions. “What did we discuss a couple days ago?” “What was that thing from last week?”

Hybrid v2 parses temporal references using regex patterns for “N days ago”, “a couple days ago”, “last week”, “N months ago”, and “recently.” It computes a target date window and boosts documents that fall within it. Up to 40% distance reduction for temporally relevant results.

This also introduced two-pass retrieval for questions about what the AI assistant previously said. When the query contains triggers like “you suggested”, “you told me”, or “you recommended,” the first pass searches a user-turn-only index, then the second pass re-indexes the top 5 results with full conversation text (user + assistant turns).

Result: 98.4% R@5. The temporal boost alone recovered conversations that semantic search couldn’t find because the embedding doesn’t inherently encode “three days ago.”

### Stage 4: Preference Extraction (v3, +0.6pp)

The preference wing comes into play here. At ingest time, sixteen regex patterns extract preference expressions and create synthetic documents. At query time, the rerank candidate pool expands from top 10 to top 20, giving preference matches room to surface.

Result: 98.4% R@5 without LLM reranking. With Haiku reranking at ~$0.001 per query, this pushes to 99.4% R@5. Three missed questions out of 500.

### Stage 5: LLM Reranking (Optional, +1.0pp)

The final stage is optional and the only one that costs money. Claude Haiku receives the top 20 candidates and makes a semantic relevance judgment. At roughly $0.001 per query, it pushes the score from 98.4% to 99.4%.

The per-category breakdown at this stage is revealing: knowledge-update questions hit 100% (n=78). Multi-session questions hit 100% (n=133). Single-session-user questions hit 100% (n=70). Temporal reasoning reaches 99.2% (n=133). The weakest category is single-session-preference at 96.7% (n=30), likely because regex-based preference extraction can’t catch every expression style.

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*DqEgo_p8GKVrM8jyqEywFQ.png)

\\

## AAAK: The Compression Experiment That Didn’t Pan Out (Yet)

MemPalace ships a lossy symbolic summarization format called AAAK (the name is deliberately unexplained; the README says “Don’t ask; it’s a whole story of its own”).

It’s worth understanding what AAAK actually does, because the gap between its ambition and its current results illustrates exactly why the raw text thesis matters.

### AAAK compresses text by extracting five components:

### Entities

Entities get mapped to 3-character uppercase codes. “Alice” becomes “ALC”. “Bob” becomes “BOB”. These codes come from a configurable entity registry.

### Topics

These are the top-frequency content words after filtering through 150+ stop words, with boosts for proper nouns and CamelCase technical terms.

### A key sentence

Thse gets scored by decision keywords and length (the system prefers 40–80 character fragments), then truncated to 55 characters max.

### Emotions

Emotions are detected via keyword signals and mapped to 3–4 character codes from a library of 30+ emotions: “vul” for vulnerable, “determ” for determined, “convict” for conviction.

### Flags

Flags are like tags that mark importance: ORIGIN, CORE, SENSITIVE, PIVOT, GENESIS, DECISION, TECHNICAL.

The sentence output looks like: `ALC+BOB|GraphQL_REST|"chose GraphQL instead"|0.85|determ+convict|DECISION`

Any LLM can read this natively. No decoder required. The theory is that at scale, when entity codes like “ALC” replace “Alice” hundreds of times across a corpus, the token savings add up.

## But here’s the honest result.

On LongMemEval, AAAK mode scores 84.2% R@5 versus raw mode’s 96.6%. That’s a 12.4 percentage point regression. The information lost during summarization hurts retrieval more than the token savings help. And at small scales, the format actually *adds* tokens: the README’s own example compresses 66 tokens of English into 73 tokens of AAAK.

### The AAAK experiment is valuable even in failure.

It provides empirical evidence for the raw text thesis: when your compression is lossy, you lose retrieval accuracy. The question of whether AAAK’s entity-code approach pays off at truly massive scale (millions of repeated entity references) remains open. Issue #95 raised thoughtful concerns about hash collision fidelity in high-precision domains like legal and medical RAG. It’s a research direction, not a production feature.

## The Economics: $0.70 Per Year Versus $507

Here’s a number that doesn’t get enough attention.

MemPalace calculated the cost of running AI memory for six months of daily use, assuming 19.5 million tokens of conversation history. Using LLM-based summarization (the industry-standard approach), you’re looking at roughly $507 per year. Zep charges a subscription. Mem0 has a cloud tier.

### MemPalace’s wake-up cost?

$0.70 per year.

Not per month. Per *year*.

Add five searches per day and you’re at roughly $10 per year. Add optional Haiku reranking at $0.001 per query and you’re still under $15.

The cost difference isn’t marginal. It’s two orders of magnitude. And it comes from the same architectural decision that drives the retrieval accuracy: don’t use LLMs where you don’t need them. Store raw text. Use embeddings for search. Only invoke an LLM for that last 3% of accuracy.

For someone building a personal knowledge management system, or a small team running AI-assisted development, this is the difference between “affordable” and “free.”

## What This Means If You’re Building a Product

Say you’re running a 10-person engineering team, all using Claude Code or Cursor daily. After six months you’ve got tens of thousands of conversation sessions. The technical decisions, the debugging approaches, the architectural discussions; all of it lives in those sessions and is lost the moment the context window scrolls past.

### MemPalace mines those sessions into a searchable corpus.

A new engineer joins and asks “how did we decide on the database schema?” The answer is in a drawer somewhere, verbatim, retrievable at 96.6% accuracy.

No one had to write documentation. No one had to maintain a wiki. The conversations *are* the documentation.

The 19-tool MCP server makes this practical. One command: `claude mcp add mempalace -- python -m mempalace.mcp_server`. Your AI assistant now has access to your entire conversation history. You're debugging a production issue and you vaguely remember solving something similar three months ago. Instead of grep-ing through chat exports, your AI queries MemPalace, retrieves the relevant conversation verbatim, and picks up exactly where you left off.

For those who can’t afford the subscription to Mem0 or Zep’s cloud tiers, this is the entire value proposition of persistent AI memory, running locally, for free.

> This is my perspective. You should do what you are comfortable with. Also, this is my first run at MemPalace. I am a bit cringed by the terminology. I think that the implementation is very premitive.
> 
> But if it works, it works. I will be giving it a serious shot with OpenPDFLoader as my core pipleine (lookg forward to the article with coding).

## What the Community Found (and Why It Made the Project Better)

The GitHub issues page for MemPalace reads like a collaborative peer review. The community didn’t just file bugs; they stress-tested assumptions, reproduced benchmarks independently, and offered constructive analysis that improved the documentation and the code.

A few highlights worth noting:

### They did not count the real thing

User panuhorsmalahti (Issue #43) ran the AAAK compression example through OpenAI’s actual tokenizer and discovered the README’s token estimates used a `len(text)//3` heuristic instead of a real tokenizer. The community flagged it, the authors acknowledged it immediately, and the correction was incorporated into the README update.

### LoCoMo Ground Truth Contains Errors

User dial481 (Issue #29) filed a detailed methodological review of the benchmark claims, noting that the LoCoMo ground truth contains errors, that some code patches targeted specific test questions, and that the ConvoMem comparison mixed different evaluation metrics. These are the kinds of methodological observations that make published numbers trustworthy.

### Raw Itself Was 96% Accurate

This makes me happy as well as Sad at the same time. Its too high for me to trust that the raw text actually worked 96% better.

User gizmax (Issue #39) ran the full benchmark suite independently on an M2 Ultra Mac Studio. The raw 96.6% reproduced exactly.

### Lower Compression Ratio Due to AAAK

In under five minutes. On independent hardware. But gizmax also confirmed that AAAK compression ratios were lower than claimed and that room detection needed work. An independent reproduction that both validates the core result and identifies areas for improvement; that’s science working correctly.

### Many Other Community Contributions Are Active

Other community contributions include feature requests for `.mempalace-ignore` functionality (Issue #102), Gemini CLI integration (Issue #107), multi-hop traversal paths (Issue #101), and a proposal to rewrite in Zig for single-binary deployment (Issue #30). There's also a thoughtful discussion (Issue #104) about architectural similarities with the Sara Brain project, which touches on the broader question of convergent design in AI memory systems.

## Milla, Ben, and the Right Way to Correct Course

On April 7, 2026, Milla Jovovich and Ben Sigman published a correction note directly in the README. Not buried in a release note. Right at the top.

They clarified that token counting had used rough heuristics, that the 96.6% headline comes from raw mode (not AAAK), that the “+34% palace boost” was standard ChromaDB metadata filtering, and that contradiction detection wasn’t yet wired into the knowledge graph pipeline.

Their closing line: “We’d rather be right than impressive.” ❤

### That’s it. No spin.

This is how open source is supposed to work. The authors shipped something ambitious, the community provided rigorous feedback, and the response was transparent and immediate. Nobody was trying to tear anything down. Everyone was trying to make it better.

panuhorsmalahti didn’t file Issue #43 to attack MemPalace. They filed it because they wanted accurate documentation. dial481 wrote eight methodological observations because rigorous benchmarking makes the entire field more trustworthy. gizmax spent time on an independent reproduction because verifiable results matter.

This is the true form of OpenSource Community being open to trying, testing, accommodating, improving, and contributing.

This is collaborative intelligence. The authors bring the vision and the code. The community brings the scrutiny and the edge cases. The project evolves faster and more honestly than any closed-source alternative ever could. And at the end, what remains is a system that stores your conversations as-is, indexes them with modern embeddings, and retrieves them at 96.6% accuracy for zero dollars.

That’s a memory system that stands on its own.

If you have read it until this point, Thank you! You are a hero (and a Nerd ❤)! I try to keep my readers up to date with “interesting happenings in the AI world,” so please 🔔 clap | follow | Subscribe 🔔

[![AI Advances](https://miro.medium.com/v2/resize:fill:96:96/1*R8zEd59FDf0l8Re94ImV0Q.png)](https://ai.gopubby.com/?source=post_page---post_publication_info--bebcf26271d0---------------------------------------)

[![AI Advances](https://miro.medium.com/v2/resize:fill:128:128/1*R8zEd59FDf0l8Re94ImV0Q.png)](https://ai.gopubby.com/?source=post_page---post_publication_info--bebcf26271d0---------------------------------------)

[Last published 2 hours ago](https://ai.gopubby.com/youve-used-google-maps-a-million-times-here-s-the-wild-ai-behind-every-single-route-5b3c29ce29ec?source=post_page---post_publication_info--bebcf26271d0---------------------------------------)

Democratizing access to artificial intelligence

[![Mandar Karhade, MD. PhD.](https://miro.medium.com/v2/resize:fill:96:96/1*Z4yG0-xCzgmOcPZaI7a77Q.jpeg)](https://medium.com/@ithinkbot?source=post_page---post_author_info--bebcf26271d0---------------------------------------)

[![Mandar Karhade, MD. PhD.](https://miro.medium.com/v2/resize:fill:128:128/1*Z4yG0-xCzgmOcPZaI7a77Q.jpeg)](https://medium.com/@ithinkbot?source=post_page---post_author_info--bebcf26271d0---------------------------------------)

[153 following](https://medium.com/@ithinkbot/following?source=post_page---post_author_info--bebcf26271d0---------------------------------------)

I ideate, plan, and build. Independent AI consultant for Health & Legal Tech firms. Providing expert strategy, leadership, and complete engineering services.

## Responses (4)

Benedek Molnar

What are your thoughts?  

```c
This all assuming there is only one developer on one machine. Even as a solo developer, I code on different machines (with different GPUs and/or OSs) for the same project, so would need a central, not local, memory system.
```

6

```c
A biased competitor offers many points that should be considered by anyone (like me) lured to this fine article:

https://vectorize.io/articles/what-is-mempalace

My approach: Research *before* getting too excited about *anything*.
```

5[WhiteCaneGamer](https://w-c-g.medium.com/?source=post_page---post_responses--bebcf26271d0----2-----------------------------------)

[he/him](https://w-c-g.medium.com/?source=post_page---post_responses--bebcf26271d0----2-----------------------------------)

[

Apr 11

](https://w-c-g.medium.com/im-still-strugling-to-believe-those-numbers-db16a4a7ca29?source=post_page---post_responses--bebcf26271d0----2-----------------------------------)

```c
I'm still strugling to believe those numbers. I got excited, even installed the package, but... I think I'll let this one cook a bit and come back to it to see if it's everything it makes out to be... pip -m uninstall mempalace.
```

1