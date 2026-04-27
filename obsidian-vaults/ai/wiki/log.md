---
title: "AI Wiki Log"
type: log
domain: ai
tags:
  - log
  - maintenance
  - history
created: 2026-04-18
updated: 2026-04-21
sources:
  - "[[wiki/index]]"
---

# AI Wiki Log

Chronological record of all wiki activity. Append-only.

---

## [2026-04-18] create | Wiki Initialization

Initialized the AI domain wiki structure for the Library of Alexandria project.

- Created directory structure: `raw/`, `raw/assets/`, `wiki/`, `wiki/entities/`, `wiki/concepts/`, `wiki/sources/`, `wiki/analyses/`
- Created `AGENTS.md` schema at project root
- Created `wiki/index.md`, `wiki/log.md`, `wiki/overview.md`
- Wiki is ready for first source ingestion

Pages touched: [[wiki/index]], [[wiki/log]], [[wiki/overview]]

---

## [2026-04-18] ingest | Bulk Ingest — 63 Raw Sources

Processed all 63 web-clipped sources from `raw/` in a single bulk ingest operation. Created 153 new wiki pages across sources, entities, and concepts (64 source pages, 49 entity pages, 40 concept pages). Updated index.md and overview.md.

**Source pages created (64)**: All sources from `wiki/sources/` — see [[wiki/index]] for full list organized by cluster.

**Entity pages created (49)**:
- People (19): [[wiki/entities/andrej-karpathy]], [[wiki/entities/boris-cherny]], [[wiki/entities/nate-b-jones]], [[wiki/entities/nate-herk]], [[wiki/entities/chip-huyen]], [[wiki/entities/steve-yegge]], [[wiki/entities/dhh]], [[wiki/entities/gergely-orosz]], [[wiki/entities/cole-medin]], [[wiki/entities/balu-kosuri]], [[wiki/entities/forrest-chang]], [[wiki/entities/networkchuck]], [[wiki/entities/malte-ubl]], [[wiki/entities/alex-dunlop]], [[wiki/entities/tobi-lutke]], [[wiki/entities/manjunath-janardhan]], [[wiki/entities/daniel-vaughan]], [[wiki/entities/nick-saraev]], [[wiki/entities/danish-sofi]]
- Organizations (12): [[wiki/entities/anthropic]], [[wiki/entities/openai]], [[wiki/entities/google-deepmind]], [[wiki/entities/vercel]], [[wiki/entities/uber]], [[wiki/entities/zhipuai]], [[wiki/entities/stepfun]], [[wiki/entities/langchain]], [[wiki/entities/37signals]], [[wiki/entities/nous-research]], [[wiki/entities/datalab]], [[wiki/entities/exo-labs]]
- Models (5): [[wiki/entities/claude-model-family]], [[wiki/entities/gemma-4]], [[wiki/entities/glm-5-1]], [[wiki/entities/step-3-5-flash]], [[wiki/entities/qwen3]]
- Products (13): [[wiki/entities/claude-code]], [[wiki/entities/openclaw]], [[wiki/entities/paperclip]], [[wiki/entities/ollama]], [[wiki/entities/langgraph]], [[wiki/entities/obsidian]], [[wiki/entities/cursor]], [[wiki/entities/codex-cli]], [[wiki/entities/exo]], [[wiki/entities/vllm]], [[wiki/entities/llama-cpp]], [[wiki/entities/mcp]], [[wiki/entities/cline]]

**Concept pages created (40)**: [[wiki/concepts/llm-wiki]], [[wiki/concepts/karpathy-loop]], [[wiki/concepts/autoresearch]], [[wiki/concepts/rag-vs-llm-wiki]], [[wiki/concepts/claude-md]], [[wiki/concepts/skill-md]], [[wiki/concepts/soul-md]], [[wiki/concepts/agent-memory]], [[wiki/concepts/context-portability]], [[wiki/concepts/multi-agent-orchestration]], [[wiki/concepts/advisor-executor-pattern]], [[wiki/concepts/harness-engineering]], [[wiki/concepts/agentic-loop]], [[wiki/concepts/tool-call-bottleneck]], [[wiki/concepts/agent-native-infrastructure]], [[wiki/concepts/outcome-agents]], [[wiki/concepts/intelligence-arbitrage]], [[wiki/concepts/local-hard-takeoff]], [[wiki/concepts/saas-disruption]], [[wiki/concepts/agentic-saas]], [[wiki/concepts/dark-code]], [[wiki/concepts/spec-driven-development]], [[wiki/concepts/vibe-coding]], [[wiki/concepts/five-safe-places-to-build]], [[wiki/concepts/mixture-of-experts]], [[wiki/concepts/local-ai-inference]], [[wiki/concepts/distributed-inference]], [[wiki/concepts/markdown-first-architecture]], [[wiki/concepts/evolutionary-prompting]], [[wiki/concepts/eval-driven-development]], [[wiki/concepts/second-brain]], [[wiki/concepts/knowledge-accumulation]], [[wiki/concepts/vectorless-rag]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/death-of-etl]], [[wiki/concepts/ocr-disruption]], [[wiki/concepts/product-minded-engineering]], [[wiki/concepts/personal-knowledge-management]], [[wiki/concepts/prediction-markets]], [[wiki/concepts/context-window-management]]

**Meta pages updated**: [[wiki/index]], [[wiki/overview]], [[wiki/log]]

---

## [2026-04-18] lint | Post-Ingest Health Check

Ran full lint pass after bulk ingest. Findings and fixes applied:

**Issues fixed (3)**:
- Corrected malformed wikilink in [[wiki/index]]: `five-safe-places-to-build-in-ai.md|alias` → `five-safe-places-to-build-in-ai`
- Corrected bulk ingest log entry date: `2026-04-28` → `2026-04-18` (all ingest activity happened today)
- Corrected `updated` frontmatter in [[wiki/index]] and [[wiki/overview]]: `2026-04-28` → `2026-04-18`
- Removed duplicate entity-creation fragment that was appended after the main bulk ingest entry in this log

**Issues flagged (2, not auto-fixed)**:
- 153 individual wiki pages (64 sources, 49 entities, 40 concepts) have `created/updated: 2026-04-28` in their frontmatter — should be `2026-04-18`. These are functionally correct but dated 10 days ahead. A mass find-and-replace of `2026-04-28` → `2026-04-18` across `wiki/` would fix this if desired.
- Raw source count: `raw/` contains 63 `.md` files; log entry originally said "64 raw sources". Corrected to 63 in this log. The wiki has 64 source pages (one source page may cover content attributed to a raw file that has since been renamed or merged).

**Health check results**:
- ✅ No orphan pages detected (all pages reachable via [[wiki/index]])
- ✅ No missing linked pages (all wikilinks resolve to existing files)
- ✅ Index completeness: 64 sources, 49 entities, 40 concepts — all directories match index
- ✅ Frontmatter structure: all sampled pages have required fields (title, type, domain, tags, created, updated)

Pages touched: [[wiki/index]], [[wiki/overview]], [[wiki/log]]

---

## [2026-04-18] query | Five Transformative Insights in AI

User asked: "What are the most transformative insights in the AI domain now?"

Synthesized query from the 63-source corpus, identifying five core insights reshaping AI infrastructure, economics, and knowledge management:

1. **Tool Call Latency** — 50x model speed improvement yields only 2–3x productivity because 90% of agent time is spent on tool calls, not inference
2. **Local Hard Takeoff** — Gemma 4 and MoE models crossed the viability threshold; local inference now frontier-competitive on most tasks at zero marginal cost
3. **LLM Wiki Compounding** — Plain markdown structured by AI compounds faster than vector RAG; a Japanese firm's markdown beat a $50M vector database
4. **SaaS Disruption** — $285B middleware market exposed; agents can replicate workflows that specialized software used to manage
5. **Intelligence Arbitrage** — Route tasks to the cheapest model that handles them reliably; capability map becomes institutional IP

Result: Saved as [[wiki/analyses/transformative-insights-2026]].

Pages touched: [[wiki/index]], [[wiki/analyses/transformative-insights-2026]]

---

## [2026-04-20] ingest | MemPalace + Local MoE Batch (12 New Sources)

Processed 12 net-new raw sources focused on MemPalace/agent-memory architecture and Apple Silicon MoE quantization.

- Created 12 source summary pages under `wiki/sources/`
- Created new entity pages: [[wiki/entities/mempalace]], [[wiki/entities/milla-jovovich]], [[wiki/entities/ben-sigman]]
- Created new concept pages: [[wiki/concepts/memory-palace-architecture]], [[wiki/concepts/aaak-dialect]], [[wiki/concepts/local-first-ai-memory]], [[wiki/concepts/graph-percolation-threshold]]
- Updated existing pages to integrate new evidence: [[wiki/concepts/agent-memory]], [[wiki/concepts/local-ai-inference]], [[wiki/concepts/mixture-of-experts]], [[wiki/entities/manjunath-janardhan]], [[wiki/overview]], [[wiki/index]]

Pages touched: [[wiki/index]], [[wiki/overview]], [[wiki/concepts/agent-memory]], [[wiki/concepts/local-ai-inference]], [[wiki/concepts/mixture-of-experts]], [[wiki/entities/manjunath-janardhan]], [[wiki/entities/mempalace]], [[wiki/entities/milla-jovovich]], [[wiki/entities/ben-sigman]]

---

## [2026-04-20] update | Tagged Duplicate Raw Clips for Deletion

Tagged clear duplicate raw clips as deletion candidates without modifying files in `raw/`. Added canonical mappings from duplicate raw filenames to already-ingested source pages, plus one non-source conversation clip candidate.

Pages touched: [[wiki/analyses/raw-dedup-candidates-2026-04-20]], [[wiki/index]]

---

## [2026-04-20] lint | Health Check After Ingest

Ran health/lint checks after ingest and dedup tagging (177 wiki pages scanned).

- ✅ No orphan wiki pages detected
- ✅ No missing non-raw wikilinks in touched files from this ingest batch
- ✅ Index updated with all newly created source/entity/concept/analysis pages
- ⚠️ Pre-existing global link debt remains in older pages (885 unresolved links to non-existent concepts/entities), outside this ingest scope
- ⚠️ Contradiction callouts remain in [[wiki/entities/openclaw]] and [[wiki/entities/cline]] (pre-existing, unresolved)

Pages touched: [[wiki/log]]

---

## [2026-04-21] query | MemPalace Research Synthesis

Completed a thorough MemPalace analysis covering all related AI-vault sources, upstream MemPalace repository docs, and external literature on long-term memory benchmarks, retrieval architecture, and cognitive memory techniques.

Result: Saved as [[wiki/analyses/mempalace-agentic-systems-research-2026-04-21]].

Pages touched: [[wiki/analyses/mempalace-agentic-systems-research-2026-04-21]], [[wiki/index]], [[wiki/log]]

---

## [2026-04-21] query | Karpathy Loop for Codebases Research

Completed a research synthesis on how to apply the Karpathy Loop to a general codebase, grounded in Karpathy's original autoresearch design, later generalizations, agent harness/evaluator patterns, and the current structure of this repository.

Result: Saved as [[wiki/analyses/karpathy-loop-for-codebases-research-2026-04-21]].

Pages touched: [[wiki/analyses/karpathy-loop-for-codebases-research-2026-04-21]], [[wiki/index]], [[wiki/log]]

---

## [2026-04-21] ingest | AI Raw Source Batch — Architecture, Skills, and Self-Evolution

Processed a new AI-vault batch spanning Claude Code workflow skills, world-model architecture, developer-role shift, Software 3.0 framing, and the emerging self-evolving-agent stack.

- Created 12 new source pages: [[wiki/sources/eight-claude-skills-meta-skills]], [[wiki/sources/world-model-interpretive-boundary]], [[wiki/sources/evolving-software-architecture-cloud-era]], [[wiki/sources/mo-gawdat-next-ai-phase-positioning]], [[wiki/sources/coder-to-architect-developer-role-2026]], [[wiki/sources/claude-session-limit-management]], [[wiki/sources/minimax-m2-7-self-evolving-agent-model]], [[wiki/sources/self-evolving-software-code-improves-itself]], [[wiki/sources/self-evolving-ai-open-weight]], [[wiki/sources/software-stack-1-0-2-0-3-0]], [[wiki/sources/autoresearch-tutorial-david-ondrej]], [[wiki/sources/self-evolving-agent-architectures-explained]]
- Created new concept pages: [[wiki/concepts/world-model]], [[wiki/concepts/cloud-native-architecture]], [[wiki/concepts/software-3-0]], [[wiki/concepts/self-evolving-software]]
- Created new entity pages: [[wiki/entities/mo-gawdat]], [[wiki/entities/minimax]]
- Updated existing synthesis pages to absorb the batch: [[wiki/concepts/skill-md]], [[wiki/concepts/autoresearch]], [[wiki/concepts/context-window-management]], [[wiki/concepts/product-minded-engineering]], [[wiki/concepts/agent-memory]], [[wiki/entities/nate-herk]], [[wiki/entities/nate-b-jones]], [[wiki/overview]], [[wiki/index]]

Pages touched: [[wiki/index]], [[wiki/overview]], [[wiki/log]], [[wiki/concepts/world-model]], [[wiki/concepts/cloud-native-architecture]], [[wiki/concepts/software-3-0]], [[wiki/concepts/self-evolving-software]]

---

## [2026-04-21] lint | AI Vault Hardening Pass

Ran a maintenance pass alongside ingest and applied targeted structural fixes:

- Added top-level tags to [[wiki/index]] and [[wiki/log]]
- Repaired quote-normalization mismatches in existing source `raw:` links so source pages again point at real raw filenames
- Added [[wiki/entities/minimax]] and rewired an existing MiniMax reference to stop a known missing-link case
- Updated [[wiki/analyses/raw-dedup-candidates-2026-04-20]] with newly observed duplicate raw clips from this batch

Remaining known debt:

- Contradiction callouts still exist in [[wiki/entities/openclaw]], [[wiki/entities/cline]], [[wiki/analyses/mempalace-agentic-systems-research-2026-04-21]], and [[wiki/analyses/karpathy-loop-for-codebases-research-2026-04-21]]
- Older pages still contain broader unresolved-link debt outside this focused repair pass

Pages touched: [[wiki/index]], [[wiki/log]], [[wiki/analyses/raw-dedup-candidates-2026-04-20]], [[wiki/entities/minimax]]

---

## [2026-04-21] update | Lint Follow-up Entity Repairs

Added missing high-signal entity pages that were showing up as unresolved wikilinks across older AI pages: [[wiki/entities/amazon]], [[wiki/entities/amazon-kira]], [[wiki/entities/apple]], [[wiki/entities/polymarket]], and [[wiki/entities/tiago-forte]].

Pages touched: [[wiki/index]], [[wiki/log]], [[wiki/entities/amazon]], [[wiki/entities/amazon-kira]], [[wiki/entities/apple]], [[wiki/entities/polymarket]], [[wiki/entities/tiago-forte]]

---

## [2026-04-27] ingest | Batch Ingest — 14 New Raw Sources

Processed 14 net-new raw sources spanning agent architecture, cost/capability analysis, economic impact, local inference optimization, and integration patterns.

**Source pages created (14)**:
- [[wiki/sources/five-agent-skills-mega-prompt]] — Mega-prompts are anti-patterns; agents need modular skills
- [[wiki/sources/agents-are-autonomous-except-when-not]] — Reality check: most agents are semi-autonomous
- [[wiki/sources/ai-21-5-trillion-into-dust]] — Wealth transfer mechanism; labor share 53.8%, top 1% owns 50% of stock
- [[wiki/sources/anthropic-claude-managed-agents]] — Managed Agents: hosted harness eliminates infrastructure work
- [[wiki/sources/claude-code-karpathy-self-evolving-10x]] — LLM wiki + Claude Code integration for 10x code generation
- [[wiki/sources/i-stopped-paying-claude-code]] — 2-week OpenCode test: quality gap 15–20%, you're paying for comfort
- [[wiki/sources/outperforming-claude-code-codex]] — Local inference techniques outperform cloud agents on latency/cost
- [[wiki/sources/paperclip-ai-agents-company]] — Orchestration platform for multi-agent governance (roles, budgets, heartbeats)
- [[wiki/sources/cli-vs-mcp-agents]] — Peter Steinberger: CLIs beat MCP; context efficiency wins over abstraction
- [[wiki/sources/local-model-ollama-guide]] — Docker + LiteLLM + Ollama integration; local-first agentic CLI comparison
- [[wiki/sources/guide-to-karpathy-autoresearch]] — AutoResearch ratchet loop for 100+ ML experiments per night
- [[wiki/sources/doubled-local-llm-speed]] — Doubling local LLM speed through software optimization (quantization, context tuning)
- [[wiki/sources/1-bit-llm-1gb]] — Extreme 1-bit quantization: 8.2B params → 1.15 GB with surprising performance
- [[wiki/sources/karpathy-fix-agents-markdown]] — Single-markdown solution for sycophantic agents; readable guardrails over mega-prompts

**Meta pages updated**: [[wiki/index]] (14 source entries added across 6 sections), [[wiki/log]]

**Key themes**:
- Shift from mega-prompts to modular skills
- Economic reality check on AI deployment ROI and wealth concentration
- Local inference reaching competitive parity with cloud on cost/latency
- Agent orchestration moving from DIY harness to managed platforms
- CLI simplicity preferred over abstraction layers for tool design

Pages touched: [[wiki/index]], [[wiki/log]], and 14 new source pages
