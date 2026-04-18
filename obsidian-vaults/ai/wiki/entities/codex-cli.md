---
title: "Codex CLI"
type: entity
domain: ai
tags:
  - product
  - openai
  - agentic-coding
  - terminal
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/codex-and-claude-side-by-side]]"
  - "[[wiki/sources/gemma-4-local-model-codex-cli]]"
---

# Codex CLI

Codex CLI is [[wiki/entities/openai]]'s terminal-based agentic coding tool — the GPT-model-powered counterpart to [[wiki/entities/anthropic]]'s [[wiki/entities/claude-code]]. It enables autonomous AI-driven software development from the command line, with the ability to read/write files, execute commands, and work through multi-step programming tasks.

## Background / History

OpenAI released Codex CLI as its answer to the growing category of terminal-based AI coding agents. It follows the same paradigm as Claude Code: a developer gives the agent a task, and the agent works through it autonomously using the model's programming knowledge and available tools. Codex CLI runs on GPT models (typically GPT-4 or newer) and follows OpenAI's API and safety constraints.

The "Codex" name connects to OpenAI's earlier Codex model — the code-specialized model that powered GitHub Copilot — though Codex CLI uses the more recent GPT model family rather than the original Codex model. The name represents brand continuity for OpenAI's code-focused products.

## Key Contributions / Features

**Terminal-Based Agentic Coding**: Like Claude Code, Codex CLI operates as a terminal application that can execute programming tasks autonomously. It supports file operations, shell command execution, and multi-step task completion. The background execution model allows Codex CLI to run tasks while the developer does other work.

**Side-by-Side Comparison with Claude Code**: Practitioners have documented detailed comparisons of Codex CLI and Claude Code running the same tasks, providing empirical data on relative performance across different task types. Results vary by task: some favor Claude's instruction-following, others favor GPT's knowledge breadth. (Source: [[wiki/sources/codex-and-claude-side-by-side]])

**Gemma 4 Local Backend**: [[wiki/entities/daniel-vaughan]] used Codex CLI as the agent framework in his benchmark of [[wiki/entities/gemma-4]] as a local inference backend via [[wiki/entities/llama-cpp]]. This unusual pairing — OpenAI's agent interface with Google's open model — works because Codex CLI can be configured to use any OpenAI-compatible API, making it infrastructure-agnostic like [[wiki/entities/openclaw]]. (Source: [[wiki/sources/gemma-4-local-model-codex-cli]])

## Role in AI Landscape

Codex CLI's primary role is as the principal competition to Claude Code — the benchmark against which Claude Code is measured and vice versa. Practitioner comparisons between the two drive real product decisions about which tool to use for which workload. OpenAI's distribution advantages (ChatGPT brand recognition, Microsoft integration, existing API relationships) mean Codex CLI will likely maintain significant adoption even if Claude Code leads on specific capability metrics. The existence of credible competition between the two is beneficial for the field, driving both products to improve faster than a monopoly would.

## Connections

- **Related entities**: [[wiki/entities/openai]], [[wiki/entities/claude-code]], [[wiki/entities/gemma-4]], [[wiki/entities/llama-cpp]], [[wiki/entities/daniel-vaughan]]
- **Key concepts**: [[wiki/concepts/agentic-coding]], [[wiki/concepts/agent-first-development]]
- **Sources**: [[wiki/sources/codex-and-claude-side-by-side]], [[wiki/sources/gemma-4-local-model-codex-cli]]
