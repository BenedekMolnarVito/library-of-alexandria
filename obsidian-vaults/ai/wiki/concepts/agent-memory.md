---
title: "Agent Memory"
type: concept
domain: ai
tags:
  - agent-architecture
  - memory
  - context-window
  - persistence
  - agent-patterns
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/anthropic-openai-memory-context-portability]]"
  - "[[wiki/sources/real-problem-ai-agents-clarity-of-intent]]"
  - "[[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]"
---

# Agent Memory

Agent memory is the collection of mechanisms by which an AI agent retains and retrieves information beyond the span of a single context window. LLM context windows are ephemeral — every session starts blank unless explicit memory mechanisms are in place. This creates a fundamental tension between the capability of individual LLM sessions and the continuity required for long-running, compounding work. Different memory architectures make different tradeoffs on speed, capacity, portability, and infrastructure cost.

## Definition

Agent memory operates across four primary categories:

**In-context memory** is the fastest and simplest: information held in the active context window during a session. It requires no infrastructure and is instantly accessible, but it evaporates at session end and is bounded by context window size (typically 128k–200k tokens for current frontier models). For short tasks, in-context memory is sufficient; for long-running or multi-session work, it is not.

**External file memory** persists information to the file system as plain text or structured files (markdown, JSON, YAML). [[claude-md]], [[soul-md]], and the [[llm-wiki]] are all external file memory architectures. This approach is highly portable, human-inspectable, and git-versionable, but requires the agent to decide what to write and when, and requires a retrieval step (reading the file) at session start.

**Vector store memory** uses embedding models to encode information as high-dimensional vectors and retrieves the most semantically similar items for a given query. This enables scalable semantic retrieval over large memory corpora, but requires infrastructure (a vector database), ongoing embedding costs, and produces memories that are not human-inspectable. See [[rag-vs-llm-wiki]] for the comparison with markdown-based alternatives.

**Structured database memory** stores information in queryable tables. This is appropriate for structured data (task lists, project states, entity relationships) and enables complex queries, but requires a database and schema design. It does not naturally handle unstructured narrative knowledge.

## How It Works

The practical memory architecture for an agent system typically combines multiple types: in-context memory for the current session, [[claude-md]] for project instructions, [[soul-md]] for accumulated relationship context, and a markdown wiki or vector store for domain knowledge. The key engineering question is: what gets written to which memory store, and when?

Anthropic and OpenAI have taken divergent philosophical positions on this question. Anthropic treats memory as a first-class agent feature — building explicit memory management into the agent architecture, giving agents the ability to decide what to write and read. OpenAI has treated memory more as a user service — a convenience feature managed on behalf of users. Nate B Jones argues that neither approach fully solves the problem, because memory needs to be built into the architecture from the ground up, not bolted on as a feature.

The context portability problem (see [[context-portability]]) makes the memory architecture decision high-stakes: if your agent's accumulated memory lives inside a platform's proprietary memory system, switching tools means losing that memory. File-based memory architectures avoid this by keeping memory in files the user controls.

## Why It Matters

The quality difference between an agent with good memory and one without is not subtle. An amnesiac agent — one that starts every session blank — is individually competent but collectively useless for any task requiring continuity. It will re-derive the same conclusions, re-make the same mistakes, and re-learn the same context every session.

An agent with good memory compounds: each session builds on the last, the agent's model of the project grows more accurate, and the human spends less time re-briefing. The gap between these two agents widens as time passes — after a week of daily sessions, the memory-equipped agent is dramatically more valuable than the amnesiac one.

The [[llm-wiki]] represents a particularly elegant memory architecture for knowledge work: the memory is the wiki itself. Every ingest adds to it; every query is answered from it; the agent's accumulated knowledge is directly readable by both the agent and the human. There is no separate memory layer — the wiki is both the product and the memory.

## In Practice

Designing agent memory for a production system requires thinking carefully about four dimensions: what needs to be remembered (not everything is worth storing), where it should be stored (matching the memory type to the information type), when it should be written (at session end? after every task? continuously?), and how it should be retrieved (reading the full file, semantic search, keyword search). Getting these wrong produces agents that are either amnesiac (under-memory) or confused by stale/contradictory stored beliefs (over-memory without curation).

## Related Concepts

- [[wiki/concepts/claude-md]] — the instruction memory layer
- [[wiki/concepts/soul-md]] — the identity/relationship memory layer
- [[wiki/concepts/context-portability]] — why memory should be portable
- [[wiki/concepts/llm-wiki]] — wiki as memory architecture
- [[wiki/concepts/rag-vs-llm-wiki]] — comparing memory retrieval approaches
- [[wiki/concepts/knowledge-accumulation]] — the compounding property of good memory
- [[wiki/concepts/context-window-management]] — managing the in-context memory layer

## Key Entities

- [[wiki/entities/anthropic]] — memory as first-class agent feature
- [[wiki/entities/openai]] — memory as user service
- [[wiki/entities/nate-b-jones]] — "memory needs to be built into the architecture"

## Sources

- [[wiki/sources/anthropic-openai-memory-context-portability]]
- [[wiki/sources/real-problem-ai-agents-clarity-of-intent]]
- [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]
