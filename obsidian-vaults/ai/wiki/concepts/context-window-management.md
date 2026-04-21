---
title: "Context Window Management"
type: concept
domain: ai
tags:
  - agent-architecture
  - context-window
  - efficiency
  - claude-code
  - optimization
created: 2026-04-28
updated: 2026-04-21
sources:
  - "[[wiki/sources/cut-claude-code-output-tokens-75-percent]]"
  - "[[wiki/sources/karpathy-claude-md-file]]"
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
  - "[[wiki/sources/claude-session-limit-management]]"
---

# Context Window Management

Context window management is the collection of techniques for making effective use of the finite context window in LLM interactions — maximizing signal density while minimizing token waste. As context windows grow (Claude 3.5: 200k tokens; future models may support millions), the problem doesn't disappear — it shifts from "what can we fit?" to "what should we put here to get the best output?" Good context management is the difference between an agent that consistently produces high-quality work and one that drifts, confuses, or forgets critical information mid-task.

## Definition

Context window management operates at three levels:

**Input curation**: what goes into the context before the agent begins work. This includes: system prompt (CLAUDE.md, SOUL.md, skill files), task specification, relevant code/documents, and any in-context memory from previous steps. Over-populating the context with tangentially relevant material dilutes the signal; under-populating leaves the agent without necessary information.

**Output control**: how verbose the agent's outputs are during the task. Every generated token that goes back into context costs future tokens. An agent that writes lengthy reasoning traces, verbose confirmations, and exhaustive explanations burns context faster than one that communicates concisely.

**Sliding window strategies**: for long tasks that exceed the context window, deciding which parts of the history to retain, which to summarize, and which to discard. The [[autoresearch]] skill implements a sliding window for long optimization runs — keeping only the most recent N iterations in full detail and summarizing earlier ones.

## How It Works

**Claude Code Caveman plugin**: an extension that reduces Claude Code's output tokens by 75% by instructing the agent to strip verbose explanations, confirmations, and intermediate reasoning from its responses. The agent still does the work; it simply stops narrating. The human-readable output is dramatically shorter while the quality of the actual work (code written, files modified) is unchanged. This is pure context efficiency gain: same outcomes, 75% less output token cost.

**CLAUDE.md length optimization**: Karpathy's observation that frontier models handle approximately 150–200 standing instructions coherently, and that Claude Code's own system prompt uses roughly 50, implies that CLAUDE.md files should be short and high-signal rather than long and comprehensive. A CLAUDE.md that attempts to encode every possible constraint and preference will have some of those constraints lose priority as the context fills. The discipline is choosing the highest-leverage constraints and trusting the model's defaults for everything else.

**Autoresearch sliding window**: Balu Kosuri's autoresearch skill includes context window management as one of seven advanced features. For optimization loops that may run dozens of iterations, naively keeping every iteration in context would overflow the window by run 15–20. The sliding window keeps the last N iterations in full detail (N tuned to the model's context size and iteration verbosity), summarizes older iterations into compact records (mutation applied, score achieved, key insight), and discards detailed records beyond a configurable horizon.

**Session handoff and rewind discipline**: Nate Herk's session-management playbook adds a more operational layer: use `/re` to drop failed branches of the conversation, treat session handoffs as normal artifacts, and clear or chain sessions before context rot becomes the dominant problem. The point is not just saving tokens; it is preserving model quality by keeping the active window sharp.

## Why It Matters

Context window limits are a hard constraint, not an engineering preference. An agent that fills its context window mid-task and then loses access to its instructions, the task specification, or critical intermediate results produces failures that are hard to diagnose. The symptoms — the agent repeating itself, forgetting constraints, making choices inconsistent with earlier decisions — look like model quality failures but are actually context management failures.

As tasks grow more complex (more files, longer optimization runs, deeper reasoning chains), context management becomes increasingly the limiting factor in agent quality. Investing in context management techniques — tighter CLAUDE.md, output token reduction, sliding windows — produces direct quality improvements independent of model capability.

The [[harness-engineering]] connection is important: context management is a harness responsibility, not a task-agent responsibility. A well-designed harness controls what gets loaded into context, how much output the agent produces, and when the context is trimmed. Leaving context management to the task agent is a recipe for inconsistent behavior.

## In Practice

A practical context management checklist for agentic tasks:

1. Load only relevant CLAUDE.md sections (task-specific skill files rather than a monolithic spec)
2. Limit file reads to files the task actually needs
3. Use output format constraints (bullet points over prose, structured JSON over narrative) to reduce response verbosity
4. Implement explicit context trimming for loops running more than 10 iterations
5. Monitor token usage and set alerts at 60–70% of the context window size
6. Summarize completed task phases before beginning new ones
7. Treat sub-agents and fresh sessions as standard workflow tools, not last-resort resets

## Related Concepts

- [[wiki/concepts/claude-md]] — the primary document requiring length discipline
- [[wiki/concepts/harness-engineering]] — the infrastructure layer where context is managed
- [[wiki/concepts/agent-memory]] — managing what information persists across context resets
- [[wiki/concepts/autoresearch]] — implements sliding window for long optimization runs
- [[wiki/concepts/agentic-loop]] — context grows with each loop iteration
- [[wiki/concepts/tool-call-bottleneck]] — tool results add to context; managing this is critical

## Key Entities

- [[wiki/entities/anthropic]] — Claude Code and its context window behavior
- [[wiki/entities/andrej-karpathy]] — CLAUDE.md length optimization guidance
- [[wiki/entities/balu-kosuri]] — autoresearch sliding window implementation

## Sources

- [[wiki/sources/cut-claude-code-output-tokens-75-percent]]
- [[wiki/sources/karpathy-claude-md-file]]
- [[wiki/sources/karpathy-autoresearch-universal-skill]]
- [[wiki/sources/claude-session-limit-management]]
