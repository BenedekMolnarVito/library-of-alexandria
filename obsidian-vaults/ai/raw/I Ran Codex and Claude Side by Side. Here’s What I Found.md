---
title: "I Ran Codex and Claude Side by Side. Here’s What I Found."
source: "https://ai.gopubby.com/i-ran-codex-and-claude-side-by-side-heres-what-i-found-ee16ea991838"
author:
  - "[[Yanli Liu]]"
published: 2026-04-12
created: 2026-04-18
description: "I Ran Codex and Claude Side by Side The setup takes 5 minutes. The compliance question takes longer. Last week I installed OpenAI’s Codex plugin inside Claude Code. Four commands, five minutes, and …"
tags:
  - "clippings"
---
## [AI Advances](https://ai.gopubby.com/?source=post_page---publication_nav-3fe99b2acc4-ee16ea991838---------------------------------------)

[![AI Advances](https://miro.medium.com/v2/resize:fill:48:48/1*R8zEd59FDf0l8Re94ImV0Q.png)](https://ai.gopubby.com/?source=post_page---post_publication_sidebar-3fe99b2acc4-ee16ea991838---------------------------------------)

Democratizing access to artificial intelligence

## The setup takes 5 minutes. The compliance question takes longer.

Last week I installed OpenAI’s Codex plugin inside Claude Code. Four commands, five minutes, and suddenly I had two competing AI systems running in the same terminal session — one drafting, one critiquing.

[Read this article for free](https://ai.gopubby.com/i-ran-codex-and-claude-side-by-side-heres-what-i-found-ee16ea991838?sk=451f44f4a6ed46a81d45f9e403697c79)

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*iWDesSmTqoyoln4D)

Photo by Tim Gouw on Unsplash

It felt like a parlor trick. Then I read what Microsoft shipped the same day.

Copilot Cowork, now live for enterprise Microsoft 365 customers, does the same thing at a completely different scale. GPT drafts a research report. Claude audits it. A third model synthesizes both.

It reports a 13.8% benchmark improvement over its nearest competitor — measured by the competitor’s own test, graded by the vendor’s own model. And for those of us working inside regulated institutions, it contains a compliance gap that nobody in tech press has written about yet.

This article covers both levels:

- First, the practical: how to pair Claude Code and Codex in your own workflow today, with a before/after example that shows exactly where second opinions matter.
- Then the architectural: what Microsoft actually built, why the benchmark story is more complicated than it looks, and the specific question that every bank deploying this product should be asking before go-live.

## The Official Plugin Nobody Talks About

**On March 30, OpenAI released an official plugin for Claude Code.** Not a community fork, not a hack. An official release from OpenAI, published under their own GitHub account, designed to run Codex inside their direct competitor’s tool.

That’s worth pausing on. The two companies are racing for the same market. Their models compete on the same benchmarks. And OpenAI just shipped a plugin that extends Claude Code’s capabilities.

The business logic is clear in retrospect: developers who live in Claude Code aren’t going away, and Codex needs to be where developers are. But the result is useful regardless of the strategy behind it.

**What the plugin actually does.** It adds Codex as a background subprocess inside your Claude session. Claude handles your active work — reading files, editing, reasoning over context. Codex takes tasks you hand it and runs them asynchronously, so you stay unblocked. Two models, two execution environments, one terminal.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Akv_LwO2n67fwtDt2Z8JXQ.png)

Claude Code + Codex: Two Agents, One Terminal

**The setup takes five minutes.** You need Node.js 18.18+, a ChatGPT account (free tier works) or an OpenAI API key, and Claude Code already running.

Install Codex CLI:

```rb
npm install -g @openai/codex
codex login
```

Add the plugin inside Claude Code:

```rb
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

The last command confirms everything is connected. If it prints a version number, you’re ready.

**What does it cost?** If you’re using your own OpenAI API key, each `/codex:rescue` call runs roughly 2K input tokens + 1K output tokens at GPT-5.4 pricing ($2.50/$15 per million tokens) -- about $0.02 per call. At 50 calls a day, that's ~$1/day, or $30/month. Heavy users running background research loops should watch their token usage. The free ChatGPT account tier rate-limits aggressively; for regular use an API key is more reliable.

## What Adversarial Review Actually Catches

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*BWc3iO2ZYmKvfWR3qQSRig.png)

Diagram by Author: What Adversarial Review Actually Catches

**For code work, use** `**/codex:adversarial-review**`**.** It doesn't just check for bugs -- it challenges design decisions, questions assumptions, and surfaces edge cases you haven't considered.

Here’s what that looks like in practice. I asked Claude to write a Python function to process a batch of API responses:

**Claude’s output (summarized):**

```rb
def process_batch(responses):
    results = []
    for r in responses:
        if r.status_code == 200:
            results.append(r.json()["data"])
    return results
```

Claude’s review of its own code: *“Looks correct. Handles the success case, filters non-200 responses.”*

**After running** `**/codex:adversarial-review**`, Codex flagged three issues:

1. `r.json()["data"]` raises `KeyError` if the API returns a 200 with no `"data"` key -- a real case for partial responses
2. No handling for `r.json()` itself failing (malformed JSON on a 200 is more common than it sounds)
3. Silent discard of non-200 responses means errors disappear — any monitoring downstream will miss failures

Claude had read the same code and said it looked fine. Two models. Different answers. Both useful — but one of them was actually useful.

The reason this works isn’t magic. Claude and Codex have different training distributions, different fine-tuning histories, different failure modes. When they disagree, the disagreement is usually pointing at something real.

**For non-coding work,** `**/codex:rescue**` **changes how you do research.** You don't have to be writing code to get value from the pairing.

Say you’re mid-draft on a document and need background on a topic — but you don’t want to lose your current Claude context. Hand the task off:

```rb
/codex:rescue research the EU AI Act Article 12 logging requirements
and summarize what a bank needs to document for high-risk AI systems
```

Codex runs that as a background job. You keep writing. When it’s done:

```rb
/codex:result
```

The summary comes back into your session. No tab switching, no lost context, no waiting. I use this for competitive research, fact-checking claims mid-draft, and checking whether a technical approach has known issues before committing to it.

**When NOT to use the Codex plugin.** It adds overhead. For small scripts you’ll throw away in an hour, the review cycle slows you down more than it helps. For exploratory tasks where you’re still figuring out the problem, adversarial review of an early draft mostly generates noise. And for anything where Claude’s reasoning depth already exceeds the complexity of the task, a second opinion doesn’t add much. Use it on work that matters — PRs going into production, research you’ll rely on for a decision, documents that will be read by people who aren’t you.

Now zoom out. What you just set up on your laptop — one model drafting, another reviewing — Microsoft shipped that same pattern at enterprise scale, inside Outlook, Teams, and Excel. And at that scale, the architecture creates a problem nobody in tech press has asked about yet.

## Two Architectures, Not One

**Most coverage of Copilot Cowork conflates two separate features.** They have different architectures, different tradeoffs, and different implications for accountability.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*vYnFtyZfTGnsF_85eN4zug.png)

Diagram by Author: Critique: Sequential Review Pipeline

The first is **Critique**.

Critique is sequential. GPT plans the research task, iterates through retrieval, and produces an initial draft with citations. Then Claude steps in as a reviewer, auditing that draft across three dimensions: source reliability, report completeness, and evidence grounding. You never see the intermediate draft. What you get is the final reviewed output, delivered as a single Researcher answer.

The design is intentional. The goal is a cleaner user experience — one answer, already checked. The review happens in the background and surfaces only if something changes.

**You can replicate this pattern today.** With the Codex plugin installed, `/codex:adversarial-review` runs the same sequential logic on whatever Claude just produced -- code, a document, a research summary. The reviewer has a different training distribution and different failure modes. The disagreements are where the value is.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*nMYdDCpFEubtYM83jnGqqw.png)

Diagram by Author: Model Council: Parallel Architecture

**The second is Model Council**, and it works differently.

Model Council runs in parallel. GPT and Claude each produce a complete, independent report on the same question simultaneously. A third “judge model” then evaluates both outputs, generating a synthesis that shows where the models agree, where they diverge, and what each found that the other missed. The disagreements are visible. You see them.

This is a more honest architecture. It acknowledges that two frontier models will reach different conclusions on the same source material — and surfaces that tension rather than hiding it.

**You can replicate this too.** Run `/codex:rescue [your question]` while Claude is answering the same question in your active session. When `/codex:result` returns, compare them. Where they agree, your confidence goes up. Where they diverge, something is worth examining. I use this for any research claim I'm about to put a number on.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*X1JkA6x2LsmgCXNVDoH0zQ.png)

Diagram by Author: Critique vs. Model Council vs. DIY Plugin

**The tradeoff is transparency versus convenience.** Critique gives you a clean answer. Model Council gives you the map of the disagreement. Which one you want depends on what you’re doing with the output — and, as we’ll see, how accountable you need to be for it.

Both features are live in Copilot Cowork’s Frontier tier as of March 30. Both require admin enablement — IT has to approve Claude access to the M365 tenant before either activates.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*pTZ2YkT9xyoyKQ_SdEsZAw.png)

Diagram by Author: DRACO Benchmark: Multi-Model Review Wins

> ***The commercial context in brief:*** *Microsoft’s stock fell 23% in Q1 2026 — worst quarter since 2008. Only 3.3% of 450M M365 subscribers pay for Copilot. When competing head-to-head against ChatGPT, users choose Copilot 18% of the time. The E7 bundle at $99/seat (May 1) is the monetization vehicle, bundling M365 E5 + Copilot + Agent 365 + Entra Suite. Cowork’s multi-model features justify the price jump. And the benchmark they chose — DRACO — was created by Perplexity, their direct competitor. Microsoft ran the tests themselves, used GPT-5.2 as judge (same vendor as the drafter), and hasn’t had results independently replicated. The 13.8% improvement may be real. It hasn’t been verified by anyone without a stake in the outcome.*

One more detail: the Anthropic partnership here is unusual. Microsoft is using Anthropic’s Claude to power a product that competes directly with Anthropic’s own standalone Claude Cowork offering.

**Same underlying model. Very different governance layer.**

## The Attribution Gap

As someone who works inside a bank, the first question I asked when I read about Critique wasn’t “does it work?” It was: “which model said what, and can I prove it to an examiner?”

The answer, as of today, is no.

**Here’s the specific problem.** Critique is designed to hide the intermediate draft. That’s a feature: it gives you a clean final answer without making you reconcile two competing outputs. But it means the identity of which model version produced which claim is abstracted behind Microsoft’s orchestration layer. You receive one Researcher output. The model attribution is not in that output.

For most use cases, that’s fine. For regulated use cases, it isn’t.

**SR 11–7 — the Federal Reserve’s model risk management guidance — applies to every model a bank uses in a consequential decision.** It requires banks to identify each model, validate it independently, document its limitations, and monitor its ongoing performance. Critically: outsourcing to a vendor does not transfer the bank’s regulatory accountability. The OCC, Fed, and FDIC are all actively applying SR 11–7 principles to generative AI deployments.

Critique creates a two-model pipeline. SR 11–7 wants documentation on both models. The output doesn’t tell you which GPT version drafted and which Claude version critiqued. If Microsoft updates either model silently, which they can, you may not know.

**The EU AI Act adds a second layer.** Article 12, effective August 2, 2026, requires that high-risk AI systems maintain automatic, event-level logs with traceability. Credit scoring, AML/fraud detection, loan approval, and KYC systems are all classified high-risk under Annex III. If a bank deploys Critique for research supporting any of those functions, the logging requirement applies to the pipeline, not just the output.

What Microsoft currently provides is M365-level audit logging, who ran what query, when. That’s not the same as per-model attribution per inference call. Whether E7 customers can get model-level logs is a question Microsoft has not publicly answered.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*89ehzRAyaHwwtBSFW5WalA.png)

Diagram by Author: The Attribution Gap: What’s Required vs. What Critique Provides

**Here’s the scenario that concerns me.** A compliance officer uses Copilot Researcher with Critique to assess whether a specific derivative structure is permissible under CFTC guidance. The pipeline returns a confident, well-cited answer. One citation is misread; one regulatory interpretation is slightly wrong. The bank relies on it. An examiner asks six months later: which model version produced that interpretation? Was it validated under SR 11–7? What was the model’s version at the time of the query?

Under the current architecture, none of those questions have answers the bank can produce.

I want to be honest about what I don’t know here. It’s possible Microsoft provides per-model audit logs to E7 customers and simply hasn’t documented it publicly. It’s possible the forthcoming FCA guidance on multi-model AI pipelines will clarify what “adequate logging” means for systems like Critique. These are open questions. But “possible” isn’t a satisfying answer to a bank examiner. And right now, the public documentation doesn’t close the gap.

## What To Do

Which Multi-Model Pattern Should You Use?

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*QRx-kICL3Iu3-49n9Umzdw.png)

Diagram by Author: Which Multi-Model Pattern Should You Use?

**If you’re a developer or knowledge worker**: the plugin is at `github.com/openai/codex-plugin-cc`. Five-minute setup. Start with `/codex:adversarial-review` on the next piece of work you care about. Use `/codex:rescue` for tasks that would break your context if you handled them yourself. One caveat: automated loops between Claude and Codex can consume API usage quickly. Keep a human in the loop until you know your patterns.

**If you’re evaluating Copilot Cowork at a regulated institution**, three questions for your next vendor call before go-live:

1. Which model versions are in the Critique pipeline right now, and will you notify us when either model is updated?
2. Do E7 customers receive per-model attribution in audit logs, or only aggregate M365 query logs?
3. How does your documentation support our SR 11–7 model inventory and EU AI Act Article 12 traceability obligations for the Critique feature specifically?

If the answers are vague, that’s the answer. It doesn’t mean don’t deploy — it means don’t deploy Critique for work touching high-risk AI use cases until the documentation exists.

**If you manage model risk**: flag Critique for SR 11–7 review before it goes live. Model Council is more defensible — both outputs are visible, both can be documented. That transparency tradeoff matters more than it looks when an examiner calls.

**What to watch:** FCA guidance on multi-model audit trails is expected H2 2026. Independent DRACO replications will appear within months. The EU AI Act clock hits banks on August 2.

## What Actually Changed in My Workflow

The adversarial review pattern changed something subtle about how I work. Before, I’d ask Claude for a second read on something I wasn’t sure about. Now I route that through Codex instead — not because Codex is smarter, but because a reviewer with different blind spots is more useful than the same model reading its own output.

I also stopped treating the cases where they disagree as noise. The disagreement is usually the finding. Two frontier models reaching different conclusions on the same source material almost always means someone’s making an assumption worth examining.

What I haven’t done yet is use Copilot Cowork’s Critique at work. Not because the feature isn’t impressive — it is. But until Microsoft answers the attribution question, deploying it for anything that could end up in front of an examiner feels like a documentation gap I’d have to own. The Model Council is more honest. I’d start there.

The multi-model quality loop is here. The technical architecture is clever. The governance architecture is still catching up — and that gap is yours to manage, not Microsoft’s.

## [Harness Engineering: What Every AI Engineer Needs to Know in 2026](https://ai.gopubby.com/harness-engineering-what-every-ai-engineer-needs-to-know-in-2026-0ab649e5686a?source=post_page-----ee16ea991838---------------------------------------)

### Harness Engineering: What Every AI Engineer Needs to Know in 2026 Three camps, three architectures - and what Opus 4.7…

ai.gopubby.com

## [Claude Is an Engine. The Harness Is the Product Now.](https://levelup.gitconnected.com/claude-is-an-engine-the-harness-is-the-product-now-584f7d3e0f41?postPublishedType=repub&source=post_page-----ee16ea991838---------------------------------------)

### Claude Is an Engine. The Harness Is the Product Now. What superpowers and everything-claude-code install inside it…

levelup.gitconnected.com

## Before you go! 🦸🏻♀️

If you liked my story and you want to support me:

1. Throw some Medium love 💕(claps, comments and highlights), your support means the world to me.👏
2. [Follow me](https://medium.com/@yanli.liu/about) on Medium and subscribe to get my latest article🫶

## [About - Yanli Liu - Medium](https://medium.com/@yanli.liu/about?source=post_page-----ee16ea991838---------------------------------------)

### Read writing from Yanli Liu on Medium. Daytime finance practitioner based in Luxembourg, seasoned coder, and passionate…

medium.com[Artificial Intelligence](https://medium.com/tag/artificial-intelligence?source=post_page-----ee16ea991838---------------------------------------)[Programming](https://medium.com/tag/programming?source=post_page-----ee16ea991838---------------------------------------)[Technology](https://medium.com/tag/technology?source=post_page-----ee16ea991838---------------------------------------)[Productivity](https://medium.com/tag/productivity?source=post_page-----ee16ea991838---------------------------------------)

## Responses (3)

Benedek Molnar

What are your thoughts?

```c
ran something similar - the second-opinion architecture works until you have to explain the audit trail. who decided, and when? that's where the complexity actually lives.
```

7

```c
Some time ago I developed consensus- a moderated ‘discussion’ platform for LLMs with optional humans in the loop, persistent shared searchable memory, and multiple adversarial modes. Solved a great many problems- programming or otherwise- for me…
```

5

```c
The 'disagreement is usually the finding' line is the part reshaping how we review internal research. Divergence points between Claude and Codex map almost 1:1 onto the paragraphs a human editor later had to rewrite, and the attribution gap isn't…
```

1

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--ee16ea991838-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)