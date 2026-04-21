---
title: "I Cut Claude Code's Output Tokens by 75%. Why Did Nobody Tell Me?"
type: source
domain: ai
tags:
  - claude-code
  - token-efficiency
  - cost-optimization
  - plugins
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/I Cut Claude Code’s Output Tokens by 75%. Why Did Nobody Tell Me.md]]"
---

# I Cut Claude Code's Output Tokens by 75%. Why Did Nobody Tell Me?

**Authors**: Alex Dunlop
**Date**: 2026-04
**Type**: article

## Summary

Alex Dunlop discovered and advocates for the 'Caveman' Claude Code plugin by Julius Brussee, which strips verbose filler language from Claude's responses and reduces output tokens by ~75%. Counterintuitively, a 2026 arxiv paper ('Brevity Constraints Reverse Performance Hierarchies in Language Models') found that brevity constraints actually improve benchmark accuracy by 26%. A companion tool, caveman-compress, rewrites CLAUDE.md for 45% token savings on input. The article challenges the common assumption that longer, more verbose LLM outputs indicate higher quality — in fact, the opposite appears to be true, and brevity constraints also happen to be cheaper.

## Key Takeaways

- Claude Code wastes tokens on filler phrases like 'Certainly', 'Sure, I'd be happy to help' — these cost real money
- Caveman plugin (13K+ GitHub stars) has three modes: lite, full, ultra; also has Classical Chinese mode for max compression
- Token test: same Unity UI bug fix — 1,252 tokens default vs. 410 tokens with caveman (67% reduction)
- arxiv paper 'Brevity Constraints Reverse Performance Hierarchies' shows brief responses are 26% more accurate — less verbose != worse
- caveman-compress rewrites CLAUDE.md into a compressed format (~45% input token savings)
- CLAUDE.md loads every session — input token savings compound across all sessions

## Entities Mentioned

- [[wiki/entities/alex-dunlop]]
- [[wiki/entities/julius-brussee]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/caveman-plugin]]
- [[wiki/entities/allen-iverson]]

## Concepts Covered

- [[wiki/concepts/token-efficiency]]
- [[wiki/concepts/output-token-reduction]]
- [[wiki/concepts/claude-plugins]]
- [[wiki/concepts/brevity-constraints]]
- [[wiki/concepts/claude-md-optimization]]
- [[wiki/concepts/cost-optimization]]

## Notable Quotes

> "Verbose answers aren't smarter, they are more expensive."

> "I think this should be the default, but more usage means more money for them."

## Cross-Connections

The caveman-compress tool directly reduces CLAUDE.md token costs, linking to the broader CLAUDE.md discussion in [[wiki/sources/karpathy-claude-md-file]]. The brevity finding challenges the common assumption that longer LLM outputs are higher quality — a key insight for anyone optimizing AI coding workflows. Pairs naturally with the token-efficiency discussions in [[wiki/sources/comparing-6-python-ai-agent-frameworks]]. The CLAUDE.md optimization also connects to the discovery in [[wiki/sources/claude-code-source-leaked-worth-learning]] that CLAUDE.md is reinserted on every turn change — making per-session savings compound multiplicatively.
