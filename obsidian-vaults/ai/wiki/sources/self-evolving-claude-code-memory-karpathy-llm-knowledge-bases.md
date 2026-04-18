---
title: "I Built Self-Evolving Claude Code Memory w/ Karpathy's LLM Knowledge Bases"
type: source
domain: ai
tags:
  - karpathy
  - claude-code
  - agent-memory
  - self-evolving
  - hooks
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/I Built Self-Evolving Claude Code Memory w Karpathy's LLM Knowledge Bases.md]]"
---

# I Built Self-Evolving Claude Code Memory w/ Karpathy's LLM Knowledge Bases

**Authors**: Cole Medin
**Date**: 2026-04
**Type**: video-transcript

## Summary

Cole Medin extends Karpathy's LLM wiki concept from external knowledge (articles) to internal, codebase-specific memory using Claude Code hooks. Session logs act as a 'raw/' folder, the Claude Agent SDK automatically summarizes each conversation end, and a daily 'flush' process promotes log summaries into a structured wiki. The result is a coding agent that compounds knowledge about its own project over time without manual maintenance. This represents a significant evolution of the LLM wiki pattern — rather than ingesting external sources, the system captures the agent's own work history and distills it into durable, queryable knowledge.

## Key Takeaways

- Karpathy's LLM wiki pattern can be adapted from external research to internal codebase memory
- Claude Code hooks (session_start, pre-compact, session_end) automate the entire knowledge-capture pipeline with no extra setup
- The session_start hook loads agents.md + index.md so the agent always understands the knowledge system
- Daily logs are promoted into a structured wiki via a 'flush' script that calls the Claude Agent SDK
- The compounding loop: answers to queries are filed back into the wiki, making future answers better
- Users can customize the flush/compile prompts to tune what gets extracted

## Entities Mentioned

- [[wiki/entities/cole-medin]]
- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/claude-agent-sdk]]
- [[wiki/entities/obsidian]]
- [[wiki/entities/insforge]]
- [[wiki/entities/dynamis]]

## Concepts Covered

- [[wiki/concepts/llm-knowledge-base]]
- [[wiki/concepts/claude-code-hooks]]
- [[wiki/concepts/self-evolving-memory]]
- [[wiki/concepts/session-log-capture]]
- [[wiki/concepts/knowledge-compounding-loop]]
- [[wiki/concepts/obsidian-vault]]
- [[wiki/concepts/agent-memory]]

## Notable Quotes

> "Unlike Claude Code's memory system, you can customize this to your heart's content — and Claude Code can even walk you through making the customizations because it has access to the agents.md."

> "We're building up our knowledge base over time. The agent is going to be able to search through our knowledge better over time."

## Cross-Connections

Directly implements and extends the LLM wiki pattern popularized by [[wiki/entities/andrej-karpathy]]. The hook-based architecture mirrors how RAG pipelines automate knowledge ingestion, but without vector databases. Connects to the broader 'second brain' movement (Obsidian, Zettelkasten) and to agentic memory research. The Claude Agent SDK usage parallels multi-agent orchestration patterns seen in frameworks like LangGraph. Compare with [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]] (Balu Kosuri's external-knowledge implementation) and [[wiki/sources/claude-code-source-leaked-worth-learning]] (the autoDream system that Claude Code uses internally for the same purpose).
