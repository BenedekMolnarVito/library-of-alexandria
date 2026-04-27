---
title: "A Guide to Andrej Karpathy's AutoResearch: Automating ML with AI Agents"
type: source
domain: ai
tags:
  - autoresearch
  - ml-experiments
  - automation
  - andrej-karpathy
  - agents
created: 2026-04-27
updated: 2026-04-27
raw: "[[raw/A Guide to Andrej Karpathy's AutoResearch Automating ML with AI Agents.md]]"
---

# A Guide to Andrej Karpathy's AutoResearch: Automating ML with AI Agents

**Author**: Bex Tuychiev
**Published**: 2026-03-23
**Source**: DataCamp tutorial
**Type**: Tutorial / Educational guide

## Summary

A comprehensive guide to Andrej Karpathy's AutoResearch pattern for automating ML experimentation. Demonstrates how to run 100+ ML experiments overnight on a single GPU. Covers the three-file architecture (CLAUDE.md / idea.md + experiments file + results file), the ratchet loop (run → observe → iterate), empirical results, and practical limitations.

## Key Takeaways

- **Three-file architecture** — Instruction file, experiment tracker, results aggregator
- **Ratchet loop** — Agents run experiments, observe results, ratchet up hyperparameters incrementally
- **100+ experiments per night** — Feasible on single GPU with proper parallelization
- **Limitations** — Requires discrete parameter space; continuous optimization less effective; expensive in API costs
- **Educational value** — Shows how agents can own the scientific method, not just execute code

## Entities Mentioned

- [[wiki/entities/andrej-karpathy]]
- [[wiki/entities/claude-model-family]]

## Concepts Covered

- [[wiki/concepts/autoresearch]]
- [[wiki/concepts/karpathy-loop]]
- [[wiki/concepts/experimental-automation]]
- [[wiki/concepts/agentic-ml]]

## Personal Notes

Bridges AI agents and ML research. The ratchet loop is elegant—simple feedback mechanism that scales. Important reference for understanding how AutoResearch generalizes beyond coding to scientific experimentation.
