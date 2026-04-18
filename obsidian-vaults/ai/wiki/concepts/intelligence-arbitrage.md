---
title: "Intelligence Arbitrage"
type: concept
domain: ai
tags:
  - cost-optimization
  - model-routing
  - local-models
  - economics
  - karpathy-loop
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/300-dollars-auto-research-karpathy-loop]]"
---

# Intelligence Arbitrage

Intelligence arbitrage is the practice of routing AI tasks to the optimal model based on task complexity and cost requirements: cheap, fast local models for simple tasks; expensive frontier APIs for complex reasoning. The term was coined (or popularized) by Nate B Jones in the context of running the [[karpathy-loop]] on a $300 budget. The economic logic is straightforward — frontier API costs are dropping but remain non-trivial at scale, while local model quality is rising rapidly — but the practical implementation requires careful task decomposition and model capability mapping.

## Definition

Arbitrage, in finance, means exploiting price differences for the same asset across different markets. Intelligence arbitrage exploits capability differences for different tasks across different models: a task that requires complex multi-step reasoning "costs" a lot to route to GPT-4 or Claude Opus but nothing to route to a local Llama model — and if the local model handles the task adequately, the arbitrage is real.

The three-tier model that emerges from this framing:

**Local models** (Ollama, llama.cpp, Gemma on Apple Silicon): zero marginal cost, sub-second latency for small models, no internet required. Best for: formatting, simple transforms, classification, template filling, extracting structured data from well-formatted input.

**Efficient cloud models** (Claude Haiku, GPT-4o-mini, Gemini Flash): low cost (~$0.25/million tokens input), good quality for most tasks, standard API latency. Best for: moderate reasoning, most code generation, synthesis of well-structured inputs, most agent execution steps.

**Frontier models** (Claude Opus, GPT-4, Gemini Ultra): high cost (~$15/million tokens), highest reasoning quality, best for: complex multi-step reasoning, ambiguous or underspecified problems, final quality checks, tasks where errors are expensive.

## How It Works

The arbitrage decision is: given this specific subtask, what is the minimum model capability required to handle it reliably, and what is the cheapest model meeting that threshold?

In Nate B Jones' [[karpathy-loop]] implementation, the arbitrage was implemented as:
- A local Ollama model for generating candidate mutations (fast, cheap, adequate quality for creative text variation)
- Claude API for final evaluation of whether a candidate meets the target (expensive, but called only for promising candidates after local prescreening)

This two-stage structure — cheap generation, expensive evaluation — is the canonical intelligence arbitrage pattern for optimization loops. It can be applied wherever the evaluation function is more expensive than the generation function.

For agentic systems more generally, the pattern extends to multi-agent orchestration: the orchestrator (which must reason about routing, evaluate outputs, handle errors) uses a capable model; the executor subagents (which perform well-specified tasks) use efficient models. See [[advisor-executor-pattern]] for the architectural implementation.

## Why It Matters

The economics of intelligence arbitrage are driven by a rapidly closing quality gap. In 2022, using a local model for anything beyond trivial tasks was inadvisable — quality was too low. In 2024–2026, local models running on Apple Silicon (Gemma 4 27B, Qwen3-80B) achieve quality competitive with 2023-era frontier models on many tasks. The cost difference (zero vs. $15/million tokens) has stayed large while the quality difference has narrowed dramatically.

This trend — [[local-hard-takeoff]] — makes intelligence arbitrage increasingly attractive over time. Tasks that required frontier APIs in 2023 can be handled by local models in 2025 at zero marginal cost. The arbitrageur who correctly identifies which tasks have crossed the quality threshold captures pure cost savings.

The latency argument is separate from the cost argument and sometimes more important: a local model that responds in 200ms can enable interactive agentic applications that a cloud API with 2-second latency cannot. Real-time stream processing, low-latency decision making, and high-frequency optimization loops all benefit from local model latency regardless of cost.

## In Practice

Building an intelligence arbitrage system requires three components: a task decomposition strategy (breaking work into sub-tasks with identifiable complexity), a capability map (matching task types to minimum model requirements), and routing logic (directing each task to the appropriate model). The capability map is the hardest part to build and the most valuable to maintain — it encodes institutional knowledge about which tasks each model handles well.

A practical starting point: maintain two system configurations (local-heavy for development/iteration, frontier-heavy for production/quality-critical tasks) and switch between them explicitly. This is cruder than per-task routing but requires no routing logic and still captures most of the arbitrage value.

## Related Concepts

- [[wiki/concepts/local-hard-takeoff]] — the trend making local models increasingly viable
- [[wiki/concepts/local-ai-inference]] — the technical foundation of local model use
- [[wiki/concepts/karpathy-loop]] — the optimization context where intelligence arbitrage was introduced
- [[wiki/concepts/advisor-executor-pattern]] — architectural implementation of the arbitrage principle
- [[wiki/concepts/mixture-of-experts]] — architecture enabling local models to approach frontier quality

## Key Entities

- [[wiki/entities/nate-b-jones]] — coined/popularized the term

## Sources

- [[wiki/sources/300-dollars-auto-research-karpathy-loop]]
