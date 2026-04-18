---
title: "What Is Andrej Karpathy’s CLAUDE.md File?"
source: "https://medium.com/the-ai-studio/what-is-andrej-karpathys-claude-md-file-7ca12ef0ecec"
author:
  - "[[Ai studio]]"
published: 2026-04-07
created: 2026-04-18
description: "Discover how Andrej Karpathy’s CLAUDE.md file improves Claude Code workflow, reduces coding errors, and boosts AI developer productivity."
tags:
  - "clippings"
---
## [The Ai Studio](https://medium.com/the-ai-studio?source=post_page---publication_nav-6d3ee42fb4b2-7ca12ef0ecec---------------------------------------)

[![The Ai Studio](https://miro.medium.com/v2/resize:fill:48:48/1*Vn-bNX34w5L-7AtkV1R9yA.jpeg)](https://medium.com/the-ai-studio?source=post_page---post_publication_sidebar-6d3ee42fb4b2-7ca12ef0ecec---------------------------------------)

A publication for all AI creators with AI-related articles covering AI art, coding, biases, ethics, new tools, and tutorials.

## And Why 10,000+ Developers Downloaded It

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Kz-4V_i7uxB6sSuo4q8eQA.png)

Image created by Author using Gemini AI

Read here for [FREE](https://medium.com/@coustom.no.03/7ca12ef0ecec?sk=aa9d43f08b172aa8d66cde1ceea9eba3)

In November 2025, Andrej Karpathy was still writing most of his code by hand. By December, he wasn’t.

In a widely-shared post from January 2026, he described a shift that took just a few weeks: from 80% manual coding to 80% agent-driven coding using Claude Code.

He called it the biggest change to his workflow in roughly two decades of programming.

Not a gradual drift. A phase shift.

That post sparked a lot of discussion.

But buried inside it was something smaller and more practical than the big claims about AI and the future of software engineering.

He mentioned a file.

A plain markdown file called CLAUDE.md. And the way he talked about it, both what it was supposed to fix and what it still couldn’t, turned out to matter more than most people noticed.

## What CLAUDE.md Actually Is

CLAUDE.md is a configuration file for Claude Code, Anthropic’s terminal-based coding agent.

You place it in the root of your project, and Claude Code reads it automatically at the start of every session. It becomes part of the model’s working context before any conversation begins.

Think of it as a standing instruction document.

You write down the things you’d otherwise have to explain from scratch every time: how tests are run, what the folder structure means, what naming conventions the codebase uses, what the model should never touch. Claude reads it, and you don’t repeat yourself.

It’s a markdown file. Plain text. No special syntax.

It can live in your project root for the whole team, or in a personal config folder that applies across all your projects. You can have multiple CLAUDE.md files in different subdirectories, and Claude will apply whichever one is closest to the code it’s working on.

That’s the basic mechanism. But the file Karpathy mentioned, and the one 10,000+ developers went looking for, isn’t really about folder structure and test commands.

## The Problem It Was Built to Solve

Karpathy’s January 2026 post wasn’t just about productivity gains. A significant part of it was a specific list of the ways LLMs fail when writing code, and they’re worth reading carefully because they’re not vague.

The problems he identified:

- Models make wrong assumptions and keep going without checking
- They don’t flag when they’re confused, don’t surface tradeoffs, don’t push back
- They overcomplicate things by default, bloating 100-line solutions into 1000
- They touch code adjacent to the task that they don’t fully understand
- They don’t clean up dead code after themselves

These aren’t rare edge cases.

Anyone who has used Claude Code or Cursor for more than a few sessions recognizes all of them. You ask for a small change. You get back a diff that touches six files.

You spend the next 20 minutes auditing code you didn’t ask to change.

The frustrating thing is that these mistakes are predictable. They happen the same way, over and over. And that predictability is exactly what a configuration file can address.

## The Karpathy-Inspired File That Spread

A developer named Forrest Chang took Karpathy’s observations and turned them into a single, downloadable CLAUDE.md file, published on GitHub under the repository andrej-karpathy-skills.

The file doesn’t try to do everything. It encodes four principles, and only four:

### Don’t assume. Don’t hide confusion. Surface tradeoffs.

If the model is uncertain, it should ask. If multiple interpretations exist, it should name them instead of picking silently. If a simpler approach exists, it should say so. This principle is a direct response to the silent-assumption problem Karpathy described.

### Minimum code that solves the problem. Nothing speculative.

No features beyond what was asked. No abstractions built for single-use code. No flexibility that wasn’t requested. The internal test: would a senior engineer call this overcomplicated? If yes, simplify.

### Touch only what you must. Clean up only your own mess.

Don’t improve adjacent code, don’t reformat things that weren’t part of the task, don’t delete comments the model doesn’t understand. Every changed line should trace directly to what was actually requested.

### Define success criteria. Loop until verified.

Instead of telling the model what to do step by step, describe what done looks like. LLMs are better at iterating toward a goal than following a rigid procedure. Give it a test to pass. Let it loop.

That’s the whole file. Sixty-odd lines.

The repository got more than 3,500 GitHub stars. A VS Code and Cursor extension was built from it. A SourceForge mirror appeared. Medium posts explained it. Developers started dropping it into their own projects with a single curl command.

## Why It Connected

Part of what made the file spread is that Karpathy’s original observations were specific and honest.

He wasn’t selling anything.

He was describing what he actually noticed, including the uncomfortable parts: that he’d started to feel his manual coding ability atrophying, that telling an AI what to write felt strange, that despite using CLAUDE.md, the problems didn’t fully go away.

That last part is worth sitting with.

Even Karpathy admitted, in a later post, that he hadn’t figured out a good way to keep his CLAUDE.md up to date.

The file helps. It doesn’t solve everything.

For developers, that honesty made the advice feel trustworthy in a way that productivity-hype articles don’t.

He wasn’t describing a perfect system.

He was describing a real workflow with real friction, and the file was one practical response to one specific category of friction.

The four principles also landed because they match what developers were already observing on their own. The problems Karpathy named aren’t theoretical. The cleanup passes after AI-generated code, the extra abstractions that crept in, the comment that vanished when the model wasn’t sure what it meant. These happen. Putting rules in a file doesn’t eliminate them, but it reduces them, and reduction is enough to make a difference in a daily workflow.

## What’s Actually Inside, and How to Use It

The simplest way to use the Karpathy-derived file is a single command in your terminal:

```c
curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md
```

This drops the file into your current project directory. Claude Code picks it up automatically the next time you start a session.

If you already have a CLAUDE.md, you can append instead of replace:

```c
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md >> CLAUDE.md
```

The file is designed to be a starting point, not a final version.

The recommendation from multiple developers who’ve used it: add your project-specific conventions below the Karpathy principles, and remove anything that doesn’t apply to how you actually work. A CLAUDE.md that’s 200 lines long and covers everything theoretically is less useful than one that’s 60 lines and genuinely accurate.

One practical constraint worth knowing: every line in CLAUDE.md competes with actual work for space in the model’s context window. Frontier models can follow roughly 150 to 200 instructions with reasonable consistency, but Claude Code’s own system prompt already uses about 50 of those before your file is even loaded. Shorter is better.

## What It Doesn’t Fix

The Karpathy file will reduce overengineering and cut down on silent assumptions. It won’t make the model perfect, and it won’t keep itself updated as your project evolves. Karpathy said as much.

The more honest framing: CLAUDE.md is a way of encoding the corrections you’d make anyway.

Instead of catching the same class of mistake on every session and explaining the fix each time, you write it once and it applies automatically. The cleanup pass still happens sometimes. It just happens less.

Whether that’s worth it depends on how often you’re using Claude Code and how much the repeated friction costs you. For developers who are already spending most of their day in an agent workflow, the answer is usually yes.

The file spread because the problem it addresses is real, the solution is small enough to actually use, and the source was someone who had no reason to oversell it.[AI](https://medium.com/tag/ai?source=post_page-----7ca12ef0ecec---------------------------------------)[Claude](https://medium.com/tag/claude?source=post_page-----7ca12ef0ecec---------------------------------------)[Technology](https://medium.com/tag/technology?source=post_page-----7ca12ef0ecec---------------------------------------)[Coding](https://medium.com/tag/coding?source=post_page-----7ca12ef0ecec---------------------------------------)[DevOps](https://medium.com/tag/devops?source=post_page-----7ca12ef0ecec---------------------------------------)

[![Ai studio](https://miro.medium.com/v2/resize:fill:60:60/1*Vn-bNX34w5L-7AtkV1R9yA.jpeg)](https://medium.com/@coustom.no.03?source=post_page---post_author_info--7ca12ef0ecec---------------------------------------)[53 following](https://medium.com/@coustom.no.03/following?source=post_page---post_author_info--7ca12ef0ecec---------------------------------------)

Reader, Passionate about AI, Youtube Channel -. [https://youtube.com/@ai.studio0?si=F8vBH-X-yqIA-b7J](https://youtube.com/@ai.studio0?si=F8vBH-X-yqIA-b7J)

## Responses (1)

Benedek Molnar

What are your thoughts?

```ts
If you already have a CLAUDE.md in your user's folder, I would recommend doing this:\`\`\`bashcd $(mktemp -d -p $HOME)claude plugin install claude-md-management@claude-plugins-officialmkdir -p ~/.claude/rulescurl -fsSL -o…
```

4

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--7ca12ef0ecec-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)