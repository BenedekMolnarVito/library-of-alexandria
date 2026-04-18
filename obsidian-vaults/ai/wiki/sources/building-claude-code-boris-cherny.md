---
title: "Building Claude Code with Boris Cherny"
type: source
domain: ai
tags:
  - claude-code
  - ai-assisted-coding
  - developer-tools
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Building Claude Code with Boris Cherny.md]]"
---

# Building Claude Code with Boris Cherny

**Authors**: The Pragmatic Engineer (Gergely Orosz)
**Date**: 2026-03
**Type**: video-transcript

## Summary

The Pragmatic Engineer interviews Boris Cherny, creator and Head of Claude Code at Anthropic, about his background (TypeScript book author, 7 years at Meta across Facebook/Instagram/WhatsApp/Messenger), how Claude Code grew from a side project to one of the fastest-growing developer tools, and his view of the current AI-coding moment. Boris describes writing 20-30 PRs per day with zero handwritten code, argues for a 'printing press' metaphor for the current moment (scribes become authors, the category expands), and discusses what changed when his first PR at Anthropic was rejected — not because the code was bad, but because he wrote it by hand.

## Key Takeaways

- Claude Code now writes ~80% of Anthropic's own code; Boris ships 20-30 PRs per day with Claude writing 100% of each — not a single line manually edited.
- Boris's first PR at Anthropic was rejected not for code quality but for being handwritten — signaling how thoroughly AI-first coding is embedded in Anthropic's culture.
- Printing press metaphor: scribes became writers/authors as the market for literature expanded massively. Similarly, programmers won't disappear — the category will expand as the market for software expands.
- Andrej Karpathy posted 'he's never felt as far behind as a programmer as he is now' — the model improvement rate is outpacing practitioners' ability to update their workflows.
- Boris's philosophy: engineering has always been practical for him — generalist by nature, focused on outcomes not technology. This shaped Claude Code's design as outcome-focused tooling.
- Meta career arc: Facebook Groups → Instagram → Messenger → led code quality across all Meta apps. Identified Instagram's Python/Django stack as extremely inefficient compared to Facebook's Hack/HHVM/GraphQL/React stack.
- Claude Code grew from a personal side project to the fastest-growing dev tool at Anthropic, with internal debate about whether to release it externally at all.
- Key engineering insight from Meta: migrations (Python→monolith, REST→GraphQL) are a perfect use case for AI coding tools — they're now dramatically faster.

## Entities Mentioned

- [[wiki/entities/boris-cherny]]
- [[wiki/entities/gergely-orosz]]
- [[wiki/entities/the-pragmatic-engineer]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/meta]]
- [[wiki/entities/andrej-karpathy]]

## Concepts Covered

- [[wiki/concepts/ai-assisted-coding]]
- [[wiki/concepts/printing-press-metaphor]]
- [[wiki/concepts/code-review-with-ai]]
- [[wiki/concepts/developer-tools]]
- [[wiki/concepts/product-engineering]]
- [[wiki/concepts/typescript]]
- [[wiki/concepts/graphql]]
- [[wiki/concepts/codebase-migration]]

## Notable Quotes

> "Opus 4.5 and Claude Code wrote 100% of every single one [PR]. I didn't edit a single line manually."

> "The model is improving so quickly that the ideas that worked with the old model might not work with the new model."

> "There was a group of scribes that knew how to write... if you think about what happened to the scribes, they ceased to become scribes, but now there's a category of writers and authors. These people now exist. And the reason they exist is because the market for literature just expanded a ton."

> "What happens when you join one of the top AI labs in the world and your first pull request gets rejected? Not because the code was bad, but because you wrote it by hand."

## Cross-Connections

Essential companion to [[wiki/sources/100-hours-claude-code-vs-antigravity]]; Boris's 'printing press' metaphor pairs with [[wiki/sources/chip-huyen-building-when-nothing-left-to-build]]'s existential question about building when anything can be copied. The zero-handwritten-code workflow is a live demonstration of the [[wiki/concepts/karpathy-loop]] at the organizational level. His Meta migration experience ties to [[wiki/sources/best-llms-opencode-qwen-gemma-tested-locally]] (migrations as ideal AI use case). The LLM Wiki pattern in [[wiki/sources/karpathy-llm-wiki-pattern-rag]] relies on Claude Code as its primary execution engine.
