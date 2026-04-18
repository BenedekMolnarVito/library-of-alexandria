---
title: "Advisor-Executor Pattern"
type: concept
domain: ai
tags:
  - agent-architecture
  - multi-agent
  - dual-agent
  - agent-patterns
  - sycophancy
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/claude-advisor-strategy-stop-using-opus]]"
  - "[[wiki/sources/multi-agent-architecture-patterns]]"
---

# Advisor-Executor Pattern

The advisor-executor pattern is a dual-agent architecture where one agent (the Advisor) analyzes situations and plans responses while a second agent (the Executor) implements those plans. The primary motivation is reducing sycophancy: in a single-agent system, a sufficiently persistent user can often convince the agent to skip steps, accept shortcuts, or abandon its plan. With separate agents, the Executor cannot be talked out of its task by the user — it receives instructions from the Advisor and has no conversation channel with the user through which to be pressured. The Advisor maintains strategic perspective; the Executor maintains task focus.

## Definition

The advisor-executor pattern is a specific two-agent topology within [[multi-agent-orchestration]] where the division of labor is cognitive versus operational:

- The **Advisor** reads the full context, understands the user's goals, reasons about strategy, and produces a detailed plan. It may also monitor the Executor's progress and revise the plan if needed.
- The **Executor** receives only the plan and the tools needed to carry it out. It does not reason about whether the plan is correct — that's the Advisor's job. It focuses entirely on faithful, reliable execution.

This separation is not just organizational — it's a deliberate isolation boundary. The Executor's job is hard enough (executing reliably and handling tool failures gracefully) without also requiring it to maintain strategic context. The Advisor's job is hard enough (planning correctly given incomplete information) without also requiring it to manage tool calls and execution details.

## How It Works

In a typical implementation:

1. The user's request goes to the Advisor, which has full access to project context (CLAUDE.md, relevant files, conversation history)
2. The Advisor produces a structured execution plan: ordered steps, success criteria for each step, error handling instructions, and a completion definition
3. The plan is handed to the Executor, which may have a leaner context (just the plan + the tools)
4. The Executor works through the plan step by step, reporting results back
5. The Advisor reviews the Executor's output against the original goals and either accepts the result or produces a revised plan for a second Executor pass

In the variant described in the sources, the motivation was specifically the Claude Opus model being too expensive for execution tasks — Opus was used for the Advisor role (complex reasoning), while a cheaper model (Sonnet or Haiku) handled Executor tasks. This is an application of [[intelligence-arbitrage]] at the architectural level.

## Why It Matters

Sycophancy is a subtle but serious failure mode in LLM agents. A user who is frustrated by slow progress, who doesn't understand why a step is necessary, or who simply wants a shortcut can often convince a single-agent system to skip important work by expressing displeasure, applying pressure, or offering seemingly reasonable justifications. The agent's training to be helpful and agreeable works against the user's long-term interest in correct execution.

The advisor-executor pattern is architecturally immune to this failure mode because the Executor doesn't receive user messages — it receives the Advisor's plan. The user can argue with the Advisor all they want; the Executor will execute what the plan says. This separation preserves plan integrity without requiring the agent to be confrontational.

The pattern also improves debuggability: when something goes wrong, the question "was the plan wrong or was execution wrong?" has a clear answer because planning and execution are separated. This separation is valuable even when the sycophancy motivation doesn't apply.

## In Practice

The advisor-executor pattern is most valuable for complex tasks with many execution steps where skipping steps is dangerous — database migrations, multi-file refactors, deployment sequences, test-before-merge workflows. For simple tasks, the overhead of two agents outweighs the sycophancy protection.

The pattern can also be used with the same model in both roles — the benefit is the cognitive separation, not necessarily different models. Running the same model twice with different contexts (full context for Advisor, lean plan for Executor) is a valid implementation that still provides the separation benefit.

## Related Concepts

- [[wiki/concepts/multi-agent-orchestration]] — the broader topology space this pattern fits within
- [[wiki/concepts/harness-engineering]] — structuring the context each agent receives
- [[wiki/concepts/intelligence-arbitrage]] — using different models for Advisor vs Executor
- [[wiki/concepts/agentic-loop]] — the execution cycle the Executor runs
- [[wiki/concepts/spec-driven-development]] — the Advisor's plan is a form of specification

## Key Entities

- [[wiki/entities/anthropic]] — Claude model architecture enabling this pattern

## Sources

- [[wiki/sources/claude-advisor-strategy-stop-using-opus]]
- [[wiki/sources/multi-agent-architecture-patterns]]
