---
title: "OpenClaw......RIGHT NOW??? (it's not what you think)"
type: source
domain: ai
tags:
  - openclaw
  - ai-agents
  - security
  - tutorial
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/OpenClaw......RIGHT NOW (it's not what you think).md]]"
---

# OpenClaw......RIGHT NOW??? (it's not what you think)

**Authors**: NetworkChuck
**Date**: 2026-03
**Type**: video-transcript

## Summary

NetworkChuck's in-depth tutorial and honest review of OpenClaw — the AI agent framework with 308K GitHub stars that lets you run autonomous AI agents on a VPS or home server. The video covers full installation, security hardening (firewall, SSH tunnel, gateway tokens, tool permission profiles), and a personal verdict: OpenClaw is real and useful for purpose-built agents, but NetworkChuck prefers Claude Code for serious work. He uses it for a personal IT team running his home lab, a Japanese-speaking personal assistant (Hermione), and a fitness assistant. The video is notable for distinguishing between OpenClaw's genuine utility and the hype that drove its explosive GitHub growth — it packaged existing agentic tooling into a clean install, making the concept of 'AI using a computer' feel accessible.

## Key Takeaways

- OpenClaw got 308K GitHub stars — more than React — because it packaged existing agentic tooling into a clean install and made the concept of 'AI using a computer' feel accessible, not because the technology itself was new
- Key security steps: run `openclaw security audit`, ensure web UI is NOT exposed to public internet (bound to 127.0.0.1 by default), enable UFW firewall allowing only SSH, use SSH tunnel for web UI access
- Tool permission profiles: `coding` (default, limited) vs `full` (all system tools visible); combined with `tools.exec` setting (full/allow-list/ask/off) to control what agent can autonomously do
- Redlining in agents.md: agent instructions that act as behavioral guardrails — 'red lines' (stop and ask), 'yellow lines' (do but log), 'always allow'
- 12% of skills found in ClawHub contained malware — vet everything before installing community skills
- Jensen Huang called OpenClaw 'the OS for personal AI'; Nvidia built Nemo Claw; Anthropic building their own — big companies are converging on the same idea
- NetworkChuck's actual use: IT team (CTO + specialists) managing home lab via ticketing, personal assistant making phone calls in Japanese, fitness trainer persona

## Entities Mentioned

- [[wiki/entities/networkchuck]]
- [[wiki/entities/openclaw]]
- [[wiki/entities/peter]]
- [[wiki/entities/jensen-huang]]
- [[wiki/entities/nvidia]]
- [[wiki/entities/anthropic]]
- [[wiki/entities/nemo-claw]]

## Concepts Covered

- [[wiki/concepts/ai-agents]]
- [[wiki/concepts/agent-security]]
- [[wiki/concepts/tool-permission-profiles]]
- [[wiki/concepts/redlining]]
- [[wiki/concepts/agent-instructions]]
- [[wiki/concepts/ssh-tunneling]]
- [[wiki/concepts/agentic-os]]

## Notable Quotes

> "What this did, and this is the reason everyone freaked out, is it made everything seem accessible. It packaged everything together in one clean install."

> "For serious work, I am normally going to be using Claude code. But I do use OpenClaw."

> "12% of skills were found with malware. Vet everything."

## Cross-Connections

Directly connects to the broader OpenClaw ecosystem ([[wiki/sources/openclaw-gemma4-free-private-ai]], [[wiki/sources/openclaw-10000-to-trade-stocks]]). NetworkChuck's comparison of OpenClaw vs Claude Code mirrors DHH's own agent stack comparison in [[wiki/sources/dhh-new-way-writing-code-agent-first]] (OpenCode vs Claude Code). The 'redlining' concept in agents.md is semantically identical to the CLAUDE.md behavioral instructions pattern that appears throughout the Claude Code leak analysis in [[wiki/sources/claude-code-source-leaked-worth-learning]].
