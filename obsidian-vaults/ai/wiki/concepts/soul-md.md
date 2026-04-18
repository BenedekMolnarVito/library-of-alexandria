---
title: "SOUL.md (Persistent Agent Identity)"
type: concept
domain: ai
tags:
  - agent-memory
  - agent-identity
  - context-persistence
  - agent-patterns
  - karpathy-loop
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/300-dollars-auto-research-karpathy-loop]]"
  - "[[wiki/sources/real-problem-ai-agents-clarity-of-intent]]"
---

# SOUL.md (Persistent Agent Identity)

SOUL.md is a markdown file that encodes an AI agent's persistent identity — its "personality," accumulated knowledge, relationship with the user, goals, and self-model. Introduced by Nate B Jones in the context of $300 [[karpathy-loop]] experiments, it is distinct from [[claude-md]] (which gives instructions) and [[skill-md]] (which gives expertise). SOUL.md is the agent's evolving sense of itself, persisted to the file system so it survives across sessions. The complementary pattern is heartbeat.md, which tracks agent state and health between sessions.

## Definition

Where CLAUDE.md asks "what rules should I follow?" and skill.md asks "how should I approach this task?", SOUL.md asks "who am I?" It encodes:

- The agent's accumulated understanding of the user's preferences, goals, and working style
- The agent's own goals and values as they've been shaped through past interactions
- A record of significant decisions, commitments, and lessons learned
- The relationship context: how long the agent has worked with this user, what they've built together, what the agent knows about what the user cares about

SOUL.md is not a static configuration — it is meant to evolve. After each session, the agent updates it with new information about the user, new lessons learned, and any changes to its understanding. The file grows over time, encoding an accumulating relationship rather than a fixed specification.

## How It Works

The mechanism is straightforward: at the start of each session, the agent reads SOUL.md alongside CLAUDE.md, integrating both project context and personal identity. At the end of the session (or when explicitly triggered), the agent writes back to SOUL.md with updates — new observations, changed understandings, corrections to previous beliefs.

This write-back makes SOUL.md fundamentally different from CLAUDE.md. The human writes CLAUDE.md (with possible agent assistance). The agent writes SOUL.md (with the human's knowledge that it's happening). The file is the agent's narrative, not the human's instructions.

The heartbeat.md pattern complements SOUL.md by tracking lower-level operational state: what tasks were in progress, what was completed in the last session, what context is needed to resume work, and any errors or anomalies encountered. Where SOUL.md is narrative and reflective, heartbeat.md is operational and structured.

## Why It Matters

Nate B Jones' key insight is that the problem with AI agents isn't capability — it's continuity. Every session starts blank: the agent has no memory of what it learned yesterday, what the user cares about, or what mistakes it made and corrected. This produces the experience of perpetually on-boarding a new employee who is individually competent but collectively amnesiac.

SOUL.md addresses the continuity problem at the identity layer. The agent that reads its SOUL.md before beginning a session is, in a meaningful sense, the same agent that worked on the project yesterday — it carries the accumulated understanding of a relationship, not just the accumulated instructions of a specification. This distinction matters for quality: an agent that knows the user prefers concise explanations, has strong opinions about naming conventions, and is working toward a specific long-term goal can make better decisions than one that knows only the rules.

The file-system persistence model has an important advantage over platform-provided memory (see [[agent-memory]]): it's portable. If the user switches from Claude Code to Copilot to Cursor, they bring SOUL.md with them. The accumulated relationship survives the tool change. This is a specific application of [[context-portability]] — the principle that critical context should live in files, not platforms.

## In Practice

SOUL.md is particularly valuable in the [[karpathy-loop]] context because optimization runs can span many sessions. An agent running a multi-day autoresearch loop needs to remember not just what it optimized but why it made certain choices, what experiments failed, and what the user's priorities are. SOUL.md provides this continuity without requiring the user to re-brief the agent at the start of each session.

The risk of SOUL.md is drift: as the agent's self-model accumulates, it may incorporate errors or outdated beliefs that persist and compound. Periodic review and correction by the human is recommended — the file should be treated as an evolving collaborative document, not a black box. The human can edit, correct, or reset sections of SOUL.md just as they can edit any markdown file.

## Related Concepts

- [[wiki/concepts/claude-md]] — the instruction complement to SOUL.md's identity layer
- [[wiki/concepts/skill-md]] — the expertise complement; all three together form a full agent context
- [[wiki/concepts/agent-memory]] — the broader problem SOUL.md addresses
- [[wiki/concepts/context-portability]] — why file-based persistence beats platform memory
- [[wiki/concepts/karpathy-loop]] — the optimization context where SOUL.md was introduced
- [[wiki/concepts/llm-wiki]] — LLM wiki as an alternative/complementary memory architecture

## Key Entities

- [[wiki/entities/nate-b-jones]] — introduced SOUL.md in the Karpathy Loop context

## Sources

- [[wiki/sources/300-dollars-auto-research-karpathy-loop]]
- [[wiki/sources/real-problem-ai-agents-clarity-of-intent]]
