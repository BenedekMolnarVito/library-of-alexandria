---
title: "LangChain Agent Patterns"
type: concept
domain: ai
tags:
  - langchain
  - langgraph
  - agent-patterns
  - agent-architecture
  - orchestration
created: 2026-10-03
updated: 2026-10-03
sources:
  - "[[wiki/sources/langchain-mcp-sample-patterns]]"
---

# LangChain Agent Patterns

Three runnable agent patterns for building LangChain agents with `langchain-anthropic` and LangGraph, distilled from a sample-projects codebase. All three share the same `.env` model config (`MODEL_FAST`, `MODEL`, `MODEL_LARGE` pointing at an LLM proxy). The progression — simple → memory → orchestrator — is a useful ladder from stateless baseline to multi-agent composition.

## Pattern 1: Simple Agent

The minimal baseline. Uses `create_agent(llm, tools=[], system_prompt=...)` from `langchain.agents`. No memory; each invocation is stateless.

## Pattern 2: Memory Agent

Two flavours, both keyed by `thread_id`:

**Simple memory** — passes a `MemorySaver` checkpointer directly to `create_agent`. The checkpointer accumulates messages per `thread_id` in-process. History is lost when the process exits.

**LangGraph memory** — builds an explicit `StateGraph` with an `add_messages` reducer on the state. The `MemorySaver` is attached at `graph.compile(checkpointer=memory)`. More verbose but gives full graph-level control and is the natural starting point for swapping in a persistent checkpointer.

To make memory cross-session persistent, replace `MemorySaver()` with:

```python
from langgraph.checkpoint.sqlite import SqliteSaver
checkpointer = SqliteSaver.from_conn_string("conversations.db")
```

## Pattern 3: Orchestrator (sub-agents as tools)

Wraps two agents as `@tool` functions, then gives those tools to a higher-level orchestrator agent. The orchestrator decides when to call `make_claim` and `validate_claim`, retrying until the validator returns `"status": "VERIFIED"`. This is the "sub-agents as tools" pattern — a simple way to compose specialists without a full multi-agent framework, and a concrete instance of the hub-and-spoke idea.

## Related Concepts

- [[wiki/concepts/langchain-mcp-client]] — give a LangChain agent MCP tools
- [[wiki/concepts/multi-agent-orchestration]] — the broader orchestration taxonomy
- [[wiki/concepts/advisor-executor-pattern]] — the generator+validator loop in Pattern 3
- [[wiki/concepts/agent-memory]] — checkpointer-backed memory in Pattern 2

## Key Entities

- [[wiki/entities/langchain]] — the framework
- [[wiki/entities/langgraph]] — the stateful graph layer

## Sources

- [[wiki/sources/langchain-mcp-sample-patterns]]
