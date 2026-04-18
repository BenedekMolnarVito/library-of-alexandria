---
title: "Multi-Agent Architectures: Patterns Every AI Engineer Should Know"
type: source
domain: ai
tags:
  - multi-agent
  - architecture
  - patterns
  - langgraph
  - orchestration
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Multi-Agent Architectures Patterns Every AI Engineer Should Know.md]]"
---

# Multi-Agent Architectures: Patterns Every AI Engineer Should Know

**Authors**: Sateesh Valluru
**Date**: 2026-01
**Type**: article

## Summary

A software-engineering-focused taxonomy of seven multi-agent system patterns — Sequential Pipeline, Router/Dispatcher, Handoff, Skill/Capability Loading, Generator+Critic, Parallel Fan-Out/Gather, and Graph-Based Custom Workflow — with code examples in LangChain/LangGraph and Google ADK. The author argues that the shift from single-agent to multi-agent thinking mirrors the historical shift from monoliths to microservices: it is about separation of responsibility, clear task ownership, and controlled communication, not about having "more AI."

Each pattern is presented with its intent, canonical failure modes, and implementation sketch. The Generator+Critic pattern (Pattern 5) is singled out as especially powerful for quality enforcement but must cap iterations to prevent infinite loops. The Graph-Based pattern (Pattern 7) is the most flexible but easiest to over-engineer prematurely. The overarching mental shift the article advocates: stop asking "what should my prompt say?" and start asking "which agent should own this responsibility?"

## Key Takeaways

- Pattern 1 — Sequential Pipeline: each agent does one thing and passes to the next; canonical use case is ETL and document processing
- Pattern 2 — Router/Dispatcher: one agent classifies and delegates, never solves; the key failure is letting the router also answer
- Pattern 3 — Handoff: agent transfers control mid-task when domain shifts; losing shared context is the primary failure mode
- Pattern 4 — Skill Loading: main agent loads specialized capability on demand to avoid prompt bloat; skills should be temporary and scoped
- Pattern 5 — Generator+Critic: one agent generates, another reviews; always cap iterations to prevent infinite loops
- Pattern 6 — Parallel Fan-Out/Gather: independent agents work simultaneously and merge results; fails when tasks secretly share state
- Pattern 7 — Graph-Based Custom Workflow: agents as nodes, transitions as edges, explicit state; avoid over-engineering early
- "Frameworks change. Patterns transfer." — understand patterns before choosing tools

## Entities Mentioned

- [[wiki/entities/sateesh-valluru]]
- [[wiki/entities/langchain]]
- [[wiki/entities/langgraph]]
- [[wiki/entities/google-adk]]
- [[wiki/entities/google]]

## Concepts Covered

- [[wiki/concepts/sequential-pipeline-pattern]]
- [[wiki/concepts/router-dispatcher-pattern]]
- [[wiki/concepts/agent-handoff]]
- [[wiki/concepts/skill-capability-loading]]
- [[wiki/concepts/generator-critic-loop]]
- [[wiki/concepts/parallel-fan-out-gather]]
- [[wiki/concepts/graph-based-agent-workflow]]
- [[wiki/concepts/separation-of-concerns-in-agents]]
- [[wiki/concepts/multi-agent-orchestration]]

## Notable Quotes

> "You're treating an AI system like a script, not like a system."

> "Frameworks change. Patterns transfer."

> "Multi-agent systems aren't about 'more AI'. They're about responsibility boundaries, explicit coordination, predictable execution."

## Cross-Connections

The Generator+Critic pattern (Pattern 5) is essentially the same quality enforcement loop used in the TDD methodology from [[wiki/sources/stop-vibe-coding-4-file-system]]. The Skill/Capability Loading pattern maps directly to Claude Code skills in [[wiki/sources/master-claude-code-skills]] and to `deepagents` subagents in [[wiki/sources/langchain-deep-agents]]. The Router/Dispatcher pattern is how [[wiki/sources/paperclip-ai-governance-platform]] dispatches tasks to agents via its heartbeat system. The at-scale implementation of Pattern 1 (Sequential Pipeline) is visible in [[wiki/sources/uber-agentic-engineering-shift]]'s AutoCover and Shepherd pipelines.
