---
title: "LangChain + MCP Sample Patterns (CFAAI sample-projects)"
type: source
domain: ai
tags:
  - langchain
  - mcp
  - agent-patterns
  - provenance
created: 2026-10-03
updated: 2026-10-03
raw: "transferred from CFAAI LLM wiki — internal sample-projects repo, no public URL"
---

# LangChain + MCP Sample Patterns (CFAAI sample-projects)

**Authors**: internal sample-projects codebase (CFAAI)
**Date**: 2026-07
**Type**: code sample distillation (provenance: inferred — no public source)

## Summary

Provenance stub for three general LangChain/LangGraph patterns transferred from a sibling CFAAI LLM wiki: the simple/memory/orchestrator agent ladder, the MCP-tool-to-`StructuredTool` conversion bridge (stdio and HTTP transports), and Claude Code CLI MCP registration. The underlying material came from an internal `sample_projects` repo with no public URL, so these pages are marked `inferred` rather than citing a verifiable source. All SAP/FAA-specific detail (internal proxy endpoints, FAA MCP URLs, production transparent-proxy debugging) was stripped on import; only the vendor-neutral patterns remain.

## Concepts Covered

- [[wiki/concepts/langchain-agent-patterns]]
- [[wiki/concepts/langchain-mcp-client]]
- [[wiki/concepts/claude-code-mcp-setup]]

## Entities Mentioned

- [[wiki/entities/langchain]]
- [[wiki/entities/langgraph]]
- [[wiki/entities/mcp]]
- [[wiki/entities/claude-code]]

## Notes

The production-grade implementation details (per-request client construction, `ToolMessage` flattening for Bedrock, `ExceptionGroup` peeling, transparent-proxy connection) were SAP-internal and intentionally excluded from this general-knowledge vault.
