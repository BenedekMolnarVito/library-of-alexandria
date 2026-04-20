---
title: "MemPalace — Give Your AI a Real Memory"
source: "https://rasha-salim.medium.com/mempalace-give-your-ai-a-real-memory-fbc43c5f7a6f"
author:
  - "[[Rasha Salim]]"
published: 2026-04-19
created: 2026-04-20
description: "MemPalace — Give Your AI a Real Memory There’s a problem nobody talks about enough when they talk about AI productivity: your AI forgets everything. Every new conversation, Claude, ChatGPT …"
tags:
  - "clippings"
---
[Sitemap](https://rasha-salim.medium.com/sitemap/sitemap.xml)

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Nm2JU2BFt1n7E4kYCmLRqw.png)

There’s a problem nobody talks about enough when they talk about AI productivity: **your AI forgets everything**.

Every new conversation, Claude, ChatGPT, whatever you’re using — it starts cold. No memory of what you decided last Tuesday. No idea why you switched frameworks. No recollection of the bug you spent three hours debugging. You rebuild context from scratch, every single time. And that costs you — in tokens, in time, and in the slow, grinding friction of re-explaining your own work to a tool that’s supposed to help you.

MemPalace is the fix. Not through fine-tuning. Not through embeddings. Not through some cloud service that needs an API key and bills you per query.

Just a structured, compressed, searchable memory system — local, fast, and built around how AI context windows actually work.

*If you don’t have a Medium account, feel free to read the full article via* [*this link*](https://medium.com/@rasha-salim/mempalace-give-your-ai-a-real-memory-fbc43c5f7a6f?sk=c5e6d6851bf135d955a967d6579769a0)*.*

## What Is a Memory Palace, Actually?

The term comes from an ancient mnemonic technique — the *method of loci* — where you mentally walk through a familiar building and place things you want to remember in specific rooms. The architecture gives you retrieval cues. You don’t try to remember everything at once; you remember *where things live*, then go there.

MemPalace maps this onto AI memory with three structural levels:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*DfHfvlz2mCLBPzmhWJujPA.png)

A palace contains wings (projects), which contain rooms (topics), which contain drawers (memories).

A **Wing** is a project. Your `my_app` codebase is a wing. Your chat history is a wing. Your notes are a wing.

A **Room** is a topic within that project — like `costs`, `auth`, `decisions`, `bugs`.

A **Drawer** is an individual compressed memory. One unit of recalled knowledge.

When your AI needs context, it doesn’t load the entire palace. It loads a **wake-up** — a curated L0 + L1 summary (~600–900 tokens) — and then reaches into specific drawers based on what’s relevant to the current conversation.

## The Cost Problem (And Why This Solves It)

Let’s be concrete. Say you have 200,000 tokens of project history — conversations, decisions, code context, notes. Stuffing all of that into every AI conversation is:

1. Impossible (most context windows cap out before that)
2. Expensive (you’re billed per token)
3. Counterproductive (more noise, worse signal)

MemPalace compresses memories using **AAAK Dialect**, a lossy compression format designed specifically for AI recall. The compression ratio is around **30x**. That same 200,000 tokens of raw context becomes ~6,700 tokens of structured, retrievable memory.

Here’s what that means in practice:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*73z_jwNo0s71tOfqJBqeSA.png)

Same project history, two ways of loading it. The bars are to scale.

You’re not just saving money. You’re reclaiming context window space for the thing that matters: the actual task.

## Getting Started

## 1\. Install

```c
pip install mempalace
```

Verify:

```c
mempalace --version
```

## 2\. Initialize Your Palace

Point it at a directory — a project folder, a notes vault, anything:

```c
mempalace init ~/projects/my_app
```

This detects your folder structure and maps it to wings and rooms. Nothing is mined yet — this just builds the skeleton.

## 3\. Mine Your Content

For a codebase, docs, or notes:

```c
mempalace mine ~/projects/my_app
```

For conversation exports (Claude, ChatGPT, Slack):

```c
mempalace mine ~/chats/claude-sessions --mode convos
```

If your conversation exports are one giant concatenated file, split them first:

```c
mempalace split ~/chats/
mempalace mine ~/chats/ --mode convos
```

## 4\. Check What Got Filed

```c
mempalace status
```

This shows wings, rooms, and drawer counts — your palace inventory.

## 5\. Search It

```c
mempalace search "why did we switch to GraphQL"
mempalace search "pricing discussion" --wing my_app --room costs
```

## 6\. Load Wake-Up Context

At the start of an AI session, generate your context primer:

```c
mempalace wake-up
# or for a specific project
mempalace wake-up --wing my_app
```

Paste this into your conversation. Your AI now has the skeleton of everything it needs to know, without burning 200k tokens to get there.

## The Mental Model (Visualized)

Here’s how it flows — from raw content to recalled knowledge:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*BXF6mzEY9BwhlFXVtsuMpg.png)

You control what gets loaded. Wake-up is the map. Search is the drawer. The palace stays local.

The key insight: **you control what gets loaded**. The wake-up gives the AI the map. Search gives it the specific room. You never load the whole palace at once.

## What MemPalace Is Not

This is where most people go wrong, so let’s be direct.

**It’s not a vector database.**  
There are no embeddings. No FAISS index. No semantic similarity search over high-dimensional vectors. The search is exact-word matching against compressed memories. That’s a feature, not a limitation — it’s predictable, fast, and requires zero infrastructure.

**It’s not a RAG pipeline.**  
RAG (Retrieval-Augmented Generation) retrieves documents and stuffs them into a prompt at query time. MemPalace is a memory architecture — it structures, compresses, and organizes knowledge so you can *choose* what to surface, not fire-and-forget retrieve it. You stay in the loop.

**It’s not a cloud service.**  
No API key. No account. No data leaving your machine. The palace lives in `~/.mempalace/` by default. You own the file system, you own the memories.

**It’s not a replacement for good prompting.**  
MemPalace gives you the *content*. You still need to give the AI good instructions on what to do with it. A well-structured wake-up context helps, but it doesn’t replace system prompts, task framing, or knowing what you want.

**It’s not magic recall.**  
It mines what you give it. If you never exported your conversations, they don’t exist in the palace. Garbage in, garbage out — but structured garbage in, structured garbage out.

## What MemPalace Actually Is

It’s a **local, structured, compressed memory system** for AI assistants.

The value proposition is simple:

- Mine your existing content (code, chats, notes) into a palace once
- Compress it ~30x so it fits in context windows without breaking the bank
- Load relevant context at session start (wake-up) or on-demand (search)
- Never re-explain your project history to an AI again

It fits into your workflow without changing it. You still use Claude, ChatGPT, or whatever. You just start sessions with a wake-up paste, and you search when you need a specific memory surfaced. The AI becomes genuinely context-aware — not because you gave it a 200k token dump, but because you gave it the right 800 tokens at the right time.

## A Note on Compression

AAAK Dialect compresses at ~30x, which means it’s lossy. You will lose some fidelity in the compressed form versus the raw source. That’s the trade-off.

But here’s the thing: **AI recall doesn’t need fidelity, it needs signal**. When you search for “why did we switch to GraphQL,” you don’t need the exact conversation transcript. You need the decision, the reasoning, and the outcome. That’s what survives compression. The noise doesn’t.

Think of it like how your own memory works. You don’t remember conversations verbatim. You remember the gist — and the gist is usually enough to reconstruct the detail when you need it.

## Practical Recommendations

**Mine your conversations regularly.** Set up a weekly habit: export, split, mine. Your palace gets richer over time.

**Use** `**--wing**` **filters on search.** Broad searches return noise. Scoped searches return signal.

**Start every AI session with a wake-up.** It’s 600–900 tokens. That’s nothing. But it orients the AI to your entire project context before you’ve typed a single question.

**Don’t mine everything blindly.** Be selective about what goes in. Raw logs, generated files, third-party docs you didn’t write — these dilute the palace with content that doesn’t reflect *your* decisions, *your* reasoning, *your* context.

## The Bigger Picture

The bottleneck in AI-assisted work isn’t intelligence. Modern models are genuinely capable. The bottleneck is **context** — getting the right information in front of the model, at the right time, without burning your budget on tokens that don’t move the needle.

MemPalace is one of the most direct solutions to that bottleneck I’ve seen. It’s small, local, zero-dependency, and it works with whatever AI you’re already using. No new accounts, no new APIs, no new infrastructure.

Give your AI a memory. Run `pip install mempalace` and see what it feels like to never re-explain your project from scratch again.

*MemPalace is open source. Install:* `*pip install mempalace*`