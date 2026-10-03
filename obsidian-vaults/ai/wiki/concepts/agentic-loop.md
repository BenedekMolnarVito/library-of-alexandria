---
title: "Agentic Loop"
type: concept
domain: ai
tags:
  - agent-architecture
  - tool-calls
  - agent-patterns
  - execution-cycle
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/ai-50x-faster-getting-2x-wrong-thing]]"
  - "[[wiki/sources/300-dollars-auto-research-karpathy-loop]]"
---

# Agentic Loop

The agentic loop is the core execution cycle of an AI agent: the language model generates output (text or a tool call), if it calls a tool the environment executes it and returns a result, the model processes the result, and the cycle repeats until the task is complete or a stopping condition is met. This loop is the fundamental unit of agentic AI — everything else (multi-agent orchestration, memory management, harness engineering) is scaffolding around it. Understanding where time is spent in the loop is essential for optimizing agentic systems.

## Definition

The loop has four phases:

1. **Generate**: the LLM produces a token sequence. This may be natural language reasoning, a structured tool call, or a final answer.
2. **Execute**: if the token sequence is a tool call, the environment executes it — running a bash command, reading a file, calling an API, searching the web.
3. **Observe**: the result of the tool call (stdout, file contents, API response) is added to the context.
4. **Repeat**: the LLM generates again with the updated context. This continues until the model produces a final answer or signals task completion.

The loop is simple in structure but complex in practice: tool calls can fail, observations can be incomplete, tasks can require dozens of iterations, and context can grow until it hits the window limit. Robust agentic systems handle all of these cases gracefully.

## How It Works

In LLM inference terms, the bottleneck is not where intuition places it. The **inference step** (generating tokens) is typically fast — frontier models produce hundreds of tokens per second on server-class hardware. The **tool call step** is where wall-clock time goes: a web search takes 2–5 seconds; a bash command might take 30 seconds; an API call can take arbitrarily long. See [[tool-call-bottleneck]] for a detailed analysis of this asymmetry.

This has practical implications for optimization. Speeding up the model (using a faster/cheaper model for some steps) produces modest gains if tool calls dominate. The highest-leverage optimizations are usually: parallelizing independent tool calls within a single generation cycle, caching tool results where possible, and reducing the number of tool calls required through better initial planning.

The [[karpathy-loop]] is a specialized agentic loop where the tool call is a complete training or evaluation run and the fitness function is the objective metric. The outer loop structure is identical; what's specialized is the tool (the evaluation harness) and the stopping condition (metric target met).

## Why It Matters

The agentic loop is the lens through which to evaluate agent infrastructure. Every optimization question — should we use a faster model? Should we cache this result? Should we parallelize these searches? Should we rewrite this tool? — is really a question about which phase of the loop is the bottleneck and whether the proposed change reduces time in that phase.

The loop also explains why context window management matters so much: with every iteration, the context grows by at least the tool result. A loop that runs 20 iterations may accumulate 50,000 tokens of tool results before producing a final answer. Poor context management (retaining all intermediate results) hits the window limit; good context management (summarizing or truncating older results) keeps the loop running.

The mental model of the loop — generate, execute, observe, repeat — also clarifies what "autonomous" means in agentic AI. The agent is autonomous over this loop: it decides when to stop, which tools to call, and how to interpret results. But it operates within the harness the engineer designed, with the tools the harness exposed, on the task the human specified.

## In Practice

Practical agentic loop design involves several recurring decisions:

**Stopping conditions**: when does the agent declare the task done? This can be model-driven ("I believe the task is complete"), criteria-driven (explicit completion criteria provided in the harness), or budget-driven (maximum iterations or token count). Criteria-driven is most reliable for production systems.

**Error handling**: what happens when a tool call fails? Retry immediately? Try an alternative tool? Report to the orchestrator? The loop needs explicit error recovery logic for each tool.

**Observation formatting**: raw tool outputs are often verbose and repetitive. Preprocessing tool results before adding them to context (stripping boilerplate, summarizing long outputs, extracting relevant sections) keeps context lean and improves subsequent generation quality.

## Related Concepts

- [[wiki/concepts/tool-call-bottleneck]] — where time actually goes in the loop
- [[wiki/concepts/agent-native-infrastructure]] — infrastructure redesigned around the loop's real bottlenecks
- [[wiki/concepts/karpathy-loop]] — a specialized agentic loop with a fitness function
- [[wiki/concepts/multi-agent-orchestration]] — orchestrating multiple loops
- [[wiki/concepts/context-window-management]] — managing context across many loop iterations
- [[wiki/concepts/harness-engineering]] — the infrastructure that surrounds the loop
- [[wiki/concepts/agentic-architecture-guide]] — Claude Certification guidance on loop control
- [[wiki/concepts/agentic-arch-orchestration]] — `stop_reason`-driven termination done rigorously

## Sources

- [[wiki/sources/ai-50x-faster-getting-2x-wrong-thing]]
- [[wiki/sources/300-dollars-auto-research-karpathy-loop]]
