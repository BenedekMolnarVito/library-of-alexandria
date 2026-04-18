---
title: "DHH's new way of writing code"
type: source
domain: ai
tags:
  - dhh
  - agent-first-development
  - claude-code
  - opencode
  - ruby-on-rails
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/DHH's new way of writing code.md]]"
---

# DHH's new way of writing code

**Authors**: The Pragmatic Engineer
**Date**: 2026-04
**Type**: video-transcript

## Summary

A wide-ranging interview with David Heinemeier Hansson (creator of Ruby on Rails, CTO of 37signals) on his complete reversal from AI skeptic to agent-first developer after the Opus 3.5/4.5 inflection point in late November 2025. DHH describes how he now starts every task with an AI agent (OpenCode running Gemma K25 + Claude Code running Opus in parallel tmux panes), reserves code review rights, and how agent acceleration is changing the economics of small teams. The interview also covers Ruby on Rails, HEY email, Omarchy Linux, and the philosophy of software craft. DHH's perspective is particularly valuable as a practitioner who resisted AI tooling until he found a workflow that respected his aesthetic and judgment.

## Key Takeaways

- DHH's AI inflection point: Claude Opus 3.5/4.5 (late November 2025) — first model to consistently produce code he wanted to merge without alteration and remember style corrections
- His previous objection wasn't to AI capability but to autocomplete UX ('you won't let me finish a sentence') — the shift to agent harnesses with terminal interfaces resolved this
- Current workflow: tmux layout with Neovim (left), OpenCode + Gemma K25 (top right), Claude Code + Opus (bottom right) — starts every task agent-first, reviews with `git diff`, merges or iterates
- OpenCode is his primary harness (not Claude Code) because Anthropic made Opus subscription-exclusive to Claude Code, which DHH views as a strategic mistake
- Demonstrated with OpenClaw: gave it no tools, just a URL (fizzy.do), asked it to sign up — it autonomously created an account using Hey.com for email and introduced itself to the 37signals Basecamp team
- Ruby on Rails is token-efficient and well-suited for agent workflows — DHH sees a Renaissance for Rails in the agent era
- Agent acceleration favors small teams and senior developers with strong aesthetic taste — the Basecamp model (tiny team + strong design + craft) becomes more competitive, not less
- 37signals designers are full-stack: product manager + designer + HTML/CSS/Ruby implementer — agent acceleration amplifies this model further

## Entities Mentioned

- [[wiki/entities/david-heinemeier-hansson]]
- [[wiki/entities/37signals]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/basecamp]]
- [[wiki/entities/hey]]
- [[wiki/entities/omarchy]]
- [[wiki/entities/opencode]]
- [[wiki/entities/openclaw]]
- [[wiki/entities/toby-lutke]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/claude-opus]]

## Concepts Covered

- [[wiki/concepts/agent-first-development]]
- [[wiki/concepts/ai-inflection-point]]
- [[wiki/concepts/software-craft]]
- [[wiki/concepts/small-team-advantage]]
- [[wiki/concepts/ruby-on-rails]]
- [[wiki/concepts/token-efficiency]]
- [[wiki/concepts/agentic-workflows]]
- [[wiki/concepts/autonomous-agents]]

## Notable Quotes

> "Now I start with the agent. Now he'll give me the draft. I'll review the draft and I'll make alterations if need be."

> "Aesthetics is truth. When something is beautiful, it's likely to be correct."

> "Agent acceleration is going to empower designers to be more capable... The industry is coming a little towards our fundamental stance."

> "The combination of Claude Code agent harnesses + Opus 4.5 was the unlock — from 'this is interesting' to 'I will now start any project agent-first.'"

## Cross-Connections

DHH's preference for OpenCode over Claude Code mirrors NetworkChuck's preference for Claude Code over OpenClaw ([[wiki/sources/networkchuck-openclaw-right-now-review]]) — both are practitioners choosing different tools in the same emerging agent-harness category. His OpenClaw demo (signing up for services autonomously) connects directly to the [[wiki/sources/openclaw-10000-to-trade-stocks]] pattern of autonomous agents. The 'Ruby on Rails is token-efficient' claim connects to the broader Anthropic harness engineering context ([[wiki/sources/anthropic-harness-engineering-two-agent-architecture]]). His description of the November 2025 inflection point aligns with the Karpathy LLM wiki going viral around the same period ([[wiki/sources/karpathy-claude-md-file]]).
