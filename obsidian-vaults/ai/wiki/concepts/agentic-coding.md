---
title: "Agentic Coding"
type: concept
domain: ai
tags:
  - software-engineering
  - ai-coding
  - claude-code
  - codex
  - agent-patterns
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/building-claude-code-boris-cherny]]"
  - "[[wiki/sources/100-hours-claude-code-vs-antigravity]]"
  - "[[wiki/sources/karpathy-claude-md-file]]"
  - "[[wiki/sources/codex-and-claude-side-by-side]]"
---

# Agentic Coding

Agentic coding is the paradigm where LLMs don't merely suggest code for humans to accept or reject, but execute complete software development tasks autonomously — reading the codebase, running tests, writing files, debugging failures, and iterating until a specification is met. It represents a qualitative shift from AI as a code autocomplete tool (Copilot's original model) to AI as a software development agent (Claude Code, Codex CLI, Cursor in agent mode). Andrej Karpathy's December 2025 shift from 80% manual to 80% agent-driven development marks the inflection point when agentic coding became the primary mode for leading practitioners.

## Definition

Agentic coding is characterized by several distinguishing properties from earlier AI coding assistance:

**Full task execution**: the agent receives a goal ("implement this feature," "fix this bug," "refactor this module") and works autonomously through all steps required: reading relevant files, writing implementations, running tests, observing failures, debugging, and iterating. The human reviews completed work, not in-progress suggestions.

**Tool use**: agentic coding agents have access to the file system (read/write), shell execution (run tests, build tools, shell commands), and often web search. This separates them from autocomplete tools that produce text without interacting with the environment.

**Codebase awareness**: the agent reads and understands the full relevant context — existing code, tests, documentation, project conventions — rather than working from a single file or function in isolation.

**Self-verification**: quality agents check their own work (run tests, verify the implementation against specified criteria) before declaring done. The [[claude-md]] failure mode analysis identifies not doing this as a key failure pattern; a well-configured agent loops until its own verification passes.

## How It Works

The primary tools in the agentic coding landscape:

**Claude Code** (Anthropic): the most capable general-purpose agentic coding tool as of 2026. Built around Claude's strong instruction-following, tool use, and long-context reasoning. Boris Cherny's account describes it as designed from the ground up for agentic task execution, not adapted from a conversational assistant.

**Codex CLI** (OpenAI): command-line coding agent based on GPT-4-class models. Well-suited for structured, well-defined coding tasks.

**Cursor** (Anysphere): IDE-integrated agentic coding with particularly strong multi-file awareness and codebase navigation.

**Cline / OpenClaw**: open-source Claude Code alternative that supports local models (Ollama) and custom model backends, enabling fully local agentic coding workflows.

**Key performance metric for local models**: for agentic coding workloads, first-pass reliability (does the generated code compile and pass tests without repair passes?) matters more than token generation speed. A model that produces correct code at 15 tokens/second is more useful than one that produces incorrect code at 50 tokens/second. This is the primary metric Gemma 4 was evaluated against for local agentic coding use cases.

## Why It Matters

Agentic coding represents the most significant shift in software development practice since the introduction of modern IDEs. The productivity implications are substantial: tasks that previously required hours of focused engineering work (reading unfamiliar code, writing boilerplate, debugging stack traces, writing test coverage) are now delegatable to agents that complete them in minutes.

The risk side is equally significant: [[dark-code]], [[vibe-coding]], and the loss of deep system understanding when engineers stop reading the code they deploy. The engineering discipline required for safe agentic coding (see [[spec-driven-development]], [[claude-md]]) is different from traditional software engineering discipline, and teams that adopt agentic coding without adapting their practices often discover this the hard way.

The long-term implication for the engineering profession: the engineers who understand how to direct agents effectively, evaluate agent-produced code, design specifications that agents can implement correctly, and maintain comprehensibility in AI-heavy codebases will be dramatically more productive than those who don't. The skill is shifting from writing code to architecting and evaluating the work of coding agents.

## In Practice

A mature agentic coding workflow for a production team:
- Pre-task: write a spec.md for any non-trivial feature (see [[spec-driven-development]])
- During-task: use CLAUDE.md to constrain agent behavior (scope, style, verification requirements)
- Post-task: review agent output against the spec, not against intuition; run the full test suite
- Commit: require human review before merging agent-produced code to main branches
- Monitor: track and address any accumulating [[dark-code]] in critical paths

## Related Concepts

- [[wiki/concepts/claude-md]] — the behavioral specification for agentic coding agents
- [[wiki/concepts/spec-driven-development]] — the workflow discipline for safe agentic coding
- [[wiki/concepts/dark-code]] — the failure mode to avoid
- [[wiki/concepts/vibe-coding]] — the anti-pattern
- [[wiki/concepts/harness-engineering]] — the infrastructure context for agentic coding
- [[wiki/concepts/local-ai-inference]] — local models for agentic coding at zero marginal cost

## Key Entities

- [[wiki/entities/anthropic]] — Claude Code
- [[wiki/entities/openai]] — Codex CLI
- [[wiki/entities/andrej-karpathy]] — 80% agent-driven development shift

## Sources

- [[wiki/sources/building-claude-code-boris-cherny]]
- [[wiki/sources/100-hours-claude-code-vs-antigravity]]
- [[wiki/sources/karpathy-claude-md-file]]
- [[wiki/sources/codex-and-claude-side-by-side]]
