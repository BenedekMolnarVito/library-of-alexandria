---
title: "LangGraph ReAct Pattern"
type: concept
domain: ai
tags:
  - langchain
  - langgraph
  - agent-patterns
  - agent-architecture
  - tools
created: 2026-10-12
updated: 2026-10-12
sources:
  - "[[wiki/sources/langchain-mcp-sample-patterns]]"
---

# LangGraph ReAct Pattern

How to wire a reliable tool-using agent in LangGraph using an explicit `StateGraph` + `ToolNode` + `tools_condition` loop. This is the recommended production shape; the older `create_react_agent` helper is deprecated upstream.

## The shape

```
START
  │
  ▼
agent_node ──┐ tools_condition
  ▲          │
  │          ▼
  │   has tool calls? ──no──→ END
  │          │
  │          yes
  │          │
  │          ▼
  └──── ToolNode
```

Three components, one loop:

| Piece | What it is |
|---|---|
| `agent_node` | Your function. Prepends a versioned `SystemMessage`, calls `llm.ainvoke(messages)` on an LLM with all `@tool`-decorated tools bound, returns the response into `messages`. |
| `ToolNode` | LangGraph's built-in. Reads tool calls from the most recent `AIMessage`, dispatches each `@tool` from the registry, appends results as `ToolMessage`s. |
| `tools_condition` | LangGraph's built-in router. If the last `AIMessage` contains tool calls → route to `ToolNode`; otherwise → `END`. |

Plus a checkpointer (e.g. `MemorySaver` keyed by `thread_id`) for multi-turn conversation history.

## Why explicit, not `create_react_agent`

- **`create_react_agent` is deprecated.** Upstream LangGraph recommends the explicit pattern.
- **Customization.** You control the state schema, checkpointer wiring, error handling, and custom tool dispatch.
- **Debuggability.** Every transition is visible in code, not buried in a factory.
- **Traceability.** Easier to wire observability span boundaries around explicit node functions.

## Why one node, not a router

The temptation when adding retrieval is to split: "is this a doc question or a data question?" Resist. The recommended pattern is **one agent node with all tools bound** — the LLM picks. Reasons:

- LLMs do this better than rule-based routers in practice.
- Lower latency (no routing decision overhead).
- Mixed queries just work: a single request can call retrieval then a database tool in sequence.

## Why RAG is a tool, not a node

If RAG is a dedicated node, retrieval runs on every request — even for pure-data queries where it's wasted latency and embedding cost. Make `retrieve_relevant_documents` a `@tool`, let the LLM skip it when it's not needed.

## State schema

Keep the `TypedDict` small. Most state flows through `messages`:

```python
class AgentState(TypedDict):
    messages: list   # the canonical channel — system, human, AI, tool messages
    user_query: str
    session_id: str
```

The agent node only reads/writes via `messages`; everything else is helper context.

## Checkpointer choices

Start with `MemorySaver` (in-memory). When you need durable conversations or replica-shared state, swap to `SqliteSaver` or `PostgresSaver` from `langgraph.checkpoint.*` — the rest of the code only knows `BaseCheckpointSaver`, so the swap is local.

## Async-first

Every node and I/O-bound tool should be `async`. Required for:

- `astream_events(version="v2")` based streaming.
- Concurrent I/O (multiple tool calls are I/O-bound).

**Never call sync blocking code inside `async def`** — deadlocks the event loop.

## Related Concepts

- [[wiki/concepts/langchain-agent-patterns]] — general LangChain agent patterns
- [[wiki/concepts/agentic-arch-orchestration]] — loop control principles this implements
- [[wiki/concepts/agentic-arch-tools-mcp]] — tool design principles that apply to `@tool` functions
- [[wiki/concepts/multi-agent-orchestration]] — extending the pattern to coordinator/specialist setups

## Key Entities

- [[wiki/entities/langgraph]] — the framework this pattern uses
- [[wiki/entities/langchain]] — the parent ecosystem

## Sources

- [[wiki/sources/langchain-mcp-sample-patterns]]
