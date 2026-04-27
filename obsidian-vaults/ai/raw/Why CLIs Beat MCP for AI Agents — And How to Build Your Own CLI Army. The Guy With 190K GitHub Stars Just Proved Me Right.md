---
title: "Why CLIs Beat MCP for AI Agents — And How to Build Your Own CLI Army. The Guy With 190K GitHub Stars Just Proved Me Right."
source: "https://medium.com/@rentierdigital/why-clis-beat-mcp-for-ai-agents-and-how-to-build-your-own-cli-army-6c27b0aec969"
author:
  - "[[Phil | Rentier Digital]]"
published: 2026-02-17
created: 2026-04-27
description: "“mcp were a mistake. bash is better.”"
tags:
  - "clippings"
---
## “mcp were a mistake. bash is better.”

Six words. Thats what Peter Steinberger — the guy behind OpenClaw, 190,000 GitHub stars, [freshly recruited by Sam Altman](https://medium.com/@rentierdigital/peter-steinberger-chose-openai-over-meta-fe8433cda551?sk=4aa8dc8ff3d7133a0a82475a180e9e1d) — posted on X last month. And my immediate reaction was to screenshot it and send it to three dev friends with “ **TOLD YOU SO** ” in all caps.

I’ve been building on Ubuntu for years.

Every tool I use daily is a CLI.

Supabase CLI, Vercel CLI, Docker, git, n8n — my entire stack runs from a terminal. When MCP servers started trending last year, I tried a few. They worked. They also ate 40% of my context window, crashed randomly, and added a dependency for something I could already do with a one-liner and a pipe.

So when the most prolific open-source dev of 2026 says CLIs are the real interface between AI agents and the world — and OpenAI agrees enough to hire him — maybe it’s time to pay attention.

> **TL;DR:** MCP servers bloat your context window, add fragile dependencies, and solve a problem that doesn’t exist if your tools are CLIs 😂 Peter Steinberger built ~10 custom CLIs for OpenClaw, got recruited by OpenAI for it.
> 
> You can use the same pattern with Claude Code today (document CLIs in CLAUDE.md), plug them into OpenClaw as skills, or build your own autonomous agent with the…