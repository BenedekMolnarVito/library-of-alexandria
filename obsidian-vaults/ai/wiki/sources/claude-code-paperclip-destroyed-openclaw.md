---
title: "Claude Code + Paperclip Just Destroyed OpenClaw"
type: source
domain: ai
tags:
  - ai-agent-orchestration
  - multi-agent-systems
  - zero-human-companies
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/Claude Code + Paperclip Just Destroyed OpenClaw.md]]"
---

# Claude Code + Paperclip Just Destroyed OpenClaw

**Authors**: Nate Herk | AI Automation
**Date**: 2026-03
**Type**: video-transcript

## Summary

Nate Herk demonstrates Paperclip, a free open-source MIT-licensed AI orchestration platform that lets users run entire companies staffed by Claude Code agents. Each agent has heartbeat schedules, configurable soul/instructions/tools files, per-agent budgets, and a ticketing system. The video walks through building a company from scratch, hiring agents (CEO hires engineer), and using a parallel Claude Code project as a 'partner in crime' to manage Paperclip itself.

## Key Takeaways

- Paperclip is a free, open-source orchestration layer for running multi-agent 'companies' on top of Claude Code.
- Agents wake up on heartbeat schedules (every 4/8/12 hours) with fresh context and check their task list each time.
- Each agent has four config files: agents, heartbeat, soul, and tools — controlling identity, behavior, and capabilities.
- Per-agent budget controls let you cap monthly token spend per role.
- You can run multiple 'companies' inside one Paperclip instance, or use departments for different business units.
- Setting up a Claude Code project that understands the Paperclip architecture dramatically improves agent quality.
- Paperclip integrates natively with GitHub repos for code-building agents.

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/paperclip]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/openclaw]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/dota]]

## Concepts Covered

- [[wiki/concepts/ai-agent-orchestration]]
- [[wiki/concepts/heartbeat-protocol]]
- [[wiki/concepts/multi-agent-systems]]
- [[wiki/concepts/agent-configuration]]
- [[wiki/concepts/zero-human-companies]]
- [[wiki/concepts/agentic-task-management]]

## Notable Quotes

> "In a matter of 30 minutes of me coming in here acting as a board… I have a CEO, a social media agent, a marketer that manages a copywriter, a strategist, a designer, and a researcher."

> "Every day he would have 20 different terminals running, 20 different Cloud Code sessions running… Paperclip is solving that orchestration problem."

## Cross-Connections

Directly connects to the Claude Code skills ecosystem and the broader trend of 'agentic companies.' Closely related to [[wiki/sources/how-to-build-claude-agent-teams]] (another multi-agent pattern native to Claude Code). The heartbeat pattern mirrors [[wiki/entities/openclaw]]'s proactive agent design, as also described in [[wiki/sources/hermes-agent-vs-openclaw]]. The per-agent budget pattern is the orchestration-level implementation of the advisor strategy discussed in [[wiki/sources/claude-advisor-strategy-stop-using-opus]]. The soul/memory file concept parallels Hermes Agent's architecture.
