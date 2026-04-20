---
title: "From Hollywood to GitHub: Inside Milla Jovovich’s Radical AI Memory Revolution"
source: "https://shekhar14.medium.com/from-hollywood-to-github-inside-milla-jovovichs-radical-ai-memory-revolution-81d73a2650d1"
author:
  - "[[Aman Shekhar]]"
published: 2026-04-08
created: 2026-04-20
description: "From Hollywood to GitHub: Inside Milla Jovovich’s Radical AI Memory Revolution In a plot twist that feels ripped straight out of a high-octane science-fiction script, Milla Jovovich — the iconic …"
tags:
  - "clippings"
---
[Sitemap](https://shekhar14.medium.com/sitemap/sitemap.xml)

[Mastodon](https://me.dm/@shekhar14)

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*BDuhh1g3d-SCc8K5_DyP4A.png)

In a plot twist that feels ripped straight out of a high-octane science-fiction script, **Milla Jovovich** — the iconic actress best known for battling zombies in *Resident Evil* and embodying futuristic mystique in *The Fifth Element* — has stepped into one of the most complex frontiers in modern technology. Far from just lending her celebrity name to a marketing campaign, Jovovich has co-created a tool called **MemPalace**, an open-source AI memory system designed to fix what she identifies as one of artificial intelligence’s biggest fundamental weaknesses: “amnesia”.

Launched in early April 2026, MemPalace has exploded across developer circles with the kind of viral energy usually reserved for summer blockbusters. Within mere days of its debut, the project racked up over **10,000 GitHub stars** and dozens of pull requests, signaling a massive wave of both awe and skeptical hype. But underneath the celebrity sheen lies a radical shift in how we think about AI context, long-term storage, and the intersection of ancient human mnemonic techniques with cutting-edge code.

**The Genesis of a Tech Revolution: Why Leeloo is Coding at Night**

The origin story of MemPalace is one of **frustration turned into obsession**. According to Jovovich, her transition from Hollywood star to tech co-creator began when she started using AI tools intensively for a personal, unnamed gaming project. Like anyone who has tried to use modern chatbots for long-term, complex work, she quickly hit a wall.

The problem, familiar to serious users of LLMs (Large Language Models), is that **AI starts every new session from zero**. Context disappears, carefully built knowledge resets, and strategic decisions vanish as if they never existed. Jovovich found that existing “memory” features in popular AI tools were insufficient because they typically involve the AI deciding what is “valuable” to keep and discarding the rest to save on expensive cloud storage.

“AI only knows what’s already been done,” Jovovich remarked in a video address. “It’s the humans running it that actually create something unique and different”. Refusing to accept the limitation of context-loss, she teamed up with **Ben Sigman**, a software engineer and CEO of the Bitcoin lending platform Libre Labs, to design a system that wouldn’t just remember more, but **remember differently**.

**What the Actress Created: A Detailed Look at the MemPalace Architecture**

MemPalace is not a traditional database; it is a **spatial, explorable memory system** built on the belief that memory is the foundation of true intelligence. Jovovich and Sigman utilized **Anthropic’s Claude Code** as a primary development tool to translate her conceptual vision into a working software architecture.

1\. The Method of Loci: Ancient Logic, Modern Code

The most striking feature of MemPalace is its philosophical foundation: the **Method of Loci**, or the “Memory Palace”. This is a 2,500-year-old mnemonic technique used by ancient Greek orators to memorize entire speeches by mentally placing pieces of information in specific locations within a familiar building.

MemPalace translates this idea into a digital architecture. Instead of flat data, it organizes information into a navigable structure of **“wings,” “rooms,” and “halls”**.

- **Wings:** Represent high-level topics or projects (e.g., Engineering, Marketing, Design).
- **Rooms:** Contain sub-topics or specific conversation clusters.
- **Drawers/Halls:** Further categorize specific ideas or memory types.

2\. Local-First Philosophy

In a direct rebellion against an industry dominated by paywalled, server-dependent services, MemPalace **runs entirely on the user’s device**. It requires no cloud connection, no API keys for its core functions, and no subscription fees. This “local-first” approach ensures that data processing stays on-device, offering a level of **privacy and data sovereignty** that cloud-synced memory (used by OpenAI or Google) cannot match.

3\. The Technical Stack

The “engine” under the hood of MemPalace utilizes a combination of open-source infrastructures:

- **ChromaDB:** Used for vector storage and semantic search, allowing users to find memories by meaning rather than just keywords.
- **SQLite:** Powers a **temporal knowledge graph** that tracks relationships between facts, including “validity windows” (valid\_from and valid\_to dates) so that facts can expire or be updated over time.
- **Embeddings:** It uses the `all-MiniLM-L6-v2` model to generate semantic embeddings of conversations.
- **MCP (Model Context Protocol):** MemPalace includes integration for **19 different tools** via the MCP standard, allowing it to connect seamlessly to AI interfaces like Claude, Cursor, and ChatGPT.

4\. The AAAK Compression Dialect

One of the more experimental aspects of the creation is the **AAAK compression dialect**. Jovovich and Sigman initially marketed this as a “lossless” language only AI could understand, claiming it could pack repeated entities into 30 times fewer tokens. While its “lossless” status was later challenged by the developer community, the goal remains the same: to reduce the “token load” when feeding massive amounts of history back into an AI’s context window.

**The Benchmark War: Claims of Perfection Meet Cold Reality**

The viral surge of MemPalace was fueled by a headline-grabbing claim: it achieved **“perfect scores”** on industry-standard benchmarks. Sigman posted on X that the system posted a perfect 500/500 on **LongMemEval**, a benchmark evaluating information extraction, reasoning, and knowledge updates.

However, the developer community was quick to scrutinize these numbers. Skeptics and rival researchers pointed out several methodology issues:

- **“Teaching to the Test”:** Analysts found that the 100% score on LongMemEval was achieved using **targeted fixes** for the specific questions the model had previously failed, rather than general algorithmic improvements.
- **The LoCoMo Loophole:** The claim of 100% on the LoCoMo benchmark was criticized because it used a `top_k=50` setting against a dataset where the maximum session count was only 32. This meant the system effectively dumped the entire conversation history into the AI for reading comprehension, bypassing the "retrieval" challenge entirely.
- **The Honest Score:** Under pressure, Sigman updated the scores to reflect a **96.6% recall** in raw mode. Remarkably, even this “honest” score still outperforms major paid competitors like Mem0 and Zep, which typically hover around 85%.

**The Human Mystery: Who is “Lu”?**

While Jovovich and Sigman are the public faces of the project, a technical controversy has emerged regarding the primary coder. Critics who dug into the GitHub repository noticed that many files and benchmark notes were attributed to a developer named **“Lu” (also known as Lumi or DTL)**.

Some skeptics argue that Lu is the sole actual coder behind the implementation, while the GitHub repository was published under Jovovich’s name with a “squashed” commit history to emphasize her involvement. There is even playful speculation that “Lu” might be an **AI agent** used during development — an ironic possibility given the project’s goal of advanced AI collaboration. Despite this, Jovovich’s supporters argue that her role as the architect and conceptual designer is what brought a “refreshing perspective” to a stagnant field.

**Why MemPalace Matters: Beyond the Hype**

For the average user or a bootstrapped startup, MemPalace represents a **rare break from the corporate-dominated AI ecosystem**. In Europe, where GDPR compliance is non-negotiable, a memory system that keeps sensitive business conversations on a local machine rather than a third-party cloud is a game-changer.

MemPalace challenges the core assumption that AI memory must be a “filtered summary”. Most tools aggressively summarize, deciding what you *might* need later and throwing the rest away. MemPalace flips this logic: **nothing is forgotten, only reorganized**. By storing everything verbatim, it allows the AI to retrieve the exact context of a decision made months ago, such as “why we chose JWT over sessions”.

**How to Build Your Own Palace: A Practical Guide**

For those looking to step into Jovovich’s creation, the process is designed to be surprisingly accessible.

1. **Installation:** The tool is available via `pip install mempalace` for users with Python 3.9 or later.
2. **The “Mine” Step:** Users can export their existing data from ChatGPT, Claude, or Slack. The MemPalace “mining” mode then parses these JSON files and generates semantic embeddings.
3. **Visualization:** The tool organizes these conversations automatically into the Wing/Room structure, allowing you to browse your “palace” visually or search 1,000 chats in 0.1 seconds.
4. **Connecting the AI:** By adding a single MCP URL to a tool like Claude or Cursor, your AI assistant suddenly has access to your entire historical library of ideas.

**The Verdict: A New Paradigm for Human-AI Collaboration**

Whether MemPalace is a technical masterpiece or a “polished promotional” experiment remains a subject of debate in developer forums. However, the project has undeniably succeeded in **reframing memory as the foundation of intelligence**.

Milla Jovovich has demonstrated that the boundaries between science-fiction storytelling and real-world AI development are blurring. By reaching for a 2,500-year-old human solution to solve a modern “technological amnesia,” she has provided a tool that — benchmarks aside — is **genuinely useful for anyone** trying to build a consistent, long-term relationship with an AI assistant.

As the AI industry continues its high-stakes global race, MemPalace stands as a reminder that the most powerful “context window” isn’t just an algorithm — it’s the structured history of our own human ideas. **In the world of MemPalace, your AI doesn’t just process your words; it lives in the rooms you built for it**.

If you enjoy learning through real-world problem solving, I’ve got something for you 🚀

I regularly solve LeetCode problems and break them down in a way that’s easy to understand — focusing not just on the solution, but the thinking process behind it. Alongside that, I also share insights and practical knowledge around AI, helping you stay ahead in this fast-moving space.

This article is also covered in detail on my YouTube channel, where I walk through concepts step-by-step so you can follow along and build confidence.

If this kind of content helps you, consider supporting the journey:  
👍 Like the video  
💬 Share your thoughts or questions  
🔔 Subscribe for more content on DSA, system thinking, and AI

Let’s grow and learn together.

[![Aman Shekhar](https://miro.medium.com/v2/resize:fill:96:96/1*2nw6c7lC7UR7QgyvLGjOww.png)](https://shekhar14.medium.com/?source=post_page---post_author_info--81d73a2650d1---------------------------------------)

[![Aman Shekhar](https://miro.medium.com/v2/resize:fill:128:128/1*2nw6c7lC7UR7QgyvLGjOww.png)](https://shekhar14.medium.com/?source=post_page---post_author_info--81d73a2650d1---------------------------------------)

[264 following](https://shekhar14.medium.com/following?source=post_page---post_author_info--81d73a2650d1---------------------------------------)

Mobile App Developer by profession, a Chess Player by heart, and an Aspiring Author by ambition.