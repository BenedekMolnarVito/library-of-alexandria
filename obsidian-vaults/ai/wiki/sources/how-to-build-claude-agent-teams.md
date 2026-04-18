---
title: "How to Build Claude Agent Teams Better Than 99% of People"
type: source
domain: ai
tags:
  - agent-teams
  - multi-agent-orchestration
  - claude-code
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/How to Build Claude Agent Teams Better Than 99% of People.md]]"
---

# How to Build Claude Agent Teams Better Than 99% of People

**Authors**: Nate Herk | AI Automation
**Date**: 2026-03
**Type**: video-transcript

## Summary

Nate Herk provides a comprehensive guide to Claude Code's experimental Agent Teams feature, distinguishing it from sub-agents (independent, report back to orchestrator) vs agent teams (shared task list, direct inter-agent messaging). Teams are enabled via a single settings.json variable and prompted in natural language. Key demos include a full-stack app build with front-end dev + back-end dev + QA agent, a tmux split-pane visualization of parallel agents, and a workspace analysis team. The video covers prompting patterns, dos/don'ts, common pitfalls, and plan approval mode.

## Key Takeaways

- Agent teams differ from sub-agents: teams share a task list and can message each other directly without going through the orchestrator.
- Enable with one settings.json variable (experimental feature, disabled by default).
- Ideal team size: 3–5 agents; swarms of 10+ are expensive and harder to coordinate.
- Each agent should own specific files to avoid overwrites; deliverables and recipients should be explicitly named in prompts.
- Teammates inherit permissions, MCP servers, skills, and file access from the main session.
- Plan approval mode: agents plan first, get plans approved by orchestrator (or user) before executing.
- tmux allows a split-pane view where each agent appears as a separate colored panel you can interact with individually.
- Common pitfall: if an agent keeps stopping for permissions, pre-approve certain tools in project settings.

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/claude-sonnet-4-6]]
- [[wiki/entities/tmux]]

## Concepts Covered

- [[wiki/concepts/agent-teams]]
- [[wiki/concepts/multi-agent-orchestration]]
- [[wiki/concepts/parallel-agents]]
- [[wiki/concepts/sub-agents]]
- [[wiki/concepts/plan-approval-mode]]
- [[wiki/concepts/agent-communication]]
- [[wiki/concepts/shared-task-list]]
- [[wiki/concepts/claude-code-experimental-features]]
- [[wiki/concepts/agent-file-ownership]]

## Notable Quotes

> "Sub-agents work independently and then send their individual result back to the main agent. Agent teams have a team lead and a shared task list — individual teammates can talk to each other."

> "This is truly one of the most powerful AI agent features I've ever used, but you have to know how to use it."

## Cross-Connections

Closely related to [[wiki/sources/claude-code-paperclip-destroyed-openclaw]] — both solve multi-agent orchestration, but Agent Teams is native to Claude Code while Paperclip is an external platform. Connects to [[wiki/sources/from-ides-to-ai-agents-steve-yegge]]'s Gas Town (same orchestration paradigm, different tooling). The plan approval mode parallels the 'human in the loop' concepts from [[wiki/sources/claude-advisor-strategy-stop-using-opus]]. The file ownership pattern addresses the static planning weakness identified in [[wiki/sources/building-ai-agent-scratch-pure-python]]. Agent skills inherited by teammates connect to [[wiki/sources/claude-code-skills-got-better]].
