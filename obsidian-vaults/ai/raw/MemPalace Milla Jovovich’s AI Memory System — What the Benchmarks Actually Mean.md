---
title: "MemPalace: Milla Jovovich’s AI Memory System — What the Benchmarks Actually Mean"
source: "https://medium.com/@tentenco/mempalace-milla-jovovichs-ai-memory-system-what-the-benchmarks-actually-mean-1a3abe4490d8"
author:
  - "[[Ewan Mak]]"
published: 2026-04-11
created: 2026-04-20
description: "MemPalace: Milla Jovovich’s AI Memory System — What the Benchmarks Actually Mean Milla Jovovich has a GitHub account. The code she shipped actually works. Those two facts are doing more for …"
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

![](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*DctlPi6cjs8VaVYpEbFBWQ.jpeg)

Milla Jovovich has a GitHub account. The code she shipped actually works. Those two facts are doing more for MemPalace’s star count than any benchmark number.

The Resident Evil and Fifth Element actress open-sourced an AI memory system on April 5, 2026, under her own GitHub account (milla-jovovich/mempalace). MIT licensed, free to use. Within 48 hours it hit 7,000 stars. By the time Ben Sigman tweeted about it, the repo had crossed 10,000. As of this writing, it’s past 15,600 stars and 1,800 forks.

The question worth asking isn’t whether a Hollywood actress can ship software. It’s whether MemPalace solves a real problem, and whether the numbers hold up.

## Why This Project Exists

Jovovich started using ChatGPT and Claude heavily in late 2025 — thousands of conversations covering business decisions, creative projects, debugging sessions. Then she hit the wall every power user hits: start a new session, and the AI has amnesia. All that context, gone.

She tried Mem0 and Zep. Both use AI to decide what’s worth remembering. The reasoning and tradeoff discussions she actually needed were exactly what got discarded. She wanted something that kept everything and made it findable.

She found Ben Sigman, CEO of Libre Labs (a Bitcoin lending platform), and they spent months building MemPalace with Claude Code. Jovovich designed the architecture. Sigman handled the engineering.

## The Architecture: Store Everything, Then Structure It

Most AI memory systems extract summaries. Mem0 turns your conversations into facts like “user prefers Postgres” and throws away the conversation where you explained why.

MemPalace takes the opposite approach: store every word verbatim, then organize it so search actually works.

The organizational metaphor comes from the ancient Greek method of loci. Orators would mentally place ideas in rooms of an imaginary building, then walk through the building to recall them. MemPalace maps this to a concrete data structure:

Wings are top-level domains — a project, a person, a topic. Halls are memory types that repeat across every wing: facts, events, advice, emotional context. Rooms are specific subjects within a wing (auth, billing, deployment). Drawers hold the raw verbatim text. Closets hold compressed versions.

When the same room name appears in different wings, the system creates a “tunnel” connecting them — so “auth-migration” under your project wing links to “auth-migration” under a team member’s wing.

Under the hood it’s ChromaDB for vector storage and SQLite for a temporal knowledge graph. Two runtime dependencies: chromadb and pyyaml. Everything runs locally. No API keys, no cloud, no subscription.

## The Benchmarks: What 96.6% Actually Measures

This is where things get complicated.

MemPalace claims 96.6% on LongMemEval in raw mode (zero API calls) and 100% in hybrid mode (with Haiku reranking). Mem0 and Zep score around 85%.

The 96.6% number comes from “raw verbatim mode” — uncompressed conversation text stored in ChromaDB, retrieved via standard nearest-neighbor search. The palace structure (wings, rooms, halls) is not involved in this benchmark at all. An independent code analysis by lhl/agentic-memory concluded that this score measures ChromaDB’s default embedding model performance, not MemPalace itself.

The 100% number has bigger problems. An X Community Note on Sigman’s launch tweet states that the LongMemEval perfect score used targeted fixes for 3 failing questions plus LLM reranking, with a held-out score of 98.4%. The LoCoMo 100% used top\_k=50 against a candidate pool that maxes out at 32 sessions — meaning it retrieves everything and lets Claude Sonnet do reading comprehension. The vector retrieval step is bypassed entirely.

The benchmark runner only does retrieval. It never generates an answer, never invokes a judge. For each of the 500 LongMemEval questions, it checks whether any gold session ID appears in the top 5 results (recall\_any@5). It doesn’t verify that the retrieved sessions actually answer the question.

Penfield Labs published a detailed teardown and didn’t mince words: the variable producing the orders-of-magnitude difference in engagement compared to similar open-source memory projects “is not the engineering.”

To be fair: the team’s own BENCHMARKS.md (over 5,000 words) honestly discloses these methodology limitations. The problem is that the launch communication stripped the caveats. The 96.6% raw score, in the zero-API-cost category, is genuinely the highest published result. That’s real. The marketing around it isn’t.

## AAAK Compression: Interesting but Oversold

MemPalace includes a custom compression format called AAAK — aggressive abbreviation that any LLM can read without a decoder. The team claimed 30x compression with “zero information loss.”

Independent testing found that AAAK mode drops LongMemEval accuracy from 96.6% to 84.2% — a 12.4 percentage point quality loss. The token counting used `len(text)//3` instead of an actual tokenizer. The team acknowledged both issues in a README update, noting that AAAK doesn't save tokens at small scales and the example was misleading.

The decode function is string splitting, not text reconstruction. AAAK is lossy compression marketed as lossless.

## The 34% Retrieval Improvement

The team reports that narrowing search from all drawers to wing+room improves retrieval from 60.9% to 94.8% — a 34% gain.

This is metadata filtering. It’s a standard technique available in any vector database. Scoping your search to a specific project and topic will always beat searching everything. MemPalace’s contribution is providing an automated classification layer on top of this standard practice, not inventing the underlying technique.

## MCP Integration and Practical Usage

MemPalace ships an MCP server with 19 tools across five categories: palace reads, search, knowledge graph queries, diary/emotion logging, and system management.

Setup is one line:

```c
claude mcp add mempalace -- python -m mempalace.mcp_server
```

After that, Claude automatically calls mempalace\_search when relevant. It also works with Gemini CLI. For local models that don’t support MCP, a wake-up command loads ~170 tokens of key context.

The `PALACE_PROTOCOL` embedded in the status tool output instructs the AI to check MemPalace before answering questions about people — solid prompt engineering that reduces hallucination.

## Code Reality Check

The lhl/agentic-memory analysis found several gaps between documentation and implementation:

Everything lives in a single ChromaDB collection. Palace graph building scans all metadata in 1,000-item batches (O(n) per build). L1 loading is also O(n). No write gating — MCP’s add\_drawer inserts directly without confirmation. No input sanitization, creating a prompt injection surface. The knowledge graph does flat triple lookups, not multi-hop traversal. Halls exist as metadata strings but aren’t used in retrieval ranking.

None of this is unusual for a three-day-old project with 21 Python files. But some README claims describe features that don’t exist in the codebase yet.

## MemPalace vs. Mem0 vs. Zep

Mem0 has $24 million in funding, enterprise support, and starts at $19/month. Zep starts at $25/month. Both use LLM-based extraction to decide what’s worth keeping.

MemPalace is free, local, and stores everything verbatim. The philosophical split is “curated summaries” versus “store everything, search later.”

For privacy-conscious users or teams that don’t want to pay $19–25/month for memory, MemPalace is currently the only serious open-source option doing full local verbatim storage. But it has no enterprise support, no mature ecosystem, and code that’s three days old.

## The Celebrity Factor

The most honest take on MemPalace might be this: it’s a genuinely interesting architectural idea (spatial organization for AI memory), wrapped in aggressive benchmark marketing, amplified by celebrity novelty.

Brian Roemmele deployed it to 79 employees within days. The community found README errors within hours — and the team fixed them. Feature requests for Cursor integration, Windows support, and better onboarding are pouring in. The X Community has crossed 161 members.

But the gap between BENCHMARKS.md’s careful disclosures and the launch tweet’s headline claims is exactly the kind of thing that erodes trust in the open-source AI ecosystem. Every project on arXiv does it. That doesn’t make it fine.

## Who Should Care

If you run heavy AI workflows — daily Claude Code sessions, multi-week projects with dozens of conversations — the problem MemPalace targets is real. Every new session starts from zero, and that wastes time.

Whether to use it now depends on your tolerance for early-stage software. The install is `pip install mempalace`, the risk is low (your data stays local), and you can test it on a single project before committing. Don't expect the 96.6% benchmark to mean every query gets a perfect answer — that's not what it measures.

The more interesting question is whether the “store everything, structure it spatially” approach will prove better than “let AI extract what matters” as these systems mature. That’s still genuinely unresolved.

## Author Insight

Our team runs daily Claude Code workflows for OpenClaw deployments and client projects. The “AI amnesia” problem MemPalace targets is something we deal with constantly — reexplaining context across sessions burns real time. After reviewing the code analysis, we think MemPalace’s actual value right now is a well-organized metadata layer on top of ChromaDB vector search. That’s not nothing — good data organization has always been the unsexy thing that makes search work. But the benchmark marketing oversells what the palace structure currently does versus what ChromaDB’s embeddings do on their own. We’ll be watching the project’s evolution, particularly whether the palace hierarchy starts pulling its weight in actual retrieval benchmarks, not just marketing copy.

## FAQ

How is MemPalace different from Claude’s built-in memory?

Claude’s memory automatically extracts key facts and retains them across conversations, but you don’t control what it keeps or discards. MemPalace stores complete raw conversations and lets you search them with structured queries. They can work together — Claude’s memory for daily preferences, MemPalace for deep technical context.

Does MemPalace really cost nothing to run?

In raw mode, yes. The only dependencies are ChromaDB and PyYAML, both free. Vector embeddings use ChromaDB’s default local model. The optional hybrid mode with Haiku reranking costs about $0.001 per query, but it’s not required.

Does the palace structure actually improve search quality?

Yes, but the mechanism is metadata filtering — a standard vector database technique. Scoping search to a specific wing and room naturally improves precision. MemPalace’s contribution is automated classification into that structure, not the filtering technique itself.

Is AAAK compression safe to use? Does it lose information?

AAAK mode drops LongMemEval accuracy from 96.6% to 84.2%, so it’s not lossless despite the marketing claim. Raw verbatim text is always preserved in drawers. For accuracy-sensitive use cases, stick with raw mode search.

Should I start using MemPalace now?

If you have a Python environment and are comfortable with CLI tools, try it on a small project. `pip install mempalace` plus `mempalace init` and `mempalace mine` gets you started. Main risk is the project launched days ago, so expect rough edges. The upside is zero cost and fully local data.

[![Ewan Mak](https://miro.medium.com/v2/resize:fill:96:96/1*CK7i5eiljEq6abDJvMZPcQ.jpeg)](https://medium.com/@tentenco?source=post_page---post_author_info--1a3abe4490d8---------------------------------------)

[![Ewan Mak](https://miro.medium.com/v2/resize:fill:128:128/1*CK7i5eiljEq6abDJvMZPcQ.jpeg)](https://medium.com/@tentenco?source=post_page---post_author_info--1a3abe4490d8---------------------------------------)

[91 following](https://medium.com/@tentenco/following?source=post_page---post_author_info--1a3abe4490d8---------------------------------------)

Tech Lead at Tenten, driving product architecture, specializing in AI-native web experiences, AI Agent design, and scalable digital delivery for modern brands.