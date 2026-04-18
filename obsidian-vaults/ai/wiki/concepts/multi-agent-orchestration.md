---
title: "Multi-Agent Orchestration"
type: concept
domain: ai
tags:
  - agent-architecture
  - orchestration
  - multi-agent
  - langgraph
  - agent-patterns
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/multi-agent-architecture-patterns]]"
  - "[[wiki/sources/how-to-build-claude-agent-teams]]"
  - "[[wiki/sources/comparing-6-python-ai-agent-frameworks]]"
  - "[[wiki/sources/langchain-deep-agents]]"
---

# Multi-Agent Orchestration

Multi-agent orchestration is the design pattern where multiple specialized AI agents collaborate on a task, with an orchestrator coordinating their work. Rather than a single general-purpose agent attempting everything, the system decomposes work into subtasks suited to specialized agents — one for web research, one for code execution, one for synthesis, one for quality control — and routes work between them according to task structure. The tradeoff is straightforward: coordination overhead versus specialization gain. Getting it right requires careful thought about which decompositions are worth the complexity.

## Definition

A multi-agent system consists of at minimum: an **orchestrator** (which receives the overall task, decomposes it, routes subtasks, and assembles results) and one or more **subagents** (which receive specific subtasks, execute them, and return results). The orchestrator may itself be an LLM, using reasoning to determine routing; or it may be a deterministic workflow that routes based on task type.

The key architectural decision is how much intelligence lives in the orchestrator versus the subagents. Pure orchestration (dumb orchestrator, smart subagents) is simpler but inflexible. Pure intelligence centralization (smart orchestrator handling everything) defeats the purpose. Most practical systems use a smart orchestrator for routing decisions and specialized subagents for domain-specific execution.

## How It Works

Four primary topologies cover most multi-agent use cases:

**Sequential (pipeline)**: each agent processes the output of the previous one in a fixed order. Appropriate for tasks with a clear phase structure (research → synthesis → critique → revise). Simple to reason about; bottlenecked by the slowest stage.

**Parallel (fan-out/fan-in)**: the orchestrator splits a task into independent subtasks, dispatches them to multiple agents simultaneously, and merges results. Appropriate when subtasks are independent (web research on multiple topics simultaneously). Fast when subtasks are truly parallel; complex merge logic when they're not.

**Hierarchical (supervisor/worker)**: a supervisor agent manages a pool of worker agents, assigning tasks, monitoring progress, and handling failures. The supervisor has strategic authority; workers have execution authority. The [[advisor-executor-pattern]] is a specific implementation of this topology with an emphasis on separating cognition from action.

**Event-driven**: agents react to events rather than following a predetermined routing plan. Appropriate for open-ended, long-running systems (monitoring, alerting, reactive automation). Hardest to reason about and debug; most flexible for complex dynamic domains.

LangGraph implements multi-agent orchestration as a stateful graph: nodes are agents (or functions), edges are conditional routing logic, and the graph state is shared context passed between nodes. This makes the routing explicit and inspectable — a significant debugging advantage over implicit orchestration.

Claude Code's agent teams model allows Claude to spawn sub-agents for parallel work, with the top-level agent acting as orchestrator. The spawned agents can use the same tools (file operations, web search, code execution) but operate in parallel, dramatically reducing wall-clock time for parallelizable tasks.

## Why It Matters

The fundamental motivation is that no single LLM context window can hold the state of a complex, long-running task. Multi-agent systems solve two related problems: **state scaling** (distributing context across multiple agents that each hold a manageable slice) and **specialization** (using agents whose prompts/tools are tuned for specific task types).

The debugging challenge is the primary cost. A single agent failing produces a clear error. A multi-agent system failing can produce subtle incorrect results — an orchestrator makes a wrong routing decision, a subagent returns a plausible but incorrect result that passes downstream, and the error compounds invisibly. Investing in explicit state logging, agent audit trails, and result validation is essential for production multi-agent systems.

## In Practice

The most important practical advice is to start with the simplest topology that could work. Sequential pipelines are underrated: they're easy to understand, easy to debug, and surprisingly capable when each stage is well-specified. Reach for parallel and hierarchical orchestration only when sequential processing is clearly the bottleneck.

The harness engineering (see [[harness-engineering]]) question is critical for orchestration: what context does each agent see? An orchestrator that passes too much context to subagents bloats tokens and confuses specialization. One that passes too little produces subagents that make wrong assumptions. The art is in the boundaries.

## Related Concepts

- [[wiki/concepts/advisor-executor-pattern]] — a specific two-agent topology
- [[wiki/concepts/harness-engineering]] — structuring what each agent sees
- [[wiki/concepts/agentic-loop]] — the execution cycle each agent runs
- [[wiki/concepts/agentic-saas]] — multi-agent systems as product building blocks
- [[wiki/concepts/tool-call-bottleneck]] — where orchestration systems lose time

## Key Entities

- [[wiki/entities/anthropic]] — Claude Code agent teams
- [[wiki/entities/langchain]] — LangGraph orchestration framework

## Sources

- [[wiki/sources/multi-agent-architecture-patterns]]
- [[wiki/sources/how-to-build-claude-agent-teams]]
- [[wiki/sources/comparing-6-python-ai-agent-frameworks]]
- [[wiki/sources/langchain-deep-agents]]
