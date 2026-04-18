---
title: "AI Domain Overview"
type: overview
domain: ai
tags:
  - artificial-intelligence
  - machine-learning
  - llm
  - agents
  - agentic-coding
  - knowledge-management
created: 2026-04-18
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]"
  - "[[wiki/sources/ai-50x-faster-getting-2x-wrong-thing]]"
  - "[[wiki/sources/wall-street-285b-ai-agents-review]]"
  - "[[wiki/sources/building-claude-code-boris-cherny]]"
---

# AI Domain Overview

This wiki tracks the AI landscape as of early 2026 — a pivotal moment when frontier models crossed the threshold from "impressive demos" into tools that are restructuring how software is written, how knowledge is managed, and how organizations operate. The 64 sources ingested represent a cross-section of practitioners, researchers, strategists, and builders who are living through this transition in real time.

## The Central Thesis

The dominant through-line across this corpus is a single insight, articulated most crisply by **Andrej Karpathy**: *"Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase."* This metaphor is not just about note-taking — it captures a generalized architectural pattern that is showing up everywhere: plain markdown files as the substrate, AI as the maintenance layer, and humans as the source-finders and question-askers.

The pattern appears as:
- The **LLM wiki** (Karpathy's personal knowledge base; Balu Kosuri's open-source implementation)
- The **autoresearch loop** (AI optimizes code or prompts via keep/discard until good)
- **CLAUDE.md / AGENTS.md** (standing instructions that encode your corrections once, forever)
- **SOUL.md** (persistent agent identity that survives session resets)
- **Self-evolving code memory** (Cole Medin's context-portal: the codebase documents itself for the AI)

All of these are instances of the same architecture: **AI owns and maintains a plain-text artifact; humans supply raw material and judgment.**

## The Landscape in Five Themes

### 1. Agentic Coding Has Crossed the Threshold

By early 2026, AI coding went from "copilot that suggests lines" to "agent that implements features end-to-end." **Boris Cherny** at Anthropic built **Claude Code** — a terminal agent that reads/writes files, runs commands, browses the web, and spawns sub-agents. **OpenAI** shipped **Codex CLI** as a direct competitor. Both are being run by practitioners 8+ hours a day (see Nate Herk's 100-hour review, Pawel Jozefiak's 10x'd workflow).

The critical bottleneck is no longer model capability but **first-pass reliability**: a local Gemma 4 model generating tokens 5x faster than cloud GPT still loses on wall-clock time because it takes multiple repair passes. The lesson: *quality beats speed for agentic tasks*.

**Karpathy's shift** — from 80% manual to 80% agent-driven coding in December 2025 — is treated as a signal event. It validated that frontier engineers have found a workflow where agents are genuinely productive, not just occasionally helpful.

### 2. The LLM Wiki Pattern Is the Library of Alexandria's Own Foundation

Eight of the 64 sources directly discuss, implement, or extend Karpathy's LLM wiki pattern. This is significant: the source corpus is documenting the same architecture as the system it is being ingested into. Key implementations:

- **Balu Kosuri** built a complete implementation in 3 Cursor prompts and open-sourced it
- **Cole Medin** built a self-evolving memory system (context-portal) that feeds the codebase's own documentation back to the AI
- **evoailabs** surveyed 5 adjacent ecosystem projects (Waykee, Sage-Wiki, Thinking-MCP, ELF, qmd)
- **Tobi Lütke** (Shopify CEO) built `qmd`, a hybrid BM25+vector local search tool for personal PKM

The RAG-vs-LLM-wiki debate is settled in this corpus: RAG starts from scratch on every query; the LLM wiki compounds knowledge over time. A Japanese firm's practical test confirmed that well-structured markdown outperformed a $50M vector database for their knowledge retrieval use case.

### 3. Local AI Is Becoming Production-Grade

The open-source model landscape advanced dramatically in Q1-Q2 2026:

- **Gemma 4** (Google DeepMind): tool-calling jumped from 6.6% to **86.4%** on tau2-bench — the threshold that makes local agentic coding practical. MoE architecture means 27B parameters at only 3.8B active params/token.
- **GLM 5.1** (ZhipuAI): free OpenAI-compatible API, 128K context, strong UI generation. Multiple users cancelled $100/month Claude subscriptions.
- **Step-3.5-Flash** (StepFun): 196B MoE model competitive with GPT-5.4 Turbo on reasoning benchmarks.
- **Exo** (Exo Labs): pool consumer devices into an 80B AI cluster. Two Macs running Qwen3-Next-80B at 70-80 tok/s with zero cloud cost.

**Nate B Jones' "local hard takeoff" thesis**: the next major capability leap will come from edge/local models, not cloud giants. The cost/latency advantage is compounding as MoE efficiency, Apple Silicon bandwidth, and distributed inference (Exo) converge.

**Intelligence arbitrage** — routing tasks to the optimal model (cheap local for simple tasks, expensive API for complex ones) — is the practitioner's response to this landscape.

### 4. The Infrastructure Gap: We're Bottlenecking on Human-Speed APIs

Nate B Jones identified what may be the most important structural insight in the corpus: AI inference is 50x faster than it was two years ago, but developers are only getting 2-3x productivity gains. The reason: **tool calls** (file system, APIs, databases, compilers) dominate wall-clock time in agentic loops, and all of those tools were designed for human speed.

The fix requires three layers:
1. **Faster existing tools** (TypeScript 7 rewritten in Go for 10x speed)
2. **Agent-native primitives**: persistent containers, branchFS (sub-second branch creation), shared KV cache across multi-agent runs
3. **Bitter lesson**: general agent-native methods will eventually outperform all human-engineered scaffolding

MCP (Model Context Protocol) is a stopgap — it wraps human-friendly APIs for agent consumption but adds latency. The real solution is infrastructure built from scratch for agent speed.

### 5. Strategic Disruption: The $285B SaaS Reckoning

Wall Street's 2026 sell-off of SaaS middleware stocks was, per Nate B Jones, **correct**: AI agents can now replace the routine data-pipeline, form-processing, and dashboard-generating SaaS products that make up the bulk of the $285B market.

Amazon's story is the sharpest case study: after a December 2024 production outage caused by **dark code** (AI-generated code nobody fully understood), they mandated **spec-driven development** — write a complete specification before delegating to an agent. Some teams were restructured from 20 engineers to 2.

**Five safe places to build** (per Nate B Jones):
1. **Verifiable domains** (legal, medical, financial compliance — AI advises but humans certify)
2. **Hardware integration** (physical-world interfaces)
3. **Relationship capital** (trust networks that AI cannot replicate)
4. **Synthetic data and evaluation** (the training layer)
5. **Orchestration and governance** (managing agents themselves)

## Key People in This Corpus

| Person | Role | Key Contribution |
|--------|------|-----------------|
| **Andrej Karpathy** | Independent researcher | LLM wiki, autoresearch, CLAUDE.md patterns |
| **Boris Cherny** | Anthropic engineer | Built Claude Code from scratch |
| **Nate B Jones** | Strategist | Intelligence arbitrage, dark code, 5 safe places |
| **Nate Herk** | Practitioner | 100-hour Claude Code review, $438K Polymarket bot |
| **Balu Kosuri** | Builder | Open-source LLM wiki; autoresearch universal skill |
| **Cole Medin** | Builder | Context-portal self-evolving memory |
| **Steve Yegge** | Engineer | "IDEs are dying; agents replace them" |
| **DHH** | Creator of Rails | Craft-preserving AI adoption model |
| **Chip Huyen** | ML systems author | Evaluation frameworks for production AI |
| **Gergely Orosz** | Pragmatic Engineer | Long-form interviews with frontier AI engineers |

## Open Questions

> [!question] Open Question: When does local hard takeoff actually arrive?
> Gemma 4's tool-calling leap (6.6%→86.4%) happened in one model generation. If the next generation closes the remaining gap on complex reasoning, local inference becomes the default for most coding tasks. The question is timing and which benchmarks to trust.

> [!question] Open Question: What is the right memory architecture for production agents?
> Anthropic and OpenAI have different philosophies. SOUL.md + markdown files is the practitioner's grassroots solution. Context-portal is a codebase-specific implementation. No consensus on the right architecture for long-running agents with months of accumulated context.

> [!question] Open Question: Is dark code a solvable problem?
> Amazon's spec-driven mandate helps but doesn't eliminate the problem. Karpathy admits that even with CLAUDE.md, failure modes don't fully go away. The deeper question is whether AI-written code will ever be as auditable as human-written code.

> [!question] Open Question: When does agent-native infrastructure replace human-speed APIs?
> Nate B Jones argues MCP is a stopgap and the real fix requires branchFS, persistent containers, and shared KV caches. But these require significant platform investment. Timeline unclear.

## Scope Notes

This wiki focuses on **AI tooling, practices, and strategy as of early 2026**. It deliberately emphasizes:
- The practitioner perspective (what works in practice, not just in benchmarks)
- The knowledge management angle (the LLM wiki pattern is the soul of this project)
- Strategic/business implications (SaaS disruption, agent economics)
- Open-source and local AI (privacy, cost, autonomy from cloud platforms)

It does not currently cover: foundational AI research (transformers, scaling laws), AI safety/alignment theory, computer vision, robotics, or policy/regulation in depth.
