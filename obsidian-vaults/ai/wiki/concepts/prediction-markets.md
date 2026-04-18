---
title: "Prediction Markets"
type: concept
domain: ai
tags:
  - prediction-markets
  - information-aggregation
  - polymarket
  - trading
  - ai-agents
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/polymarket-bot-438k-ai-arbitrage]]"
---

# Prediction Markets

Prediction markets are market-based mechanisms for aggregating information about uncertain outcomes: participants bet on whether specific events will occur, and the prices that emerge reflect the aggregate probability estimates of all market participants. They function as information aggregation systems — when participants have genuine knowledge about an outcome and can profit by trading on that knowledge, the market price becomes a weighted aggregate of all available information. Polymarket is the leading crypto-based prediction market platform. AI agents can participate in prediction markets as traders, using language model reasoning to identify mispriced probabilities — as demonstrated by Nate Herk's $438K automated trading bot.

## Definition

A prediction market operates as follows: a question is posed ("Will X happen by date Y?"), shares are issued for YES and NO outcomes, and shares for the outcome that occurs pay out at $1 while shares for the non-occurring outcome pay out at $0. The market price of a YES share at any time reflects the market's collective estimate of the probability that X will happen.

For example: if YES shares for "Will Company X announce earnings above estimates?" trade at $0.72, the market estimates a 72% probability of above-estimates earnings. Traders who believe the probability is higher buy YES shares; traders who believe it's lower sell them (or buy NO). The price adjusts until no more profitable trades exist.

Prediction markets have strong theoretical properties: they aggregate dispersed private information (each trader's private knowledge about the outcome) more efficiently than other forecasting mechanisms. In domains with verifiable outcomes and active market participants, they produce well-calibrated probability estimates.

## How It Works

AI-assisted prediction market trading works by identifying markets where the price misrepresents the true probability — where the model's estimate of the probability differs from the market price by enough to justify a trade after accounting for costs.

Nate Herk's $438K trading bot used the following approach:
1. Monitor Polymarket for newly listed or recently updated markets
2. Use an LLM to analyze available information (news, base rates, expert estimates, related market prices) about the outcome
3. Generate a probability estimate for the outcome
4. Compare the LLM estimate to the current market price
5. Execute a trade when the discrepancy exceeds a threshold (the "edge")
6. Close positions as events resolve or as new information moves the market price toward the model's estimate

The LLM provides reasoning capability that goes beyond simple statistical analysis: it can evaluate qualitative information (expert statements, context-specific factors, analogical reasoning from similar historical events) that simpler models can't process. This is [[intelligence-arbitrage]] applied to information trading.

## Why It Matters

Prediction markets are a direct application of [[intelligence-arbitrage]] economics: if you have better information processing capability than the average market participant, you can profit from the discrepancy between your probability estimate and the market price. An LLM with access to current information and strong reasoning capability has a potential information processing advantage over individual traders making intuitive judgment calls.

The practical significance is broader than trading: prediction markets are useful tools for decision-making under uncertainty wherever they exist. Organizations that consult Polymarket prices for relevant questions (election outcomes, regulatory decisions, technology release timing) get access to aggregated information that no single analyst can match.

The connection to [[agentic-saas]] is also direct: automated prediction market trading is a specific instance of an agentic workflow that produces outcomes (profitable trades) based on continuous information monitoring and LLM reasoning. It demonstrates that agentic workflows can be commercially valuable in information-rich, outcome-verifiable domains.

## In Practice

Prediction market arbitrage faces several practical challenges: market liquidity (thin markets mean large spreads that consume the edge), resolution timing (capital tied up waiting for event resolution), and information freshness (markets already price in widely available information — the edge comes from information that isn't yet reflected in prices, which requires fast reaction).

The $438K bot success was achieved in a specific market environment and with access to information processing capabilities that the average participant lacked. Future market efficiency (as more AI traders enter) will likely compress the available edge over time — the same commoditization dynamic that affects [[intelligence-arbitrage]] everywhere.

## Related Concepts

- [[wiki/concepts/intelligence-arbitrage]] — information routing for competitive advantage
- [[wiki/concepts/agentic-saas]] — prediction market trading as an agentic workflow
- [[wiki/concepts/agentic-loop]] — the execution cycle for continuous market monitoring

## Key Entities

- [[wiki/entities/polymarket]] — leading prediction market platform
- [[wiki/entities/nate-herk]] — $438K AI trading bot

## Sources

- [[wiki/sources/polymarket-bot-438k-ai-arbitrage]]
