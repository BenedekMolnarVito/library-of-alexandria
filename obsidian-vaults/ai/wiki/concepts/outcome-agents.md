---
title: "Outcome Agents"
type: concept
domain: ai
tags:
  - agent-evaluation
  - agent-patterns
  - memory
  - artifacts
  - knowledge-accumulation
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/wall-street-285b-ai-agents-review]]"
---

# Outcome Agents

Outcome agents is a framework for evaluating AI agents by what they produce rather than how they work. The distinction matters because many AI agent implementations are impressive in operation but produce nothing that accumulates, nothing that the user can edit, and nothing that compounds in value over time. An outcome agent produces **persistent artifacts** — editable files, structured knowledge, versioned outputs — that remain useful after the session ends, and whose value grows as subsequent agent sessions build on them. Three criteria define an outcome agent: persistent memory, artifact production, and compounding context.

## Definition

The three criteria for an outcome agent:

**Persistent memory**: the agent retains learned context across sessions. It doesn't re-introduce itself, re-learn the project, or re-derive previously established insights. Memory is encoded in files (CLAUDE.md, SOUL.md, the wiki) that survive session end and are loaded at session start. Without this, the agent is impressive in demonstration but useless for compounding work.

**Artifact production**: the agent produces **editable, persistent outputs** — not just responses. A markdown file, a piece of code, a structured report, an updated wiki page, a test suite. Crucially, these artifacts must be on "a surface that is easily visible" — meaning the user can see, inspect, and edit them without specialized tools. Chat responses don't count; markdown files in a git repository do.

**Compounding context**: each agent run adds value to the project. The first run produces a baseline. The second run builds on it. The fiftieth run reflects fifty iterations of compounding context, each more valuable than the last. An agent that produces the same quality of output on run fifty as on run one isn't compounding.

## How It Works

The framework is evaluative: apply the three criteria to any agent workflow to determine whether it produces outcomes or just activity. Many impressive agent demonstrations fail the test. A research agent that produces a long chat message summarizing ten papers fails because the message isn't editable and isn't persistent — it disappears when the chat session ends. The same agent that produces a structured wiki page, updates the index, and appends to the log passes all three criteria.

The practical implication is that artifact format matters enormously. The agent should be designed to write to files, not to respond in chat. The human's interface to agent work should be the file system (preferably a git repository), not the chat history.

The framing of "editable" is important: an artifact the agent produces but the human can't meaningfully modify is less valuable than one the human can correct, extend, or redirect. PDF output is editable with effort; markdown is editable trivially. JSON is editable but requires care; YAML is more readable. The best artifact formats are the ones humans use naturally — markdown, code, structured text.

## Why It Matters

The outcome agent framework provides a sharp test for the question "is this agent actually useful for my work?" Many agent tools are exciting in demonstration but fail to compound value in practice. The excitement comes from the performance — watching an agent navigate multiple tools, reason through a complex task, and produce a coherent response. The failure comes from the format: a chat message that disappears, a web search that isn't saved, a plan that exists only in the conversation context.

The framework also clarifies the design question for agent system builders: "What artifact should this agent produce, and how will the user interact with it after the session?" Starting from the desired artifact and working backward to the agent design is the right direction. Most agent systems are designed in the other direction: starting from capabilities and hoping valuable artifacts emerge.

## In Practice

The [[llm-wiki]] is the canonical outcome agent system: every session produces persistent markdown files (source summaries, concept pages, entity pages, analysis pages), updates to the index, and log entries. The user can read, edit, and correct every artifact. Each ingest compounds on previous ingests. It passes all three outcome agent criteria by design.

The SaaS disruption question (see [[saas-disruption]]) is also an outcome agent question: does the SaaS tool you use produce artifacts the outcome agent framework can beat? If the value of the SaaS is in its UI (convenience, discoverability, collaboration) rather than its outputs, an agent with better artifact quality can replace it. If the SaaS produces high-quality, persistent, editable artifacts (a design system, a data model, a structured workflow), it's more defensible.

## Related Concepts

- [[wiki/concepts/agent-memory]] — persistent memory is the first outcome criterion
- [[wiki/concepts/knowledge-accumulation]] — the compounding property
- [[wiki/concepts/llm-wiki]] — the canonical outcome agent application
- [[wiki/concepts/saas-disruption]] — outcome agents as SaaS replacements
- [[wiki/concepts/markdown-first-architecture]] — the artifact format that maximizes editability
- [[wiki/concepts/spec-driven-development]] — the workflow design that produces artifact-oriented agents

## Sources

- [[wiki/sources/wall-street-285b-ai-agents-review]]
