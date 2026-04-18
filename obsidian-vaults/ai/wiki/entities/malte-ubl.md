---
title: "Malte Ubl"
type: entity
domain: ai
tags:
  - person
  - engineer
  - cto
  - vercel
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/vercel-v0-d0-agent-lessons]]"
---

# Malte Ubl

Malte Ubl is the CTO of [[wiki/entities/vercel]], where he oversees the development of AI-native developer tools including v0 (AI-powered UI generation) and d0 (agent-native execution environment). His work represents one of the most concrete attempts by a major developer infrastructure company to rearchitect its tooling around AI agents rather than human developers.

## Background / History

Ubl is a veteran web platform engineer with deep roots in the browser and web standards community. He worked at Google for many years, where he was the technical lead for AMP (Accelerated Mobile Pages) — a large-scale infrastructure project that gave him experience building systems where correctness, performance, and developer experience must coexist at scale. At Vercel, he brings this infrastructure perspective to the challenge of building developer tools that work well with AI agents as primary users.

## Key Contributions / Features

**v0 (AI UI Generation)**: Under Ubl's technical leadership, Vercel built v0 — a tool that generates React UI components from natural language descriptions. v0 represents an early, high-quality example of AI-native product development: the output is runnable, deployable code rather than suggestions or snippets. It uses Vercel's deployment infrastructure as a fast feedback loop, allowing generated UI to be previewed instantly.

**d0 (Agent-Native Execution)**: Ubl has been involved in developing d0, Vercel's agent-native execution environment — infrastructure designed from the ground up to run AI agent workloads rather than adapting human-centric tooling for agent use. The key insight driving d0 is that agent execution patterns (high parallelism, variable duration, tool-calling loops) require different infrastructure primitives than traditional serverless.

**Lessons from Building Agent Tools**: Ubl has shared publicly the design lessons Vercel learned building agent-native tools — including the importance of fast iteration loops for agents, the challenge of evaluating agent output quality, and the infrastructure changes needed to support agent workloads at scale. (Source: [[wiki/sources/vercel-v0-d0-agent-lessons]])

## Role in AI Landscape

Ubl's work at Vercel positions the company as infrastructure for the agent-native development era, and his public commentary on building agent tools provides rare insight from someone who is building for agents as primary consumers rather than humans. His perspective bridges web infrastructure (where Vercel is a major player) and AI tooling, a combination that is increasingly relevant as AI agents become the primary generators of web applications.

## Connections

- **Related entities**: [[wiki/entities/vercel]], [[wiki/entities/claude-code]], [[wiki/entities/codex-cli]]
- **Key concepts**: [[wiki/concepts/agent-first-development]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/ai-native-infrastructure]]
- **Sources**: [[wiki/sources/vercel-v0-d0-agent-lessons]]
