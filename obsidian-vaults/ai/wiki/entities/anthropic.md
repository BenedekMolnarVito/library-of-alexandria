---
title: "Anthropic"
type: entity
domain: ai
tags:
  - org
  - ai-safety
  - model-provider
  - claude
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/building-claude-code-boris-cherny]]"
  - "[[wiki/sources/anthropic-harness-engineering-two-agent-architecture]]"
  - "[[wiki/sources/anthropic-openai-memory-context-portability]]"
---

# Anthropic

Anthropic is an AI safety company and the creator of the Claude model family and [[wiki/entities/claude-code]]. Founded by former OpenAI researchers and executives, it has positioned itself as the safety-focused alternative to OpenAI while competing directly on frontier model capability and developer tooling.

## Background / History

Anthropic was founded in 2021 by Dario Amodei and Daniela Amodei, along with several other ex-OpenAI researchers including [[wiki/entities/boris-cherny]] and others who were concerned about the pace and safety properties of OpenAI's development trajectory. The company is headquartered in San Francisco and has raised multiple billion-dollar funding rounds from investors including Google, Spark Capital, and others. Its stated mission is "the responsible development and maintenance of advanced AI for the long-term benefit of humanity" — a framing that emphasizes safety research alongside commercial product development.

Anthropic's research arm produces work on interpretability (understanding what neural networks are actually doing internally), constitutional AI (training models to be helpful, harmless, and honest through self-critique), and alignment. Its commercial products fund this research, creating a tension — common to AI safety labs — between moving fast enough to generate revenue and moving carefully enough to avoid deploying unsafe systems.

## Key Contributions / Features

**Claude Model Family**: Anthropic's primary commercial output is the Claude family of models, segmented into Haiku (fast, low-cost), Sonnet (balanced performance and cost), and Opus (flagship capability). Claude 3.7 Sonnet introduced extended thinking — the ability to reason through problems step-by-step before responding — which significantly improved performance on complex coding and reasoning tasks. Claude models are the backbone of Claude Code and are widely used by third-party developers building on the API. (Source: [[wiki/sources/building-claude-code-boris-cherny]])

**Claude Code**: The flagship agentic development tool built by [[wiki/entities/boris-cherny]] — a terminal-based and VS Code-integrated AI programmer that can autonomously read/write files, run commands, browse the web, and orchestrate sub-agents. Claude Code became one of the most widely adopted AI coding tools within months of launch, directly competing with [[wiki/entities/openai]]'s Codex CLI. (Source: [[wiki/sources/building-claude-code-boris-cherny]])

**Model Context Protocol (MCP)**: Anthropic released MCP as an open standard for connecting AI models to external tools and data sources. While criticized as a "stopgap" for human-speed APIs, MCP provides a standardized interface that has been widely adopted across the AI tooling ecosystem. (Source: [[wiki/sources/anthropic-openai-memory-context-portability]])

**Two-Agent Architecture (Harness Engineering)**: Anthropic has documented its internal use of a two-agent architecture — one agent writing code, another reviewing and critiquing it — that mirrors software engineering review practices. This demonstrates how AI labs are beginning to apply their own models to internal software development in sophisticated, structured ways. (Source: [[wiki/sources/anthropic-harness-engineering-two-agent-architecture]])

**Memory and Context Portability**: Anthropic is competing directly with OpenAI on the question of memory and context portability — how agents maintain state across sessions, share context across tools, and allow users to control what the agent knows. This competition reflects the emerging importance of persistent agent state as a product differentiator. (Source: [[wiki/sources/anthropic-openai-memory-context-portability]])

## Role in AI Landscape

Anthropic occupies a distinctive position: simultaneously the most safety-focused of the major AI labs and one of the most aggressive competitors in the commercial AI market. Its decision to open-source Claude Code's core and to invest heavily in developer tooling signals a strategy of winning the infrastructure layer — if developers build on Claude Code and MCP, Anthropic models become the default inference backend for a generation of AI applications. Claude's reputation for particularly strong coding and instruction-following capabilities has made it the dominant model choice in the agentic coding space covered throughout this wiki.

## Connections

- **Related entities**: [[wiki/entities/openai]], [[wiki/entities/boris-cherny]], [[wiki/entities/claude-code]], [[wiki/entities/claude-model-family]], [[wiki/entities/mcp]]
- **Key concepts**: [[wiki/concepts/ai-safety]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/constitutional-ai]], [[wiki/concepts/multi-agent-architecture]]
- **Sources**: [[wiki/sources/building-claude-code-boris-cherny]], [[wiki/sources/anthropic-harness-engineering-two-agent-architecture]], [[wiki/sources/anthropic-openai-memory-context-portability]]
