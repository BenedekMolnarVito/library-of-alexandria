---
title: "Ayona (OpenClaw) vs Milla (MemPalace): I Challenged a Specialized Memory Library With a 30-Year-Old…"
source: "https://medium.com/@zabolotniua/ayona-openclaw-vs-milla-mempalace-i-challenged-a-specialized-memory-library-with-a-30-year-old-2cc60aa12e6e"
author:
  - "[[Serhii Zabolotnii]]"
published: 2026-04-09
created: 2026-04-20
description: "Ayona (OpenClaw) vs Milla (MemPalace): I Challenged a Specialized Memory Library With a 30-Year-Old Algorithm “The best retrieval system is the one you’ve actually measured.” — the hard …"
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

> *“The best retrieval system is the one you’ve actually measured.” — the hard way*

One morning I opened GitHub trending and saw something unusual: a repository called [MemPalace](https://github.com/milla-jovovich/mempalace), authored by **Milla Jovovich** — yes, the actress from Resident Evil — with **32.6k stars**, 4.1k forks, and a description that read:

> “The highest-scoring AI memory system ever benchmarked. And it’s free.”

The repo was real, the benchmarks were published, and the numbers were impressive: **96.6% R@5** on LongMemEval, a rigorous 500-question conversational memory benchmark. A purpose-built memory system with ChromaDB, a four-layer memory stack, and a 30x compression dialect.

Which immediately raised an uncomfortable question for me.

In Part 2 of this series, I described how we built hybrid retrieval for Ayona: BM25 + E5 embeddings, combined via Reciprocal Rank Fusion. At the time, I presented code, architecture diagrams, and real failure cases — but no formal benchmark numbers. We knew it worked well enough for our operational needs. We never asked *how well*.

Now I had a benchmark to compare against. Could our general-purpose agent pipeline compete with a celebrity-endorsed, purpose-built memory system on the same dataset?

We ran the experiment. The results surprised us.

## The Setup: Same Data, Same Questions, Same Metrics

A fair comparison requires identical conditions. We chose [LongMemEval](https://arxiv.org/abs/2410.10813) — a dataset of 500 questions across six categories, each with approximately 53 conversation sessions as the haystack. The task: given a question, retrieve the correct session(s) from the haystack.

**Three configurations tested:**

The Ayona adapter builds a fresh BM25 index for each question’s haystack, queries it, and evaluates whether the ground truth session appears in the top-K results. No embeddings, no GPU, no external API calls. Just tokenization and IDF scoring.

MemPalace creates a ChromaDB collection per question, embeds all sessions using all-MiniLM-L6-v2 (384-dimensional, ONNX runtime), and performs semantic similarity search. The hybrid\_v4 mode adds keyword overlap boosting (30% weight), temporal date parsing (40% distance reduction on date match), and quoted phrase extraction.

Same questions. Same ground truth. Same metrics: R@1, R@5, R@10, MRR, NDCG@10.

All code is [open-source](https://github.com/szabolotnii/ayona-vs-mempalace-benchmark).

## The Results

Read that again: BM25 with no embeddings achieves **96.8% R@5** — matching MemPalace’s embedding-based search (96.6%) and trailing the full hybrid\_v4 by just 1.4 percentage points. And it does so **77 times faster**.

But we didn’t stop there.

## The Full Ablation: 7 Configurations

We tested every combination: BM25 alone, BM25 with temporal date parsing, BM25 with keyword overlap boosting, all-MiniLM-L6-v2 vector search alone, hybrid BM25+vector via RRF, and the full enhanced hybrid. Same model as MemPalace (all-MiniLM-L6-v2, 384-dim) for fair comparison.

The surprise: **adding embeddings made things worse**. BM25 enhanced (97.4%) outperforms every hybrid configuration (97.0%). The vector component introduces noise that dilutes the BM25 signal through RRF fusion. On specific questions, the correct answer ranks #2 in BM25 but doesn’t appear in the vector top-30 at all — and after fusion, it drops out of the final top-10.

Vector-only retrieval (92.8%) is dramatically worse than BM25 (96.8%). On single-session-user questions, vector drops to 82.9% while BM25 holds at 98.6%.

## Per-Category Breakdown

The six-category breakdown reveals *where* each approach excels:

Two categories where embeddings genuinely help: **preference queries** (86.7% → 90.0% with hybrid) and **multi-session** (97.0% → 98.5%). Two categories where embeddings hurt: **temporal** (97.0% → 95.5%) and **single-session-user** (98.6% → 97.1%).

The implication: embeddings aren’t universally helpful or harmful — they’re *category-dependent*. A smarter system would route queries to the appropriate retrieval method based on query type, not blindly fuse everything.

## What Broke and Why

Out of 500 questions, BM25 baseline missed 16. After adding temporal date parsing and keyword overlap boosting, 3 were fixed (0 regressions), leaving 13 misses. Every failure tells a story.

**Temporal queries (6 → 4 after enhancement).** “What kitchen appliance did I buy 10 days ago?” BM25 sees tokens: *kitchen*, *appliance*, *buy*, *10*, *days*, *ago*. It finds sessions about kitchen appliances. But “10 days ago” requires resolving a relative date to an absolute timestamp and matching against session dates — something BM25 fundamentally cannot do.

We added temporal date parsing that resolves relative dates (“last Tuesday,” “two weeks ago,” “past month”) against each question’s timestamp and boosts sessions within the target window. This fixed 3 of 6 temporal misses — with zero regressions.

**Preference queries (4 misses).** “What should I serve for dinner this weekend with my homegrown herbs?” The answer is buried in a casual conversation where the user mentioned growing basil. BM25 looks for *dinner*, *weekend*, *homegrown*, *herbs* — but the relevant session uses different vocabulary. Semantic embeddings capture the conceptual proximity between “homegrown herbs” and “I’ve been growing basil in my garden” without lexical overlap.

**Multi-hop aggregation (5 misses).** “How many different doctors did I visit?” Answering requires scanning multiple sessions, extracting doctor mentions, and counting unique entities. This is fundamentally a reasoning problem disguised as a retrieval problem.

**One genuine surprise (1 miss).** “How much time do I dedicate to practicing violin every day?” — a simple factual query that BM25 should catch. On inspection, the answer session used phrasing like “I practice for two hours daily on my instrument” without the word “violin” appearing near the time commitment. A semantic match would catch this; a lexical one cannot.

## Why BM25 Works (Surprisingly Well)

The conventional wisdom in the RAG community goes like this: embeddings capture semantic meaning, BM25 only captures lexical overlap, therefore embeddings are strictly superior for retrieval. Our benchmark challenges this assumption on conversation memory tasks.

**IDF is a powerful discriminator.** When someone asks “What degree did I graduate with?”, the word *degree* has moderate IDF (common in many sessions), but *graduated* has high IDF (appears in very few sessions). BM25 effectively zeroes in on the right session through the rarity signal. Embeddings, by contrast, map “graduated” into a semantic neighborhood that includes “completed education,” “finished school,” “academic achievement” — all plausible but less discriminating.

**Conversation data is keyword-rich.** Unlike academic papers or technical documentation, conversations about daily life are full of specific, unique identifiers: names, places, activities, objects. “I bought a new coffee grinder at Williams-Sonoma” contains several high-IDF tokens that virtually guarantee a BM25 match.

**The embedding curse on vague queries.** “What should I serve for dinner?” is semantically close to hundreds of sessions that mention food, meals, cooking, recipes. The embedding space is crowded precisely where vagueness lives. BM25 at least requires some specific token overlap to score a document, which acts as an implicit precision filter.

**Hybrid gains come from heuristics, not embeddings alone.** MemPalace hybrid\_v4 outperforms raw embedding search by 1.6% R@5. But that gain comes from keyword overlap boosting and temporal date parsing — domain-specific heuristics layered on top of embeddings. The embeddings alone (raw mode) actually *underperform* BM25 on R@1 by 5.6 percentage points.

## Lessons for Production RAG Systems

## 1\. Benchmark before you optimize

We spent time building an E5 embedding pipeline, deploying a Docker container for local inference, implementing FAISS indexing — and our BM25 baseline was already at 96.8% R@5. Without a benchmark, we would have kept optimizing the embedding pipeline, never knowing the baseline was already competitive.

The cost of not benchmarking isn’t wasted compute. It’s wasted engineering attention on the wrong problem.

## 2\. Hybrid doesn’t automatically mean better

“Hybrid search” has become a default recommendation in the RAG community. Combine BM25 and embeddings via RRF, and you’ll get the best of both worlds — the story goes. Our data suggests this is true only when you add domain-specific heuristics. Pure BM25+embedding fusion without temporal parsing or keyword boosting may not justify the additional complexity and latency.

## 3\. Latency is a feature

Ayona serves responses through Telegram. At 20ms per retrieval, the search step is invisible to the user. At 1,540ms, it’s noticeable. At 2,000ms (hybrid\_v4), it dominates the response time. In a real-time chat interface, a 77x speedup is not an optimization — it’s a different product category.

## 4\. Failure analysis matters more than aggregate metrics

96.8% R@5 looks great. But the 16 failures reveal *where* the system will disappoint users: temporal questions and preference-based queries. These are exactly the scenarios where users expect AI to be “smart” — and where a production system needs explicit handling (date parsing, preference extraction), not just better embeddings.

## 5\. Open benchmarks keep you honest

We published all code, all results, and the reproduction scripts. Anyone can run the same benchmark and verify our numbers. This matters because retrieval benchmarks are notoriously sensitive to implementation details: tokenization choices, embedding model versions, index parameters. Transparency is the only defense against accidental self-deception.

## What We Did Next — and What Remains

After the initial BM25 benchmark, we implemented and tested four approaches:

**Done: Temporal date parsing** (+0.6% R@5, 3 fixes, 0 regressions). Parses “last Tuesday,” “two weeks ago,” “past month” and boosts sessions within the resolved date window. Cost: +10ms latency. Verdict: **integrate into production**.

**Done: Keyword overlap boosting** (+0.2% R@5, combined with temporal). The MemPalace hybrid\_v4 formula adapted to BM25 scores. Marginal standalone gain — BM25 IDF already captures most of this signal — but useful in combination.

**Done: Hybrid BM25 + all-MiniLM-L6-v2** (same model as MemPalace). Verdict: **does not improve overall R@5** (97.0% < 97.4% enhanced BM25). Embeddings help on preferences (86.7% → 90.0%) and multi-session (96.2% → 98.5%) but hurt on temporal (97.0% → 95.5%) and single-session-user (98.6% → 97.1%). Global hybrid is a net negative.

**Done: QMD query expansion — verdict: concept works, overhead too high.** We ran [QMD](https://github.com/tobi/qmd) (Qwen3 0.6B GGUF, local) on a 50-question subset:

- *QMD search (FTS5 BM25)* — 64% R@5 at 2,561ms. SQLite FTS5 significantly underperforms Okapi BM25 (96.8%), confirming that BM25 implementation quality matters enormously.
- *QMD query (BM25+Vec+Expand, no rerank)* — **88% R@5 at 13,075ms**. LLM query expansion brings R@5 from 64% → 88% — but still 8.8 points below our BM25 baseline at **650x the latency**.

**Done: Ukrainian morphology test** (50Q, Google Translate). BM25 without lemmatization: **94.0% R@5** (−3% vs English baseline). With pymorphy3 lemmatization: **96.0% R@5, 100.0% R@10** — full parity with English. See the Bonus section below.

**Next: Selective hybrid routing** — classify queries and route to BM25 or hybrid based on query type.

**Next: LoCoMo benchmark** (1,986 multi-hop questions) — stress-test the multi-session weakness.

## Bonus: Does BM25 Work on Ukrainian?

Ayona’s knowledge base is primarily in Ukrainian. Ukrainian has rich morphology — 7 noun cases, verb aspects, gender — meaning one word can appear in 10+ surface forms. “Лікар” (doctor, nominative) becomes “лікаря” (genitive), “лікарю” (dative), “лікарем” (instrumental). These are treated as distinct tokens by vanilla BM25.

We translated a 50-question subset of LongMemEval to Ukrainian using Google Translate and ran four configurations:

**Three findings:**

**1\. Ukrainian morphology costs ~3% R@5.** Without lemmatization, BM25 drops from 96.8% (English) to 94.0% (Ukrainian) — a modest penalty. The penalty is smaller than feared — BM25’s term frequency weighting partially compensates, and many key named entities don’t inflect.

**2\. pymorphy3 lemmatization closes the gap.** With Ukrainian morphological normalization via [pymorphy3](https://github.com/kmike/pymorphy3), R@5 reaches 96.0% — matching the English baseline. R@10 hits 100%: perfect recall within the top 10.

**3\. The latency cost is real but avoidable.** Lemmatizing at query time costs 1,498ms/q — a 79x overhead. The production solution: **lemmatize at index time** (once, when cards are added to the knowledge base). Query-time cost then drops to near-zero.

## Reproduce It Yourself

Everything is open-source: [ayona-vs-mempalace-benchmark](https://github.com/szabolotnii/ayona-vs-mempalace-benchmark).

```c
# 1. Download dataset
curl -fsSL -o data/longmemeval_s_cleaned.json \
  https://huggingface.co/datasets/xiaowu0162/longmemeval-cleaned/resolve/main/longmemeval_s_cleaned.json

# 2. Run BM25 benchmark (10 seconds, no GPU needed)
pip install numpy requests
python src/lme_adapter.py data/longmemeval_s_cleaned.json --mode bm25 -v

# 3. Run MemPalace benchmark (~15 minutes, CPU embedding)
pip install mempalace
bash benchmarks/run_mempalace.sh
```

Pre-computed results for all configurations are included in `results/`.

## Conclusion

We assumed embeddings would win. We assumed a specialized memory library would outperform a general-purpose agent pipeline. We assumed that adding semantic search was always worth the complexity and latency cost.

None of these assumptions survived contact with a benchmark.

BM25 — an algorithm from 1994 — achieved 96.8% recall on a modern conversational memory benchmark, matching a 2026 embedding-based system while running 77 times faster. After adding temporal date parsing (+0.6%), it reaches 97.4% — trailing MemPalace hybrid\_v4 by just 0.8%.

The most counterintuitive finding: **adding embeddings (all-MiniLM-L6-v2) to BM25 made overall retrieval worse** (97.0% < 97.4%). Vector noise dilutes the BM25 signal in global RRF fusion. Embeddings help on exactly two categories — preferences and multi-session — and hurt on two others.

One more finding, often overlooked in English-centric benchmarks: **BM25 generalizes to morphologically rich languages**. On Ukrainian (50Q), BM25 achieves 94.0% R@5 without any language-specific tuning — only 3% below the English baseline. Adding pymorphy3 lemmatization restores full parity at 96.0% R@5, 100.0% R@10. The algorithm from 1994 works in 2026 across language families.

The practical recommendation: start with BM25. Benchmark it. Analyze the failures by category. Add targeted enhancements (temporal parsing, query expansion) for the specific failure modes you find. Use embeddings selectively, not globally. Lemmatize at index time for morphologically rich languages. And measure everything — because the intuitive answer (“embeddings are better”) is often wrong.

*Serhii Zabolotnii — DSc, NLP/LLM Researcher, Professor, AI Systems Architect. Building* [*Ayona*](https://medium.com/@zabolotniua/when-a-single-agent-hits-its-limits-ayona-openclaw-shift-from-orchestration-to-composition-38492b1bab9c) *— an AI-native research and operations system. This is Part 4 of the Ayona/OpenClaw Architecture series. Acknowledgments:* [*MemPalace*](https://github.com/milla-jovovich/mempalace) *for an excellent memory library with public benchmarks.* [*LongMemEval*](https://arxiv.org/abs/2410.10813) *(Wu et al., 2024) for the dataset.* [*QMD*](https://github.com/tobi/qmd) *for LLM query expansion runtime.*

[![Serhii Zabolotnii](https://miro.medium.com/v2/resize:fill:96:96/0*MyyIF1nB3iGg8cE_)](https://medium.com/@zabolotniua?source=post_page---post_author_info--2cc60aa12e6e---------------------------------------)

[![Serhii Zabolotnii](https://miro.medium.com/v2/resize:fill:128:128/0*MyyIF1nB3iGg8cE_)](https://medium.com/@zabolotniua?source=post_page---post_author_info--2cc60aa12e6e---------------------------------------)

[68 following](https://medium.com/@zabolotniua/following?source=post_page---post_author_info--2cc60aa12e6e---------------------------------------)

## Responses (1)

Benedek Molnar

What are your thoughts?  

```c
Personal digital memory has value. That value might be multiplied with collective human digital memory and reasoning. Is any existing open source, decentralized database software good enough?
```