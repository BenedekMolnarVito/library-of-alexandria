---
title: "Building an AI Agent from Scratch with pure Python"
type: source
domain: ai
tags:
  - agent-architecture
  - plan-and-execute
  - observability
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Building an AI Agent from Scratch with pure Python.md]]"
---

# Building an AI Agent from Scratch with pure Python

**Authors**: Christian Bernecker
**Date**: 2026-02
**Type**: article

## Summary

A hands-on tutorial for building a Plan-and-Execute AI agent using raw Python and direct API calls — no LangChain, no CrewAI. The article walks through the four components: Hands (tools defined via JSON schema as an API contract between Python and LLM), Planner (LLM decomposes user query into JSON task list), Executor (maps tasks to tools, runs Python functions, implements 3-stage retry loop), and Synthesizer (translates raw execution results into a coherent final answer). Includes enterprise-readiness patterns: Pydantic schema validation, self-correcting retry loops with error feedback, and observability/tracing for auditability.

## Key Takeaways

- Agent definition: LLM + Tools + Loop. The article builds these from scratch to expose the mechanical reality hidden by frameworks.
- Plan-and-Execute vs ReAct: Plan-and-Execute decomposes the full query into a JSON task list before acting — more robust for complex workflows, more predictable. ReAct thinks and acts one step at a time — more dynamic but less structured.
- The API Contract: every tool requires both a Python function (logic) and a JSON schema (description for the LLM) — the LLM sees only the schema, never the code.
- Executor design: for each task, ask the LLM which tool fits, call the Python function, store result in execution_plan (so later tasks can depend on earlier results).
- 3-stage retry loop: if JSON parsing/validation fails, send the error message itself back to the LLM as feedback — 'You gave me the wrong format. Here is the error: [ValidationError]. Try again.' This significantly increases reliability.
- Pydantic for schema validation: define tools as Pydantic models to enforce type contracts at code level, catching LLM output errors before they reach functions.
- Observability: log every Thought, Action, and Observation — the Execution Trace is the audit trail. 'I don't know why it did that' is not acceptable in enterprise.
- Weakness of Plan-and-Execute: static planning. If Task 1 reveals Task 2 is impossible, the agent may try anyway. Next article covers ReAct/Manager-Worker pattern for dynamic replanning.

## Entities Mentioned

- [[wiki/entities/christian-bernecker]]
- [[wiki/entities/langchain]]
- [[wiki/entities/crewai]]
- [[wiki/entities/openai]]

## Concepts Covered

- [[wiki/concepts/plan-and-execute-agent]]
- [[wiki/concepts/react-agent]]
- [[wiki/concepts/json-schema-tools]]
- [[wiki/concepts/pydantic-validation]]
- [[wiki/concepts/retry-loop]]
- [[wiki/concepts/agent-architecture]]
- [[wiki/concepts/tool-calling]]
- [[wiki/concepts/execution-trace]]
- [[wiki/concepts/observability]]

## Notable Quotes

> "An Agent is an LLM equipped with Tools and a Loop."

> "Notice the execution_system_prompt: 'If no tools fit to Task write None.' This prevents the agent from 'faking' an action when it doesn't have the right equipment."

> "In enterprise, 'I don't know why it did that' is an unacceptable answer. You must log every Thought, Action, and Observation."

> "The power of building from scratch is that you control the Security Layer. In an enterprise setting, your 'Executor' can include permission checks — ensuring the LLM never triggers a tool it isn't authorized to use."

## Cross-Connections

The Plan-and-Execute architecture described here is the conceptual foundation for all agentic systems discussed in the other sources — from [[wiki/entities/claude-code]] to the [[wiki/sources/agentic-saas-playbook-2026]] Control plane. The retry loop and Pydantic validation patterns connect directly to the production-readiness discussion in the SaaS Playbook. The observability requirement echoes the 'traces are everything' finding in [[wiki/sources/300-dollars-auto-research-karpathy-loop]]. The static planning weakness motivates the orchestration designs in [[wiki/sources/how-to-build-claude-agent-teams]] and [[wiki/sources/from-ides-to-ai-agents-steve-yegge]].
