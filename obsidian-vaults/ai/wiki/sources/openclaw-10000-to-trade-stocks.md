---
title: "I Gave OpenClaw $10,000 to Trade Stocks"
type: source
domain: ai
tags:
  - openclaw
  - ai-agents
  - trading
  - finance
  - real-world-experiment
created: 2026-04-28
updated: 2026-04-28
raw: "[[raw/I Gave OpenClaw $10,000 to Trade Stocks.md]]"
---

# I Gave OpenClaw $10,000 to Trade Stocks

**Authors**: Nate Herk
**Date**: 2026-04
**Type**: video-transcript

## Summary

Nate Herk and collaborator Salman each built an AI trading bot using Claude (referred to as 'OpenClaw') and gave them $10,000 real cash to trade on Alpaca for 30 days during a volatile market (S&P fell ~8.46%). Nate's bot ended at $9,980 (lost only $19) while Salman's ended at $9,624 — both significantly outperforming the S&P 500 baseline. The bots also sent each other sarcastic trash-talk emails throughout the challenge. This experiment provides rare empirical data on AI agents in real-world adversarial financial conditions, and demonstrates multi-agent collaboration (research sub-agents, financial adviser persona) in a high-stakes domain.

## Key Takeaways

- Both AI bots outperformed the S&P 500 during a bear market month (S&P: -8.46%, Nate: -0.2%, Salman: -3.76%)
- Nate's strategy: simple — told the bot to research every 2 hours and make a plan, acting as a financial adviser with sub-agents; no predefined strategy
- Salman's strategy: Pareto principle — buy many stocks expecting 80% to lose and 20% to gain big (high-risk VC-style)
- Alpaca's day-trading limits constrained aggressive trading strategies
- Bot's self-advice at the end: 'Go all-in on energy from day one, use 10% trailing stops, never touch short-dated options'
- One bad options trade cost $550 — without it, Nate's bot would have been up 5.3%
- Challenge was run over a real bear market period (Feb 25 – March 30, 2026)

## Entities Mentioned

- [[wiki/entities/nate-herk]]
- [[wiki/entities/salman]]
- [[wiki/entities/claude-code]]
- [[wiki/entities/openclaw]]
- [[wiki/entities/alpaca]]
- [[wiki/entities/palantir]]
- [[wiki/entities/nvidia]]
- [[wiki/entities/microstrategy]]

## Concepts Covered

- [[wiki/concepts/ai-trading-bot]]
- [[wiki/concepts/algorithmic-trading]]
- [[wiki/concepts/multi-agent-finance]]
- [[wiki/concepts/ai-automation]]
- [[wiki/concepts/stock-market-ai]]

## Notable Quotes

> "Go all-in on energy from day one. Use 10% trailing stops instead of 2% and never touch short-dated options. One bad option trade costed us 550 bucks and without it we would have finished plus 5.3 in the green."

## Cross-Connections

Uses Claude-based multi-agent architecture in a financial domain, connecting to broader agentic AI applications. The use of sub-agents for research mirrors the multi-agent patterns in LangGraph/CrewAI ([[wiki/sources/comparing-6-python-ai-agent-frameworks]]). The 30-day real-money experiment provides empirical data on AI agents in adversarial, real-world conditions. The email-exchange between bots is an interesting emergent multi-agent behavior. Also by [[wiki/entities/nate-herk]], who covered the LLM wiki pattern in [[wiki/sources/karpathy-10x-claude-code-llm-wiki]]. Compare with [[wiki/sources/networkchuck-openclaw-right-now-review]] for OpenClaw's core architecture and security model.
