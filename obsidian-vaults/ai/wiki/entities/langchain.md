---
title: "LangChain"
type: entity
domain: ai
tags:
  - org
  - open-source
  - agent-framework
  - langsmith
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/langchain-deep-agents]]"
  - "[[wiki/sources/comparing-6-python-ai-agent-frameworks]]"
---

# LangChain

LangChain is an open-source framework company that builds tooling for LLM application development, most notably [[wiki/entities/langgraph]] (stateful multi-agent orchestration) and LangSmith (evaluation and observability). It became the first major "LLM framework" to achieve widespread adoption and has evolved from a simple prompt chaining library into a comprehensive agent orchestration platform.

## Background / History

LangChain was founded by Harrison Chase in 2022 and grew explosively as developers sought structured ways to build LLM applications — combining prompts, retrieval, tools, and memory in reproducible patterns. The initial version was essentially a library for chaining LLM calls with context management; it has since evolved significantly, with LangGraph representing a more principled approach to multi-agent architectures based on graph theory rather than linear chains. LangChain has raised substantial VC funding and has transitioned from a pure open-source project to a commercial entity offering hosted LangSmith as a SaaS product.

## Key Contributions / Features

**LangChain (Core Framework)**: The original library provided abstractions for prompt templates, LLM wrappers, vector stores, document loaders, and agents. While often criticized for complexity and abstraction leakage, it dramatically accelerated prototype development and established vocabulary that became industry standard (chains, agents, tools, memory).

**LangGraph**: LangChain's second-generation framework, built on graph theory rather than chain metaphors. Nodes represent agents or tools, edges represent conditional routing logic, and state is explicitly managed as the graph executes. LangGraph is designed for production multi-agent systems where control flow is complex, state persistence is required, and human-in-the-loop checkpoints are needed. In a comparison of six Python agent frameworks, LangGraph was identified as the most production-ready option. (Source: [[wiki/sources/comparing-6-python-ai-agent-frameworks]])

**LangSmith**: LangChain's commercial evaluation and observability platform for LLM applications. LangSmith provides tracing (recording every LLM call and tool invocation in an application), evaluation (running test suites against models), and dataset management. As agent systems become more complex, observability tools like LangSmith become essential for understanding what agents are actually doing and why.

**Deep Agents Research**: LangChain has published research and documentation on "deep agents" — agents that can reason over long time horizons, maintain complex state, and orchestrate other agents as subprocesses. (Source: [[wiki/sources/langchain-deep-agents]])

## Role in AI Landscape

LangChain's position is that of infrastructure provider for the agent era — attempting to be the "Rails of AI" by providing opinionated, high-productivity abstractions over the underlying LLM complexity. Whether this abstraction strategy succeeds long-term is contested: some practitioners find LangChain's abstractions helpful, others find them leaky and prefer to work closer to the model API. LangGraph's graph-based approach is more defensible architecturally than the original chain approach, and its adoption as the multi-agent framework of choice by production teams is a signal that the company has found a sustainable niche.

## Connections

- **Related entities**: [[wiki/entities/langgraph]], [[wiki/entities/anthropic]], [[wiki/entities/openai]], [[wiki/entities/mcp]]
- **Key concepts**: [[wiki/concepts/multi-agent-architecture]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/llm-evaluation]], [[wiki/concepts/agent-orchestration]]
- **Sources**: [[wiki/sources/langchain-deep-agents]], [[wiki/sources/comparing-6-python-ai-agent-frameworks]]
