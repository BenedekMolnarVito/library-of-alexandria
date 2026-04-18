---
title: "Master 95% of Claude Code Skills in 28 Minutes"
type: source
domain: ai
tags:
  - claude-code
  - skills
  - parallel-agents
  - productivity
  - automation
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Master 95% of Claude Code Skills in 28 Minutes.md]]"
---

# Master 95% of Claude Code Skills in 28 Minutes

**Authors**: Nate Herk | AI Automation
**Date**: 2026-02
**Type**: video-transcript

## Summary

A practical tutorial on Claude Code "skills" — reusable markdown instruction files stored in `.claude/skills/` that teach agents a repeatable workflow. Each skill file uses YAML frontmatter with a name and description, followed by step-by-step instructions. The author demonstrates running four parallel Claude Code agents simultaneously across four different skills: morning planning, project pulse check, diagram generation, and YouTube comment analysis — all completing in roughly 30 seconds.

The tutorial covers skill anatomy, how to embed reference files (tone-of-voice documents, channel data, business context), building skills incrementally through refinement, and the leverage multiplier when skills are shared across a team. Skills function as "SOPs for AI agents" — the same way a human reads a standard operating procedure, an agent reads the skill file and executes it deterministically. Skills can also run sub-agents, call APIs, and execute scripts.

## Key Takeaways

- Skills are markdown files at `.claude/skills/<skillname>/skill.md` with YAML frontmatter and a step-by-step workflow section
- Running 4 agents in parallel on different skills simultaneously took ~30 seconds to invoke — a significant personal leverage multiplier
- Skills can include reference files either self-contained or as path references to external data (tone docs, channel history, etc.)
- Skills function as "SOPs for AI agents" — a human reads an SOP the same way an agent reads a skill and executes it
- Skills improve over time through incremental refinement; team-shared skills compound productivity across the entire organization
- Skills can run sub-agents, call APIs, and execute scripts — not limited to text generation
- More context baked into a skill (business data, priorities, history) directly improves output quality

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/clickup]]
- [[wiki/entities/excalidraw]]

## Concepts Covered

- [[wiki/concepts/claude-code-skills]]
- [[wiki/concepts/reusable-agent-instructions]]
- [[wiki/concepts/parallel-agent-execution]]
- [[wiki/concepts/agent-sop]]
- [[wiki/concepts/skill-anatomy]]
- [[wiki/concepts/reference-files]]
- [[wiki/concepts/personal-ai-assistant]]
- [[wiki/concepts/team-leverage]]

## Notable Quotes

> "In one day I can get a week's worth of output... one person can figure out the best way to do something and turn it into a skill that the entire team can use."

> "This speed of work that we're able to achieve right now feels insane, but that is going to become normal. And if you can't do that, you instantly become way too slow and way too expensive."

## Cross-Connections

Claude Code skills are the practical implementation of the reusable agent context concept discussed abstractly in the AGENTS.md schema from [[wiki/sources/stop-vibe-coding-4-file-system]]. The parallel agent execution demonstrated here mirrors the subagent spawning pattern in [[wiki/sources/langchain-deep-agents]]. The "SOPs for agents" framing connects to the spec-driven development philosophy throughout this corpus — and to the [[wiki/sources/japanese-firm-markdown-employee]] case study where skills compress multi-step expert workflows. See also [[wiki/sources/ollama-claude-code-free]] by the same author for the cost-reduction angle.
