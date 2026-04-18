---
title: "AI Wiki Log"
type: log
domain: ai
created: 2026-04-18
updated: 2026-04-18
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

## [2026-04-28] ingest | Bulk Ingest — 64 Raw Sources

Processed all 64 web-clipped sources from `raw/` in a single bulk ingest operation. Created 153 new wiki pages across sources, entities, and concepts. Updated index.md and overview.md.

**Source pages created (64)**: All sources from `wiki/sources/` — see [[wiki/index]] for full list organized by cluster.

**Entity pages created (49)**:
- People (19): [[wiki/entities/andrej-karpathy]], [[wiki/entities/boris-cherny]], [[wiki/entities/nate-b-jones]], [[wiki/entities/nate-herk]], [[wiki/entities/chip-huyen]], [[wiki/entities/steve-yegge]], [[wiki/entities/dhh]], [[wiki/entities/gergely-orosz]], [[wiki/entities/cole-medin]], [[wiki/entities/balu-kosuri]], [[wiki/entities/forrest-chang]], [[wiki/entities/networkchuck]], [[wiki/entities/malte-ubl]], [[wiki/entities/alex-dunlop]], [[wiki/entities/tobi-lutke]], [[wiki/entities/manjunath-janardhan]], [[wiki/entities/daniel-vaughan]], [[wiki/entities/nick-saraev]], [[wiki/entities/danish-sofi]]
- Organizations (12): [[wiki/entities/anthropic]], [[wiki/entities/openai]], [[wiki/entities/google-deepmind]], [[wiki/entities/vercel]], [[wiki/entities/uber]], [[wiki/entities/zhipuai]], [[wiki/entities/stepfun]], [[wiki/entities/langchain]], [[wiki/entities/37signals]], [[wiki/entities/nous-research]], [[wiki/entities/datalab]], [[wiki/entities/exo-labs]]
- Models (5): [[wiki/entities/claude-model-family]], [[wiki/entities/gemma-4]], [[wiki/entities/glm-5-1]], [[wiki/entities/step-3-5-flash]], [[wiki/entities/qwen3]]
- Products (13): [[wiki/entities/claude-code]], [[wiki/entities/openclaw]], [[wiki/entities/paperclip]], [[wiki/entities/ollama]], [[wiki/entities/langgraph]], [[wiki/entities/obsidian]], [[wiki/entities/cursor]], [[wiki/entities/codex-cli]], [[wiki/entities/exo]], [[wiki/entities/vllm]], [[wiki/entities/llama-cpp]], [[wiki/entities/mcp]], [[wiki/entities/cline]]

**Concept pages created (40)**: [[wiki/concepts/llm-wiki]], [[wiki/concepts/karpathy-loop]], [[wiki/concepts/autoresearch]], [[wiki/concepts/rag-vs-llm-wiki]], [[wiki/concepts/claude-md]], [[wiki/concepts/skill-md]], [[wiki/concepts/soul-md]], [[wiki/concepts/agent-memory]], [[wiki/concepts/context-portability]], [[wiki/concepts/multi-agent-orchestration]], [[wiki/concepts/advisor-executor-pattern]], [[wiki/concepts/harness-engineering]], [[wiki/concepts/agentic-loop]], [[wiki/concepts/tool-call-bottleneck]], [[wiki/concepts/agent-native-infrastructure]], [[wiki/concepts/outcome-agents]], [[wiki/concepts/intelligence-arbitrage]], [[wiki/concepts/local-hard-takeoff]], [[wiki/concepts/saas-disruption]], [[wiki/concepts/agentic-saas]], [[wiki/concepts/dark-code]], [[wiki/concepts/spec-driven-development]], [[wiki/concepts/vibe-coding]], [[wiki/concepts/five-safe-places-to-build]], [[wiki/concepts/mixture-of-experts]], [[wiki/concepts/local-ai-inference]], [[wiki/concepts/distributed-inference]], [[wiki/concepts/markdown-first-architecture]], [[wiki/concepts/evolutionary-prompting]], [[wiki/concepts/eval-driven-development]], [[wiki/concepts/second-brain]], [[wiki/concepts/knowledge-accumulation]], [[wiki/concepts/vectorless-rag]], [[wiki/concepts/agentic-coding]], [[wiki/concepts/death-of-etl]], [[wiki/concepts/ocr-disruption]], [[wiki/concepts/product-minded-engineering]], [[wiki/concepts/personal-knowledge-management]], [[wiki/concepts/prediction-markets]], [[wiki/concepts/context-window-management]]

**Meta pages updated**: [[wiki/index]], [[wiki/overview]], [[wiki/log]]

---

Created all entity pages for the AI domain wiki in a single batch operation. Entities cover the major people, organizations, models, and products documented across the source corpus.

**People created (19)**:
[[wiki/entities/andrej-karpathy]], [[wiki/entities/boris-cherny]], [[wiki/entities/nate-b-jones]], [[wiki/entities/nate-herk]], [[wiki/entities/chip-huyen]], [[wiki/entities/steve-yegge]], [[wiki/entities/dhh]], [[wiki/entities/gergely-orosz]], [[wiki/entities/cole-medin]], [[wiki/entities/balu-kosuri]], [[wiki/entities/forrest-chang]], [[wiki/entities/networkchuck]], [[wiki/entities/malte-ubl]], [[wiki/entities/alex-dunlop]], [[wiki/entities/tobi-lutke]], [[wiki/entities/manjunath-janardhan]], [[wiki/entities/daniel-vaughan]], [[wiki/entities/nick-saraev]], [[wiki/entities/danish-sofi]]

**Organizations created (12)**:
[[wiki/entities/anthropic]], [[wiki/entities/openai]], [[wiki/entities/google-deepmind]], [[wiki/entities/vercel]], [[wiki/entities/uber]], [[wiki/entities/zhipuai]], [[wiki/entities/stepfun]], [[wiki/entities/langchain]], [[wiki/entities/37signals]], [[wiki/entities/nous-research]], [[wiki/entities/datalab]], [[wiki/entities/exo-labs]]

**Models created (5)**:
[[wiki/entities/claude-model-family]], [[wiki/entities/gemma-4]], [[wiki/entities/glm-5-1]], [[wiki/entities/step-3-5-flash]], [[wiki/entities/qwen3]]

**Products created (13)**:
[[wiki/entities/claude-code]], [[wiki/entities/openclaw]], [[wiki/entities/paperclip]], [[wiki/entities/ollama]], [[wiki/entities/langgraph]], [[wiki/entities/obsidian]], [[wiki/entities/cursor]], [[wiki/entities/codex-cli]], [[wiki/entities/exo]], [[wiki/entities/vllm]], [[wiki/entities/llama-cpp]], [[wiki/entities/mcp]], [[wiki/entities/cline]]

Updated: [[wiki/index]]
