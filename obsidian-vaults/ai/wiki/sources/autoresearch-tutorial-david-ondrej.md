---
title: "The only AutoResearch tutorial you’ll ever need"
type: source
domain: ai
tags:
  - autoresearch
  - evaluation
  - optimization
  - karpathy-loop
  - tutorials
created: 2026-04-21
updated: 2026-04-21
raw: "[[raw/The only AutoResearch tutorial you’ll ever need.md]]"
---

# The only AutoResearch tutorial you’ll ever need

**Authors**: David Ondrej
**Date**: 2026-03
**Type**: video-transcript

## Summary

This is a practical tutorialization of Karpathy's autoresearch pattern. It explains the core three-file setup (`program.md`, mutable artifact, evaluator), the fixed-metric logic that prevents cheating, and the broader claim that autoresearch is a general optimization loop rather than something limited to ML training.

Compared with the Balu Kosuri source already in the vault, this one is more beginner-facing and implementation-driven. Its value is in making the loop legible to builders who want to apply it to prompts, websites, trading strategies, or other measurable systems.

## Key Takeaways

- The evaluator must be fixed and untouchable or the loop will game the metric
- Autoresearch generalizes anywhere you can define one mutable artifact and one score
- The bottleneck is not execution but choosing the right metric and constraints
- Binary or clearly measurable outcomes make the loop materially more useful
- Karpathy's pattern is best understood as a repeatable engineering loop, not a magical AI capability

## Entities Mentioned

- [[wiki/entities/andrej-karpathy]]

## Concepts Covered

- [[wiki/concepts/autoresearch]]
- [[wiki/concepts/karpathy-loop]]
- [[wiki/concepts/eval-driven-development]]
- [[wiki/concepts/skill-md]]

## Notable Quotes

> "If you can score it, you can auto research it."

## Cross-Connections

This is the most tutorial-oriented companion to [[wiki/sources/karpathy-autoresearch-universal-skill]]. It also overlaps with the harness-evolution discussion in [[wiki/concepts/self-evolving-software]] by making the evaluator-centric loop explicit.
