---
title: "Graph Percolation Threshold"
type: concept
domain: ai
tags:
  - graphrag
  - knowledge-graphs
  - network-science
  - retrieval
created: 2026-04-20
updated: 2026-04-20
sources:
  - "[[wiki/sources/phase-transition-knowledge-graph-agent-memory]]"
---

# Graph Percolation Threshold

The graph percolation threshold is the connectivity tipping point where a fragmented graph transitions into a large connected component, enabling reliable multi-hop traversal.

## Definition

In memory and GraphRAG contexts, this threshold is often discussed via average node degree and giant-component fraction. Below threshold, knowledge remains isolated; above threshold, cross-document reasoning paths become available.

## Why It Matters

This concept explains why many graph memory systems appear to improve non-linearly: usefulness can remain low for extended periods, then jump once connectivity crosses a critical point.

## Practical Implications

- Track average degree and giant-component ratio as operational metrics.
- Prioritize bridge-building links and entity resolution when graphs are subcritical.
- Avoid judging graph memory quality without checking connectivity state.

## Related Concepts

- [[wiki/concepts/agent-memory]]
- [[wiki/concepts/eval-driven-development]]

## Sources

- [[wiki/sources/phase-transition-knowledge-graph-agent-memory]]

