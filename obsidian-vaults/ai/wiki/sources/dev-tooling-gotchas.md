---
title: "Developer Tooling Gotchas (transferred notes)"
type: source
domain: ai
tags:
  - git
  - pre-commit
  - developer-experience
  - provenance
  - tooling
created: 2026-10-03
updated: 2026-10-03
raw: "transferred from CFAAI LLM wiki — manual dev note, no public URL"
---

# Developer Tooling Gotchas (transferred notes)

**Authors**: manual developer notes (CFAAI)
**Date**: 2026-06
**Type**: dev note distillation (provenance: inferred — no public source)

## Summary

Provenance stub for general developer-tooling gotchas transferred from a sibling CFAAI LLM wiki. The underlying notes were manual observations with no public URL, so dependent pages are marked `inferred`. Only vendor-neutral gotchas (reproducible on any repo) were imported; SAP/FAA-specific gotchas (Vault secret handling, `.env` inline-comment traps, MCP two-hop auth, MLflow tracing) were excluded as they are platform-coupled.

## Concepts Covered

- [[wiki/concepts/precommit-eof-fixer-gotcha]]

## Notes

The `end-of-file-fixer` gotcha reproduces on any repository that enables the standard `pre-commit` hooks of the same name — it is not SAP-specific, which is why it qualified for transfer.
