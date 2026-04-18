---
title: "Harness Engineering"
type: concept
domain: ai
tags:
  - agent-architecture
  - context-engineering
  - agent-patterns
  - anthropic
  - prompt-engineering
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/anthropic-harness-engineering-two-agent-architecture]]"
---

# Harness Engineering

Harness engineering is Anthropic's internal term for the engineering discipline of systematically structuring what an agent sees in its context window — what tools are available, what memory is loaded, what constraints are active, what output format is expected, and what task context is provided. Unlike prompt engineering (writing good one-off instructions), harness engineering is infrastructure: a reusable, systematic framework for configuring agent context across many tasks. The "harness" is the apparatus that surrounds the agent's raw LLM capability, shaping its perception and its action space.

## Definition

The harness is everything except the model weights themselves: the system prompt, the tool definitions, the memory-loading logic, the output parser, the error-handling scaffolding, and the coordination logic for multi-agent systems. Harness engineering is the discipline of designing this apparatus well.

Anthropic's two-agent architecture for harness engineering separates concerns cleanly: one agent handles **harness management** (deciding what context to load, what tools to expose, what constraints to activate), while the second agent handles **task execution** (using the configured harness to accomplish the actual work). This is related to but distinct from the [[advisor-executor-pattern]] — here the split is about context management versus task execution, not planning versus doing.

## How It Works

A well-designed harness for an agent session determines:

**Tool availability**: which tools the agent can call. Over-exposing tools (giving a research agent file-write access) creates unnecessary risk. Under-exposing them (giving a coding agent no shell access) limits capability. The harness configures this precisely for the task type.

**Memory loading**: which files to load into context at session start. Not everything in the repository is relevant to every task. A harness that loads only relevant context (CLAUDE.md, the specific source files, the relevant skill) is more focused and uses fewer tokens than one that dumps everything.

**Constraint activation**: which behavioral constraints are active. A code-review harness might activate "never modify files, only comment" constraints. A migration harness might activate "always write tests before modifying production code" constraints. These are different from CLAUDE.md's standing constraints — they are task-specific, activated by the harness for this particular agent invocation.

**Output format**: what structure the agent's output should have. For a harness feeding into downstream processing, structured output (JSON, YAML, specific markdown) is essential. For a harness delivering to a human, prose is appropriate. The harness specifies this so the agent doesn't need to guess.

## Why It Matters

The key distinction from prompt engineering is systematicity. A prompt engineer writes instructions for a specific conversation. A harness engineer designs a system that correctly configures agents for a class of tasks, reliably and repeatably. The difference is the difference between a craftsperson and an engineer: the engineer's solution scales.

This systematicity matters because production agentic systems handle many tasks, not one. If context configuration is done ad hoc (different instructions written each time), quality varies with the instruction-writer's skill and attention. If it's handled by a harness, quality is determined by the harness design — which can be tested, iterated, and improved systematically.

The harness is also where [[agent-memory]] retrieval decisions are made: which parts of the accumulated memory are relevant to this task? A memory retrieval strategy that's part of the harness is systematic; one that's part of the agent's own reasoning is unpredictable. Externalizing retrieval logic to the harness makes memory use reliable.

## In Practice

Practically, harness engineering is manifest in files like [[claude-md]] (standing context), [[skill-md]] (task-specific context), tool configuration (which MCP servers are exposed), and output parsing logic. The harness engineer's job is ensuring these components work together correctly for each class of agent task the system supports.

The two-agent harness architecture (harness manager + task executor) is most valuable when the number of task types is large or when context configuration is itself complex — for example, in a system where different tasks require very different tool sets, memory subsets, and constraints. For simple systems with one task type, a static CLAUDE.md is the entire harness and no management agent is needed.

Context engineering is becoming a recognized sub-discipline of AI engineering precisely because the complexity of configuring contexts well at scale is non-trivial, and because getting it wrong produces subtle failures (agent makes wrong assumptions, uses wrong tools, formats output incorrectly) that are hard to diagnose without systematic tooling.

## Related Concepts

- [[wiki/concepts/claude-md]] — the primary harness artifact for standing context
- [[wiki/concepts/skill-md]] — task-specific harness components
- [[wiki/concepts/agent-memory]] — memory loading is a key harness function
- [[wiki/concepts/multi-agent-orchestration]] — harness engineering scales to multi-agent systems
- [[wiki/concepts/advisor-executor-pattern]] — a specific two-agent architecture for harness management
- [[wiki/concepts/context-window-management]] — harness determines what fits in context

## Key Entities

- [[wiki/entities/anthropic]] — coined the term and developed the discipline

## Sources

- [[wiki/sources/anthropic-harness-engineering-two-agent-architecture]]
