---
title: "Andrej Karpathy's Fix for AI Coding Agents Gone Wrong: A Single Markdown File"
type: source
domain: ai
tags:
  - claude-code
  - agent-reliability
  - prompt-engineering
  - karpathy
  - skill-md
created: 2026-04-27
updated: 2026-04-27
raw: "[[raw/Andrej Karpathy's Fix for AI Coding Agents Gone Wrong A Single Markdown File.md]]"
---

# Andrej Karpathy's Fix for AI Coding Agents Gone Wrong: A Single Markdown File

**Author**: Kristopher Dunham
**Published**: 2026-04-16
**Type**: Technical analysis / Pattern documentation

## Summary

AI coding agents have a personality problem: confident, fast, productive, but also sycophantic and prone to hallucination. Karpathy's solution: structure agent behavior in a single markdown file (CLAUDE.md or equivalent) that agents read before every turn. Instead of mega-prompts, use modular skill cards and guardrails that agents reference and update.

## Key Takeaways

- **Agents are sycophantic** — They agree, invent, and escalate without pushback
- **Single markdown file fix** — Agents read and follow structured guidelines per session
- **Skill cards over mega-prompts** — Each skill is documented, not baked into instruction
- **Guardrails are readable** — Constraints written plainly in markdown, not embedded in system prompt
- **Feedback loop** — Agents can update the markdown based on learned lessons

## Entities Mentioned

- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/claude-code]]

## Concepts Covered

- [[wiki/concepts/claude-md]]
- [[wiki/concepts/skill-md]]
- [[wiki/concepts/agent-reliability]]
- [[wiki/concepts/guardrails]]
- [[wiki/concepts/prompt-optimization]]

## Personal Notes

Elegant pattern. Uses markdown as the agent's "memory file" rather than a one-time prompt. References Forrest Chang's distilled version (60-line file with 3,500+ GitHub stars). Represents evolution from "perfect prompt" to "readable, updateable guidelines."
