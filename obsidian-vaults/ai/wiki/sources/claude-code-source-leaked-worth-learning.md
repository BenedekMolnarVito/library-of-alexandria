---
title: "Claude Code's Source Got Leaked. Here's What's Actually Worth Learning."
type: source
domain: ai
tags:
  - claude-code
  - anthropic
  - memory-architecture
  - multi-agent
  - leaked-source
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Claude Code’s Source Got Leaked. Here’s What’s Actually Worth Learning.md]]"
---

# Claude Code's Source Got Leaked. Here's What's Actually Worth Learning.

**Authors**: Pawel Jozefiak
**Date**: 2026-04
**Type**: article

## Summary

On March 31, 2026, a missing `.npmignore` entry caused Claude Code's 512K-line TypeScript source to accidentally leak via an npm source map. Pawel Jozefiak, who runs a 24/7 Mac Mini AI agent, read the entire codebase overnight and extracted five actionable architectural patterns: three-layer skeptical memory, autoDream consolidation, file-read deduplication, multi-agent coordinator mode with prompt cache sharing, and three-tier risk classification. He built five modules from these patterns the same night. This article is one of the most technically dense sources in the vault, providing ground-truth implementation details for architectural concepts that other sources describe from the outside.

## Key Takeaways

- How it leaked: Bun (Claude Code's runtime) generates source maps by default; someone forgot to add `*.map` to .npmignore; the map referenced unobfuscated TypeScript on Anthropic's Cloudflare R2 bucket — 1,900 files, 512K lines, mirrored to GitHub in hours (84K stars in under 2 hours — fastest-growing repo in history)
- Three-layer memory: Core index (MEMORY.md, <150 chars per entry, always loaded), topic files (fetched on-demand), raw transcripts (never re-read in full, only grep'd). 'Skeptical memory' — agent verifies against codebase before acting on remembered facts
- autoDream: background memory consolidation daemon forked as read-only subagent, runs when: 24h since last run + 5+ sessions completed + consolidation lock available. Four phases: orient → gather → consolidate → prune (keeps total memory under 200 lines / 25KB)
- Tool architecture: 40+ discrete tools with PermissionGate structures; file-read deduplication (skip re-read if unchanged); large result offloading to disk with preview + reference; CLAUDE.md reinserted on EVERY turn change (not just at session start)
- Coordinator Mode (unreleased): lead Claude spawns parallel worker agents in isolated contexts; workers share prompt cache prefix (pay input tokens once, not per-worker); communicate via XML-structured task notifications + scratchpad directory
- KAIROS (unreleased always-on daemon): 15-second blocking budget for proactive actions, max 2 proactive messages per window; reactive messages bypass budget entirely
- 44 feature flags; 'Undercover Mode' to prevent internal leaks (leaked along with everything else); 5 compaction strategies for context overflow

## Entities Mentioned

- [[wiki/entities/pawel-jozefiak]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/bun]]
- [[wiki/entities/cloudflare-r2]]
- [[wiki/entities/kairos]]
- [[wiki/entities/autodream]]

## Concepts Covered

- [[wiki/concepts/skeptical-memory]]
- [[wiki/concepts/memory-consolidation]]
- [[wiki/concepts/prompt-cache-sharing]]
- [[wiki/concepts/multi-agent-coordination]]
- [[wiki/concepts/context-window-management]]
- [[wiki/concepts/adversarial-verification]]
- [[wiki/concepts/tool-permission-architecture]]
- [[wiki/concepts/proactive-agent-rate-limiting]]

## Notable Quotes

> "Memory is a hint. The codebase is the truth."

> "The system prompt for coordinators emphasizes 'parallelism is your superpower.'"

> "CLAUDE.md doesn't just get loaded once at the start. It gets reinserted into the conversation on every turn change."

> "Someone forgot to add *.map to the .npmignore file. That's it. A missing line in a config file."

## Cross-Connections

The three-layer memory architecture in Claude Code is a production-grade implementation of Karpathy's LLM wiki pattern — index + topic files + raw transcripts maps exactly to Karpathy's raw/wiki/index structure ([[wiki/sources/karpathy-10x-claude-code-llm-wiki]]). The autoDream consolidation daemon is a direct solution to the 'context entropy' problem Jack Roberts calls out in [[wiki/sources/claude-code-karpathy-obsidian-new-meta]]. The Coordinator Mode multi-agent pattern is what Anthropic's harness engineering article describes as the two-agent Initializer/Coding Agent split ([[wiki/sources/anthropic-harness-engineering-two-agent-architecture]]). Collectively, these four sources form a coherent theoretical cluster around context management and persistent memory that underlies this entire knowledge base.
