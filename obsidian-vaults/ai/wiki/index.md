---
title: "AI Wiki Index"
type: index
domain: ai
tags:
  - index
  - navigation
  - ai
created: 2026-04-18
updated: 2026-04-21
sources:
  - "[[wiki/overview]]"
---

# AI Wiki Index

A catalog of all pages in the AI knowledge wiki. Updated on every ingest.

---

## Overview

- [[wiki/overview]] — High-level overview of the AI domain and current landscape
- [[wiki/log]] — Chronological record of ingest, update, query, and lint actions

## Entities

### People

- [[wiki/entities/andrej-karpathy]] — AI researcher, OpenAI co-founder, originator of LLM wiki, autoresearch, and CLAUDE.md patterns
- [[wiki/entities/boris-cherny]] — Anthropic engineer who built Claude Code from scratch
- [[wiki/entities/nate-b-jones]] — Creator of *AI News & Strategy Daily*; frameworks: intelligence arbitrage, dark code, SOUL.md
- [[wiki/entities/nate-herk]] — AI automation practitioner; built $438K Polymarket bot; 100-hour Claude Code review
- [[wiki/entities/mo-gawdat]] — Former Google X executive focused on AI macro strategy, labor disruption, and ethical adaptation
- [[wiki/entities/tiago-forte]] — Popularized the second-brain framework that LLM wikis partly inherit and automate
- [[wiki/entities/chip-huyen]] — ML systems author (*Designing ML Systems*); AI evaluation frameworks
- [[wiki/entities/steve-yegge]] — Veteran engineer (Google/Amazon/Sourcegraph); "IDEs are dying" thesis
- [[wiki/entities/dhh]] — Creator of Rails, co-founder of 37signals; craft-preserving AI adoption model
- [[wiki/entities/gergely-orosz]] — Author of *The Pragmatic Engineer*; deep-dive AI engineering interviews
- [[wiki/entities/cole-medin]] — Builder of context-portal (self-evolving Claude Code memory)
- [[wiki/entities/balu-kosuri]] — Open-source LLM wiki implementer; generalized autoresearch into universal skill
- [[wiki/entities/forrest-chang]] — Distilled Karpathy's CLAUDE.md into 60-line file; 3,500+ GitHub stars
- [[wiki/entities/networkchuck]] — IT/networking YouTuber; OpenClaw + Gemma 4 local AI tutorials
- [[wiki/entities/malte-ubl]] — CTO of Vercel; building v0 (AI UI gen) and d0 (agent-native execution)
- [[wiki/entities/alex-dunlop]] — Short-form AI tips; 75% Claude Code token reduction technique
- [[wiki/entities/tobi-lutke]] — CEO of Shopify; built qmd hybrid BM25+vector search for personal PKM
- [[wiki/entities/manjunath-janardhan]] — Demonstrated Exo two-Mac 80B cluster at 70–80 tok/s
- [[wiki/entities/daniel-vaughan]] — Benchmarked Gemma 4 + Codex CLI; finding: quality > speed for agentic coding
- [[wiki/entities/nick-saraev]] — Applied autoresearch pattern to text-to-image; 32→40/40 in 12 minutes
- [[wiki/entities/danish-sofi]] — Cancelled $100/month Claude subscription after trying GLM 5.1
- [[wiki/entities/milla-jovovich]] — Public co-creator and architectural lead voice behind MemPalace
- [[wiki/entities/ben-sigman]] — Engineer credited across sources for MemPalace implementation

### Organizations

- [[wiki/entities/anthropic]] — AI safety company; creator of Claude family, Claude Code, MCP
- [[wiki/entities/openai]] — Creator of GPT family, Codex CLI, ChatGPT
- [[wiki/entities/google-deepmind]] — Google Brain + DeepMind merged; creator of Gemma 4 open model family
- [[wiki/entities/vercel]] — Developer infrastructure; building v0 (AI UI gen) and d0 (agent-native execution)
- [[wiki/entities/uber]] — Agentic engineering case study; some teams reduced from 20 engineers to 2
- [[wiki/entities/zhipuai]] — Chinese AI lab; GLM 5.1 free OpenAI-compatible API, 128K context
- [[wiki/entities/stepfun]] — Chinese AI startup; Step-3.5-Flash 196B MoE, competitive with GPT-5.4 Turbo
- [[wiki/entities/langchain]] — Open-source framework; LangGraph (multi-agent) and LangSmith (eval)
- [[wiki/entities/37signals]] — Basecamp/Hey company (DHH); pragmatist AI adoption model
- [[wiki/entities/nous-research]] — Open-source AI org; Hermes fine-tuned model series
- [[wiki/entities/datalab]] — Built Chandra OCR 2; benchmark-topping document intelligence
- [[wiki/entities/exo-labs]] — Open-source distributed inference (Exo tool)
- [[wiki/entities/minimax]] — Model lab emphasizing low-cost agentic models and self-evolving harness narratives
- [[wiki/entities/amazon]] — Large-scale enterprise AI adoption case study; dark code and spec-driven governance pressure
- [[wiki/entities/apple]] — Apple Silicon as the hardware substrate for local-first AI workflows

### Models

- [[wiki/entities/claude-model-family]] — Anthropic's Haiku/Sonnet/Opus tiers; backbone of agentic coding ecosystem
- [[wiki/entities/gemma-4]] — Google DeepMind open model; tool-calling 6.6%→86.4%; 27B MoE multimodal
- [[wiki/entities/glm-5-1]] — ZhipuAI free API; 128K context; strong UI generation
- [[wiki/entities/step-3-5-flash]] — StepFun 196B MoE; competitive reasoning with GPT-5.4 Turbo
- [[wiki/entities/qwen3]] — Alibaba open model family; Qwen3-Next-80B ran on Exo at 70–80 tok/s

### Products

- [[wiki/entities/claude-code]] — Anthropic's autonomous agentic coding tool (terminal + VS Code)
- [[wiki/entities/openclaw]] — Open-source model-agnostic agentic coding alternative to Claude Code
- [[wiki/entities/paperclip]] — AI automation + governance platform built on Claude Code
- [[wiki/entities/ollama]] — One-command local model runner; OpenAI-compatible API
- [[wiki/entities/langgraph]] — LangChain's stateful graph multi-agent framework; most production-ready
- [[wiki/entities/obsidian]] — Markdown note-taking app; central to Karpathy's LLM wiki pattern
- [[wiki/entities/cursor]] — AI-native VS Code fork; used to build LLM wiki in 3 prompts
- [[wiki/entities/codex-cli]] — OpenAI's terminal agentic coding tool; Claude Code competitor
- [[wiki/entities/exo]] — Distributed inference across consumer devices; OpenAI-compatible API
- [[wiki/entities/vllm]] — High-throughput NVIDIA inference server; PagedAttention + continuous batching
- [[wiki/entities/llama-cpp]] — C++ inference engine for CPU/Apple Silicon; foundation of local AI
- [[wiki/entities/mcp]] — Anthropic's Model Context Protocol; open standard for AI tool connectivity
- [[wiki/entities/cline]] — Open-source VS Code extension for agentic coding; model-agnostic
- [[wiki/entities/mempalace]] — Local-first AI memory system using spatial organization and layered recall
- [[wiki/entities/polymarket]] — Prediction-market platform used as a clean AI arbitrage case study
- [[wiki/entities/amazon-kira]] — Amazon's internal coding tool pushed toward spec-driven workflows after failures

## Concepts

### Core Patterns (LLM Wiki Ecosystem)
- [[wiki/concepts/llm-wiki]] — The foundational pattern: LLM-maintained markdown wiki; no vector DB needed
- [[wiki/concepts/karpathy-loop]] — Keep/discard optimization loop; AI runs experiments autonomously until good
- [[wiki/concepts/autoresearch]] — Karpathy's ML code optimizer; generalized to universal skill.md by Balu Kosuri
- [[wiki/concepts/rag-vs-llm-wiki]] — Why LLM wiki outperforms RAG: accumulation vs. ephemeral retrieval
- [[wiki/concepts/claude-md]] — CLAUDE.md / AGENTS.md: standing instruction files loaded at every agent session
- [[wiki/concepts/skill-md]] — Task-specific expertise files; portable, evolvable agent capabilities
- [[wiki/concepts/soul-md]] — Persistent AI identity files; agent self-model that survives across sessions
- [[wiki/concepts/world-model]] — Company-scale knowledge system that must separate fact routing from judgment

### Agent Architecture
- [[wiki/concepts/agent-memory]] — Memory types, Anthropic vs. OpenAI philosophies, memory-as-substrate thesis
- [[wiki/concepts/context-portability]] — Moving AI context between tools; markdown as the portable format
- [[wiki/concepts/multi-agent-orchestration]] — Supervisor/worker, sequential, parallel, event-driven patterns
- [[wiki/concepts/advisor-executor-pattern]] — Dual-agent: Advisor plans, Executor implements; prevents sycophancy
- [[wiki/concepts/harness-engineering]] — Anthropic's term for structuring agent context windows systematically
- [[wiki/concepts/agentic-loop]] — The core LLM→tool→environment→repeat cycle
- [[wiki/concepts/tool-call-bottleneck]] — Wall-clock time dominated by tool calls, not inference; the real constraint
- [[wiki/concepts/agent-native-infrastructure]] — branchFS, persistent containers, shared KV cache: infra for agent speed
- [[wiki/concepts/outcome-agents]] — Evaluating agents by memory + artifact production + compounding context

### Business & Strategy
- [[wiki/concepts/intelligence-arbitrage]] — Routing tasks to optimal model: local for simple, API for complex
- [[wiki/concepts/local-hard-takeoff]] — Thesis: next capability leap comes from local/edge models, not cloud giants
- [[wiki/concepts/saas-disruption]] — AI agents eating the $285B SaaS middleware market
- [[wiki/concepts/agentic-saas]] — New software category built on agents: async jobs, outcome pricing, artifact delivery
- [[wiki/concepts/dark-code]] — AI-generated code nobody understands; compiles but can't be safely modified
- [[wiki/concepts/spec-driven-development]] — Write spec first, then delegate to agent; antidote to dark code
- [[wiki/concepts/vibe-coding]] — AI iteration without a plan; fine for prototypes, dangerous in production
- [[wiki/concepts/five-safe-places-to-build]] — Verifiable domains, hardware, relationships, eval, orchestration

### Technical Concepts
- [[wiki/concepts/mixture-of-experts]] — Sparse activation: only a fraction of params fire per token; 5x speed at same VRAM
- [[wiki/concepts/local-ai-inference]] — Running LLMs on local hardware; privacy, cost, offline use
- [[wiki/concepts/distributed-inference]] — Pooling multiple consumer devices into one AI cluster (Exo)
- [[wiki/concepts/markdown-first-architecture]] — Plain markdown as primary AI knowledge format; portable, git-versionable
- [[wiki/concepts/evolutionary-prompting]] — Applying keep/discard mutation loops to prompt optimization
- [[wiki/concepts/eval-driven-development]] — Define evaluation criteria first; binary yes/no most effective
- [[wiki/concepts/second-brain]] — Externalized personal knowledge system; AI-augmented with LLM wiki
- [[wiki/concepts/knowledge-accumulation]] — Each new source enriches existing structure; compound interest for knowledge
- [[wiki/concepts/vectorless-rag]] — RAG without embeddings: structured markdown + BM25 or plain index
- [[wiki/concepts/agentic-coding]] — LLMs executing full software development autonomously; Claude Code paradigm
- [[wiki/concepts/death-of-etl]] — AI agents replacing traditional Extract-Transform-Load pipelines
- [[wiki/concepts/ocr-disruption]] — Chandra OCR 2 invalidated commercial OCR; pattern for frontier AI obsoleting markets
- [[wiki/concepts/product-minded-engineering]] — Engineering with product/outcome thinking; critical in AI-native era
- [[wiki/concepts/personal-knowledge-management]] — PKM augmented by AI: "The hard part was always the bookkeeping"
- [[wiki/concepts/prediction-markets]] — Market-based information aggregation; AI-automated arbitrage
- [[wiki/concepts/context-window-management]] — Token efficiency: Caveman plugin, CLAUDE.md length, sliding windows
- [[wiki/concepts/cloud-native-architecture]] — Modular monolith to distributed systems progression; cloud-era architecture tradeoffs
- [[wiki/concepts/software-3-0]] — Natural-language control layer that composes code, models, and tools
- [[wiki/concepts/self-evolving-software]] — Harness and memory systems that improve themselves through evaluation and write-back

### Memory & Graph Dynamics
- [[wiki/concepts/memory-palace-architecture]] — Spatially organized agent memory using structured retrieval scopes
- [[wiki/concepts/aaak-dialect]] — Compact memory encoding format and its efficiency/accuracy tradeoff
- [[wiki/concepts/local-first-ai-memory]] — User-owned, on-device memory infrastructure pattern
- [[wiki/concepts/graph-percolation-threshold]] — Connectivity tipping point for graph memory usefulness

## Sources

### Karpathy / LLM Wiki Cluster
- [[wiki/sources/karpathy-10x-claude-code-llm-wiki]] — How Karpathy 10x'd his Claude Code workflow with LLM wiki (2026-04)
- [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]] — Balu Kosuri: 3-prompt implementation of Karpathy LLM wiki (2026-04)
- [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]] — evoailabs: theoretical deep-dive + ecosystem survey (2026-04)
- [[wiki/sources/karpathy-claude-md-file]] — What Karpathy's CLAUDE.md file does + Forrest Chang's 60-line distillation (2026-04)
- [[wiki/sources/karpathy-autoresearch-universal-skill]] — Balu Kosuri: autoresearch → universal prompt optimization skill (2026-04)
- [[wiki/sources/karpathy-fix-agents-markdown]] — Karpathy's single-markdown fix for sycophantic agents; readable guardrails over mega-prompts (2026-04)
- [[wiki/sources/300-dollars-auto-research-karpathy-loop]] — Nate B Jones: $300 hardware build + Karpathy Loop + SOUL.md (2026-04)
- [[wiki/sources/claude-code-karpathy-obsidian-new-meta]] — Meta discussion of Karpathy Obsidian pattern as new workflow (2026-04)
- [[wiki/sources/claude-code-karpathy-self-evolving-10x]] — WorldofAI: LLM wiki architecture + Claude Code integration for 10x code generation (2026-04)
- [[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]] — Cole Medin: context-portal self-evolving memory system (2026-04)
- [[wiki/sources/autoresearch-tutorial-david-ondrej]] — David Ondrej: beginner-friendly autoresearch walkthrough and three-file architecture (2026-03)
- [[wiki/sources/guide-to-karpathy-autoresearch]] — DataCamp: Karpathy's AutoResearch for ML experimentation; three-file architecture and ratchet loop (2026-03)

### Claude Code Ecosystem
- [[wiki/sources/building-claude-code-boris-cherny]] — Pragmatic Engineer: Boris Cherny on building Claude Code at Anthropic (2026-03)
- [[wiki/sources/anthropic-claude-managed-agents]] — Joe Njenga: Claude Managed Agents removes harness work; fully hosted agent runtime (2026-04)
- [[wiki/sources/claude-code-source-leaked-worth-learning]] — Analysis of leaked Claude Code source code (2026-04)
- [[wiki/sources/100-hours-claude-code-vs-antigravity]] — Nate Herk: 100-hour Claude Code review vs. alternatives (2026-04)
- [[wiki/sources/i-stopped-paying-claude-code]] — Rohan Mistry: 2-week OpenCode test; quality gap is 15–20%, you're paying for polish (2026-04)
- [[wiki/sources/master-claude-code-skills]] — Nate Herk: mastering skills, CLAUDE.md, and advanced workflows (2026-04)
- [[wiki/sources/claude-code-skills-got-better]] — How Claude Code skill.md files evolved (2026-04)
- [[wiki/sources/eight-claude-skills-meta-skills]] — Ben AI: reusable meta skills for planning, prompting, checking, and decision support (2026-04)
- [[wiki/sources/cut-claude-code-output-tokens-75-percent]] — Alex Dunlop: Caveman plugin cuts output tokens 75% (2026-04)
- [[wiki/sources/claude-session-limit-management]] — Nate Herk: context rot, rewind, handoff, and session-discipline playbook (2026-04)
- [[wiki/sources/codex-and-claude-side-by-side]] — OpenAI Codex CLI vs. Claude Code direct comparison (2026-04)
- [[wiki/sources/anthropic-harness-engineering-two-agent-architecture]] — Anthropic's two-agent harness engineering architecture (2026-04)
- [[wiki/sources/ditched-warp-free-zshrc]] — Alex Dunlop: switched from Warp to free .zshrc setup (2026-04)

### Agent Frameworks & Patterns
- [[wiki/sources/comparing-6-python-ai-agent-frameworks]] — LangGraph vs. CrewAI vs. OpenAI Agents SDK vs. PydanticAI vs. AutoGen vs. Smolagents (2026-04)
- [[wiki/sources/agents-are-autonomous-except-when-not]] — Reality check: most deployed agents are semi-autonomous; human-in-the-loop is the realistic default (2026-04)
- [[wiki/sources/multi-agent-architecture-patterns]] — Deep dive on multi-agent patterns: sequential, parallel, hierarchical (2026-04)
- [[wiki/sources/langchain-deep-agents]] — LangChain deep agent implementation patterns (2026-04)
- [[wiki/sources/how-to-build-claude-agent-teams]] — Nate Herk: building agent teams with Claude Code (2026-04)
- [[wiki/sources/agentic-saas-playbook-2026]] — Playbook for building SaaS products on top of AI agents (2026-04)
- [[wiki/sources/claude-advisor-strategy-stop-using-opus]] — Why to use Claude as advisor, not just executor (2026-04)
- [[wiki/sources/claude-as-dungeon-master]] — Claude orchestrating complex multi-character/task scenarios (2026-04)
- [[wiki/sources/building-ai-agent-scratch-pure-python]] — Building an AI agent from scratch in pure Python (2026-04)
- [[wiki/sources/hermes-agent-vs-openclaw]] — Nous Research Hermes agent compared to OpenClaw (2026-04)
- [[wiki/sources/paperclip-ai-agents-company]] — Nikhil: Paperclip open-source orchestration platform; agents as organization with roles, budgets, heartbeats (2026-04)

### OpenClaw / Local AI
- [[wiki/sources/networkchuck-openclaw-right-now-review]] — NetworkChuck: OpenClaw setup and review (2026-04)
- [[wiki/sources/openclaw-gemma4-free-private-ai]] — Running OpenClaw with Gemma 4 for private, free AI (2026-04)
- [[wiki/sources/openclaw-10000-to-trade-stocks]] — Nate Herk: $10K stock trading with OpenClaw (2026-04)
- [[wiki/sources/ollama-claude-code-free]] — Nate Herk: Ollama as free alternative to Claude API (2026-04)
- [[wiki/sources/claude-code-paperclip-destroyed-openclaw]] — Paperclip vs. OpenClaw capability comparison (2026-04)
- [[wiki/sources/ollm-python-library-llms-consumer-hardware]] — oLLM Python library for running LLMs on consumer hardware (2026-04)

### Model Benchmarks & Local Inference
- [[wiki/sources/gemma-4-vllm-vs-ollama-blackwell-benchmarks]] — Gemma 4 on NVIDIA Blackwell: vLLM vs Ollama benchmarks (2026-04)
- [[wiki/sources/gemma-4-e4b-vs-qwen-3-5-4b-comparison]] — Gemma 4 4B vs Qwen3.5 4B head-to-head (2026-04)
- [[wiki/sources/gemma-4-open-source-ai-drop]] — Alex Dunlop: Gemma 4 open-source AI drop overview (2026-04)
- [[wiki/sources/gemma-4-local-model-codex-cli]] — Daniel Vaughan: Gemma 4 in Codex CLI; quality > speed for agentic coding (2026-04)
- [[wiki/sources/turboquant-moe-122b-macbook-apple-silicon]] — TurboQuant MoE compression for 120B+ local inference on Apple Silicon (2026-04)
- [[wiki/sources/glm-5-1-beats-gpt-5-4-claude-opus]] — GLM 5.1 benchmark vs. GPT-5.4 and Claude Opus (2026-04)
- [[wiki/sources/glm-5-1-free-claude-subscription-replacement]] — Danish Sofi: GLM 5.1 replaced $100/month Claude subscription (2026-04)
- [[wiki/sources/step-3-5-flash-196b-open-source-model]] — StepFun Step-3.5-Flash 196B MoE model release (2026-04)
- [[wiki/sources/best-llms-opencode-qwen-gemma-tested-locally]] — Best LLMs for OpenCode: Qwen and Gemma tested locally (2026-04)
- [[wiki/sources/two-macs-80b-ai-cluster-exo]] — Manjunath Janardhan: two-Mac 80B cluster with Exo (2026-03)
- [[wiki/sources/outperforming-claude-code-codex]] — Techniques for outperforming cloud agents with local inference; quantization and context tuning (2026-04)
- [[wiki/sources/doubled-local-llm-speed]] — Amar Chetri: doubling local LLM speed without hardware upgrades; optimization techniques (2026-02)
- [[wiki/sources/1-bit-llm-1gb]] — Chew Loong Nian: extreme 1-bit quantization compresses 8.2B params to 1.15 GB with surprising performance (2026-04)
- [[wiki/sources/local-model-ollama-guide]] — Gemini conversation: Ollama + Qwen + Claude Code integration; LiteLLM proxy and local-first agentic CLI comparison (2026-04)

### Strategy & Industry Analysis (Nate B Jones)
- [[wiki/sources/anthropic-openai-memory-context-portability]] — Anthropic vs. OpenAI memory architecture philosophies (2026-04)
- [[wiki/sources/real-problem-ai-agents-clarity-of-intent]] — The real problem with AI agents: clarity of intent, not capability (2026-04)
- [[wiki/sources/five-safe-places-to-build-in-ai]] — 5 business categories resistant to AI disruption (2026-04)
- [[wiki/sources/wall-street-285b-ai-agents-review]] — Wall Street's $285B SaaS sell-off was correct; agents are coming (2026-04)
- [[wiki/sources/amazon-fired-engineers-ai-dark-code]] — Amazon engineering layoffs + dark code + spec-driven mandate (2026-04)
- [[wiki/sources/ai-50x-faster-getting-2x-wrong-thing]] — Why you get 2x gains despite 50x AI speed: tool-call bottleneck (2026-04)
- [[wiki/sources/ai-21-5-trillion-into-dust]] — Mandar Karhade: wealth transfer mechanism; labor share 53.8% (lowest ever), top 1% owns 50% stock (2026-04)
- [[wiki/sources/karpathy-llm-wiki-pattern-rag]] — LLM wiki pattern killing the need for RAG (2026-04)
- [[wiki/sources/world-model-interpretive-boundary]] — Nate B Jones: world-model architectures fail when they hide judgment inside retrieval (2026-04)
- [[wiki/sources/mo-gawdat-next-ai-phase-positioning]] — Mo Gawdat on agility, ethics, and labor disruption ahead of the next AI phase (2026-03)

### Engineering Practice
- [[wiki/sources/from-ides-to-ai-agents-steve-yegge]] — Steve Yegge: IDEs are dying, agents are replacing them (2026-04)
- [[wiki/sources/dhh-new-way-writing-code-agent-first]] — DHH on the new way of writing code with AI agents (2026-04)
- [[wiki/sources/cli-vs-mcp-agents]] — Phil: Peter Steinberger's MCP critique; CLIs beat MCP for agent tool design; context efficiency wins (2026-02)
- [[wiki/sources/product-minded-engineers-ai-native]] — Pragmatic Engineer: product-minded engineering in the AI era (2026-04)
- [[wiki/sources/coder-to-architect-developer-role-2026]] — Broad career framing on the shift from implementation to architecture and AI oversight (2025-11)
- [[wiki/sources/evolving-software-architecture-cloud-era]] — Cloud-era architecture tradeoffs: modular monoliths, distribution, and resilience (2025-10)
- [[wiki/sources/software-stack-1-0-2-0-3-0]] — Jared Hatfield on how code, models, and language-directed agents compose (2026-04)
- [[wiki/sources/uber-agentic-engineering-shift]] — Uber's agentic engineering shift case study (2026-04)
- [[wiki/sources/stop-vibe-coding-4-file-system]] — Stop vibe coding: 4-file system (spec/plan/changelog/.cursorrules) (2026-04)
- [[wiki/sources/polymarket-bot-438k-ai-arbitrage]] — Nate Herk: $438K Polymarket bot built with AI (2026-04)
- [[wiki/sources/chip-huyen-building-when-nothing-left-to-build]] — Chip Huyen at AI Summit: evaluation and production ML (2026-04)
- [[wiki/sources/five-agent-skills-mega-prompt]] — Technical analysis: mega-prompts are anti-patterns; agents need modular skills over monolithic prompts (2026-04)

### Self-Evolving Systems
- [[wiki/sources/minimax-m2-7-self-evolving-agent-model]] — Developers Digest on MiniMax M2.7's self-evolving harness and cheap agentic usage (2026-03)
- [[wiki/sources/self-evolving-ai-open-weight]] — Prompt Engineering on MiniMax self-improvement loops and harness quality (2026-03)
- [[wiki/sources/self-evolving-software-code-improves-itself]] — Broad essay on continuous self-improvement in software systems (2026-03)
- [[wiki/sources/self-evolving-agent-architectures-explained]] — AI Jason on Claude Code, OpenClaw, Hermes, and memory-vs-harness evolution (2026-04)

### Knowledge & Data Architecture
- [[wiki/sources/markdown-file-beats-vector-database]] — The markdown file that beat a $50M vector database (2026-04)
- [[wiki/sources/japanese-firm-markdown-employee]] — Japanese firm's employee markdown wiki outperformed vector stores (2026-04)
- [[wiki/sources/vectorless-rag-reasoning-based-retrieval]] — RAG without vectors: reasoning-based retrieval patterns (2026-04)
- [[wiki/sources/death-of-traditional-etl-ai-agents]] — AI agents replacing traditional ETL pipelines (2026-04)
- [[wiki/sources/chandra-ocr-2-benchmark]] — Datalab Chandra OCR 2: benchmark that killed commercial OCR (2026-04)
- [[wiki/sources/temptation-of-nearly-knowing]] — The epistemic danger of LLMs appearing to know more than they do (2026-04)
- [[wiki/sources/phase-transition-knowledge-graph-agent-memory]] — Network-science view of GraphRAG phase transitions and connectivity thresholds (2026-04)

### MemPalace / AI Memory Cluster
- [[wiki/sources/mempalace-give-your-ai-a-real-memory]] — Introductory local-first memory framing and setup (2026-04)
- [[wiki/sources/giving-your-ai-a-memory-introduction-mempalace]] — Technical walkthrough of MemPalace architecture and MCP usage (2026-04)
- [[wiki/sources/mempalace-96-6-recall-zero-api-calls]] — Strong-form argument for raw-text-first memory retrieval (2026-04)
- [[wiki/sources/mempalace-benchmarks-what-they-mean]] — Critical analysis of MemPalace benchmark interpretation and tradeoffs (2026-04)
- [[wiki/sources/mempalace-viral-22k-stars-honest-setup]] — Practical setup-focused review with maturity caveats (2026-04)
- [[wiki/sources/from-hollywood-to-github-milla-jovovich-mempalace]] — Origin narrative and architecture summary (2026-04)
- [[wiki/sources/rise-of-memory-palaces-mempalace-disruption]] — Market-position framing vs managed memory platforms (2026-04)
- [[wiki/sources/death-of-ephemeral-context-aaak-dialect]] — AAAK-focused architectural teardown and future directions (2026-04)
- [[wiki/sources/resident-eval-mempalace-first-glimpse]] — Early systems-level review of MemPalace memory model (2026-04)
- [[wiki/sources/ayona-openclaw-vs-mempalace-benchmark]] — BM25 vs MemPalace benchmark comparison on LongMemEval (2026-04)

### Vercel & UI Generation
- [[wiki/sources/vercel-v0-d0-agent-lessons]] — Malte Ubl: lessons from building v0 and d0 at Vercel (2026-04)

### Miscellaneous
- [[wiki/sources/website-flipping-side-hustle]] — Gigi Creates: website flipping side hustle ($30K/year, no-code) (2026-04)
- [[wiki/sources/paperclip-ai-governance-platform]] — Paperclip platform for AI governance and automation (2026-04)

## Analyses

- [[wiki/analyses/transformative-insights-2026]] — Five core insights reshaping AI: tool-call bottleneck, local model viability, LLM wiki knowledge compounding, SaaS disruption, intelligence arbitrage (2026-04)
- [[wiki/analyses/raw-dedup-candidates-2026-04-20]] — Tagged duplicate raw clips and mapped canonical source pages (2026-04)
- [[wiki/analyses/mempalace-agentic-systems-research-2026-04-21]] — Research synthesis of MemPalace for LLM agentic systems: applications, benefits, risks, and scalable implementation guidance (2026-04)
- [[wiki/analyses/karpathy-loop-for-codebases-research-2026-04-21]] — Research synthesis on applying the Karpathy Loop to codebases, including fit criteria, benefits, risks, and a recommended MVP for this repository (2026-04)
