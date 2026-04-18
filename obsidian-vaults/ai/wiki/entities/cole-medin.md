---
title: "Cole Medin"
type: entity
domain: ai
tags:
  - person
  - builder
  - content-creator
  - agentic-systems
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]"
---

# Cole Medin

Cole Medin is an AI builder and content creator focused on practical agentic systems, best known for building the **context-portal** — an open-source system that gives [[wiki/entities/claude-code]] a self-evolving, persistent memory by implementing a version of [[wiki/entities/andrej-karpathy]]'s LLM wiki pattern as a living context management layer.

## Background / History

Medin operates primarily in the AI practitioner and open-source builder community. His GitHub profile (coleam00) hosts context-portal alongside other agentic tooling experiments. He produces content that sits at the intersection of Karpathy's conceptual frameworks and practical implementation — translating ideas that originate as observations or research patterns into usable open-source systems.

## Key Contributions / Features

**Context Portal (Self-Evolving Claude Code Memory)**: Medin's most significant contribution to the corpus covered in this wiki is the context-portal system, which implements a structured memory layer for Claude Code projects. Drawing directly on Karpathy's framing of the LLM wiki as a "codebase for the LLM," context-portal automatically accumulates project-specific knowledge across sessions — architectural decisions, patterns learned, gotchas discovered — and injects relevant context into each new Claude Code session. The system is "self-evolving" in that it updates its own knowledge base as the project progresses, rather than requiring manual curation. (Source: [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]])

**Karpathy Pattern Implementation**: Medin's work is explicitly positioned as an implementation of Karpathy's ideas, making it a useful case study in how high-level conceptual patterns from prominent researchers propagate into practical tooling. The context-portal represents one of the cleaner operationalizations of the LLM wiki concept, demonstrating that the pattern generalizes beyond personal knowledge management to project-level agent memory.

## Role in AI Landscape

Medin occupies the builder-translator role in the ecosystem — taking ideas from researchers like Karpathy and turning them into tools that practitioners can use without fully understanding the underlying concepts. Context-portal is notable for addressing one of Claude Code's most frequently cited limitations: the loss of context between sessions that forces users to re-explain project conventions, constraints, and history at the start of each interaction.

## Connections

- **Related entities**: [[wiki/entities/andrej-karpathy]], [[wiki/entities/balu-kosuri]], [[wiki/entities/claude-code]], [[wiki/entities/obsidian]]
- **Key concepts**: [[wiki/concepts/llm-wiki-pattern]], [[wiki/concepts/agent-memory]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/claude-md-pattern]]
- **Sources**: [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]
