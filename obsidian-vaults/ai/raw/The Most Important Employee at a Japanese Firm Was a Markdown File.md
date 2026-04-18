---
title: "The Most Important Employee at a Japanese Firm Was a Markdown File"
source: "https://ai.gopubby.com/the-most-important-employee-at-a-japanese-firm-was-a-markdown-file-8f079d9c4d19"
author:
  - "[[Kaitai Dong]]"
published: 2026-04-05
created: 2026-04-18
description: "The Most Important Employee at a Japanese Firm Was a Markdown File How a Japanese tax accountant uses CLAUDE.md to serve 60 clients and what it reveals about future of knowledge work. A Viral Post on …"
tags:
  - "clippings"
---
## [AI Advances](https://ai.gopubby.com/?source=post_page---publication_nav-3fe99b2acc4-8f079d9c4d19---------------------------------------)

[![AI Advances](https://miro.medium.com/v2/resize:fill:48:48/1*R8zEd59FDf0l8Re94ImV0Q.png)](https://ai.gopubby.com/?source=post_page---post_publication_sidebar-3fe99b2acc4-8f079d9c4d19---------------------------------------)

Democratizing access to artificial intelligence

## How a Japanese tax accountant uses CLAUDE.md to serve 60 clients and what it reveals about future of knowledge work.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*cTYYrX4I-qjdltXZtoLkHQ.png)

Figure 1: A screenshot of the original viral post on X by a tax accountant from Japan

## A Viral Post on X

A Japanese tax accountant with **zero programming experience** runs a firm serving **60 clients**, with **no employees**, and still leaves work at 5pm.

At first glance, this sounds like another exaggerated AI story on X \[1\]. The kind that circulates on social media for a few days before fading away.

But this one feels different.

Because the secret isn’t “AI automation” in the usual sense. It’s not a complex system, not a custom-built platform, not even a piece of code.

It’s a text file. A single file called `**CLAUDE.md**`.

The office might close at 5pm, but the system doesn’t. Later that night, Claude Code will wake up, pull unprocessed accounting entries, classify the routine ones, and leave only the ambiguous cases for the human to review the next day.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Dfp-NtJI5fv7M8CPg0YUyA.png)

Figure 2: A daily operating workflow described in the viral X post \[Image by Author\]

What captures everyone’s attention is the operator of this workflow. A Japanese accountant whose entire career was built in audit, corporate accounting, and tax, not software. He is not presenting himself as a hacker who discovered a clever shortcut. He is presenting himself as a **domain expert who found a new way to express the logic** **of his work**.

> “The most important employee in the office was not a person. It was a markdown file.”

## Why This Story Mattered

The reason this post traveled is not that it claimed a non-technical person could use AI. We already know that.

The reason it mattered is that it hinted at a deeper change: the edge is no longer only technical virtuosity. ==Increasingly, the edge belongs to whoever can== ==**decompose real work**== ==into steps, exceptions, handoffs, and review points.==

The scarce skill is NOT merely “prompting.” It is **operational translation**. I believe that professionals who traditionally have worked at the back-scene would thrive because they know how work is actually done, where exceptions live, and what must never be automated. They hold the edge.

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*dOpjGDbZBWQjMGPvqz145w.png)

Figure 3: The modern day edge for AI practitioners \[Image by Author\]

This is why the story feels bigger than one accountant’s workflow.

For years, the common mental model of AI has been “a smarter search box” or “a faster draft writer.”

But here, this tax accountant is ==not just asking for outputs. He is defining a role, assigning tools, specifying decision rights, and deciding what gets escalated. Simply put, he is defining== ==**system-level behaviour**==.

This is basically to **take professional knowledge** — the kind that normally lives in habits, judgment, and repeated explanations — and **convert it into explicit operational structure**. Impressive!

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*99NiJ4RcUgXl20Mr1ST0Xg.png)

Figure 4: The visual comparison between the traditional and agentic office workflow \[Image by Author\]

Anthropic’s own language is useful here. In its engineering writing, the company argues that the frontier has shifted from prompt engineering toward **context engineering**: the hard problem is no longer a single clever instruction, but the **curation of all the context that shapes an agent’s behavior** — instructions, files, tool access, memory, and surrounding constraints.

## Technical Autopsy

### What CLAUDE.md Actually Is

At its core, `CLAUDE.md` is simple:

> *A persistent instruction file that Claude reads before doing any work.*

But that undersells what it really is. Using an analogy, `CLAUDE.md` is an **employee handbook for an AI worker**.

Inside it, you define:

- what the AI’s role is
- what it should do
- what it must never do
- how it interacts with tools
- how it handles data

And every time Claude starts working, it reads this file **first**.

Claude Code supports *user* -, *project* -, and *organization* -scoped `CLAUDE.md` files, where more specific instructions take precedence over broader ones. Parent-directory `CLAUDE.md` files will load at launch and nested files in subdirectories load on demand.

Also, larger instruction sets can be split into `.claude/rules/` so they only load when Claude works on relevant files. Anthropic also supports `@path` imports, so a `CLAUDE.md` can pull in other docs, and recommends keeping each file concise—roughly under 200 lines—because these files consume context and are treated as context, not hard-enforced configuration. `/init` can generate a starter `CLAUDE.md` automatically.

The key idea here is that `**CLAUDE.md**` is not a memory dump. It is a **control surface**.

### The System Was Built in Four Simple Steps

In his viral X post, the author said what he did was surprisingly simple, i.e.,

- create a folder structure
- write `CLAUDE.md`
- connect tools using MCP
- turn repeated work into “Skills” (commands).

That’s it.

But each of these is deceptively powerful because each step is not just a setup task — it’s a **design decision about how work should be structured**.

![](https://miro.medium.com/v2/resize:fit:1302/format:webp/1*ZhV8oi4bH4__UOBh7ukFfA.png)

Figure 5: The 4-step Claude code setup provided by the Japanese tax accountant on his agentic tax processing workflows \[Image by Author\]

### Step 1: Define the AI’s Workspace

Before writing any instructions, before connecting any tools, he did something much more basic — He created a place for the AI to work.

```c
ai-management/
├── output/       # AI-generated files
├── reference/    # documents AI can read
├── clients/      # per-client folders
├── tools/        # automation scripts
├── work-log/     # logs
├── finance/      # accounting related
```

At first glance, this looks trivial. Just folders. But this is where most people go wrong.

AI systems don’t have an implicit sense of “where things belong.” **If you don’t define a structure, they behave wildly and the system will become unstable because the environment is undefined**.

Giving the AI a workspace is like onboarding a new employee, you show them where documents should go, where client files should stay, and where logs need to be stored. This will drastically improve consistency.

If you want to replicate this, don’t start with prompts, start with **structure** first and think about **environment design**.

Ask yourself:

> If an assistant joined today, where would they look for items or save things?

And then make that **explicit**.

### Step 2: Write CLAUDE.md

Once the workspace exists, the next step is defining how work should happen inside it.

This is where `CLAUDE.md` comes in.

Looking back, the author describes his setup for `CLAUDE.md` as surprisingly simple. It always revolves around 4 basic building blocks. But beneath that simplicity is something more important — a way of **turning work into a system that an AI can actually execute**.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*xgQ2b393HvZAJFFqlrRQYA.png)

Figure 6: The 4-block CLAUDE.md setup and its operational meaning \[Image by Author\]

Let’s now see how the author describes and implement each of these 4 blocks in his `CLAUDE.md`.

### — 1st block: Define the AI’s Role Clearly

The very first thing he did was tell the AI who it is.

Not in vague terms like “help me with accounting,” but in a way that mirrors how you would onboard a new employee:

> *“You are the execution layer of an AI tax office.”*

With a defined role, it becomes proactive. It begins to understand what it is responsible for, and more importantly, what it is not.

In his case, the division was explicit:

- **The AI handles execution**: bookkeeping, document drafting, task organization
- **The human handles judgment**: tax decisions, edge cases, final approval

### — 2nd block: Draw a Hard Line Between What AI Can and Cannot Do

This is where the system becomes reliable.

One line in his `CLAUDE.md` defines everything:

> *“AI must never make tax judgments.”*

At first glance, it might seem limiting. In reality, it’s what makes the entire system usable.

Instead of trying to make AI “smart enough” to do everything, he defines boundaries:

- If a transaction matches known patterns → AI processes it
- If it’s new or ambiguous → Human handles it
- If it involves regulated judgment → AI escalates

Moreover, the exclusion rules are just as important as the automation rules. As an example, his setup automatically prevents autonomous booking if any event describe below is identified. That is not a footnote. That is the system’s moral center. The technical sophistication is not in maximizing autonomy. It is in knowing where autonomy must end.

```c
Automatically excluded from autonomous booking:
1. Unclear charges
2. Loan repayments
3. Social insurance and taxes
4. Payroll
5. Investment activity
6. ATM withdrawals
7. Utilities requiring special handling
```

For anyone building similar systems, this is the first principle to internalize. Before asking “what can AI do?”, ask:

> *What should AI never be allowed to decide?*

That boundary is where trust is built.

### — 3rd block: Connect the AI to Real Tools

At first glance, tool integration looks like an external setup step: you connect APIs, configure MCP, and wire systems together.

But in this system, that’s only half the story. The more important half is this:

> *The* ***rules for how tools are used*** *live inside* `***CLAUDE.md***`*.*

`CLAUDE.md` defines **when, why, and how those capabilities are exercised**.

Inside `CLAUDE.md`, the author effectively encodes instructions like:

```c
- Use freee to retrieve unprocessed transactions
- Register journal entries only after classification is confirmed
- Use Google Calendar to check today’s schedule before generating tasks
- Use Notion for storing meeting notes and TODOs
- Use Gmail only for drafting replies, not sending without approval
```

This equates to giving Claude instructions on how to use tools repeatably and reliably. This will turn tool access into **operational behavior**. When building your own system, you shall avoid saying “connect notion/slack”, instead you shall define:

- when should the AI use each tool
- what actions are allowed
- what requires confirmation
- what outputs should look like and where it shall be saved

### — 4th block: Security Design

This is the part of the story that gives the whole thing credibility.

It is easy to build an AI demo that looks impressive. It is much harder to build a system that touches real client data, real accounting workflows, and real professional obligations without becoming reckless.

His approach is much more controlled. For this reason, he identified a number of risk principles and how he planned to handle it and then encoded directly into AI’s behavior via `CLAUDE.md`. Essentially, he came up with a **risk-aware** system design with AI as one component inside it.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*pugNS-uUXMyclxegzSLIfA.png)

Figure 7: The risk principles adopted in the security design inside CLAUDE.md \[Image by Author\]

With the security constraints or rules above, whenever Claude processes a task:

1. It reads `CLAUDE.md`
2. It applies security rules before acting
3. It decides:
- Can I proceed?
- Should I mask data?
- Should I escalate?

So security becomes part of the **decision loop**, not an afterthought.

### Step 3: Connect External Tool via MCP

In his setup, the AI is wired into:

- accounting software (freee)
- calendar systems
- note-taking tools (Notion)
- communication platforms (Slack, Gmail)

All of this is done through **MCP** (Model Context Protocol), which **allows the AI to interact with APIs and external systems** directly.

The actual setup of MCP has become relatively straightforward and readers can find plenty of tutorials for this. It will not be discussed here.

### Step 4: Turn Repeated Work into Commands

The final layer is what makes the system feel “alive.”

Instead of manually triggering workflows step by step, the author defines **Skills** — short commands that encapsulate complex operations. (If you would like to find out how to define Skills iteratively, check out this [article](https://medium.com/ai-advances/agent-skills-the-complete-workflow-build-test-benchmark-iterate-944cb8b1c29f) I wrote!!)

For example:

- Typing “ **Good morning** ” generates the day’s schedule and task plan
- Typing “ **Remember this** ” stores context into memory
- Typing “ **Accounting** ” triggers batch processing across all 60 clients

This is more than convenience. It’s abstraction.

You’re taking a multi-step workflow and compressing it into a single interface — a command.

For readers looking to apply this idea, the pattern is straightforward:

1. Identify tasks you repeat frequently
2. Break them into steps
3. Wrap those steps into a single command

Over time, your work shifts from executing tasks to **invoking systems**.

### The Nightly Accounting Runtime with CLAUDE.md

Now let’s circle back to the scene I described at the beginning. With the help of `CLAUDE.md`, this Japanese tax accountant now has one of the most important workflows in his office running at night.

At 21:00, Claude kicks off an accounting batch against Freee and retrieves unprocessed transactions. It then normalizes the descriptions so that the raw transaction text becomes easier to classify consistently.

From there, the system checks whether the transaction matches a known pattern in a keyword dictionary. If it does, the entry can be classified deterministically. If it does not, Claude steps in as a fallback classifier, using the masked description and amount to infer the most likely category. High-confidence results can continue through the pipeline; low-confidence cases are held back for human confirmation.

Before anything is finally written back, the system performs duplicate checks so that the same entry is not posted twice.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ChZmEzaZh7CFHDN7I3M8Lw.png)

Figure 8: The nightly accounting workflow utilized to handle tax-related tasks \[Image by Author\]

As you might have noticed, the pipeline is a **selectively autonomous** one. The system is designed to absorb routine operational load across many clients, while preserving human judgment for the cases that are new, ambiguous, regulated, or simply too risky to guess on.

If you want to generalize this pattern beyond accounting, the design is surprisingly reusable. Replace “freee” with your source system, replace “account category” with your own classification task, and keep the same control logic:

- pull work from the system of record
- normalize it
- route known cases through rules
- send unknown cases to the model
- require review when confidence is low
- write back only after checks
- log everything

Always remember, **rules first, model second, and human last**!

## My thesis

My own read is that this is not really a story about no-code. It is a story about **domain experts becoming system designers**.

The Japanese tax accountant still needed to decide what counted as routine, what counted as regulated judgment, what should be masked, what could be sent to a model, what needed a confidence threshold, and what must be kept for human review. None of that is trivial. In fact, it is exactly the hard part. The code may increasingly be written by Claude Code, but the system still depends on someone who understands the work well enough to translate it into structure.

That is why I think `CLAUDE.md` is more important than it first appears. It is not merely a prompt file. It is a compressed org chart, playbook, and control policy. It tells the agent who it is, what tools it can touch, where judgment ends, and how data should move. Read that way, the most interesting shift in AI is not that models are getting better at answering questions. It is that people are beginning to author workers in plain language.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*NANXuakmcyz2x2KxIlO4jA.png)

Figure 9: The side by side comparison between what was in the past and what is in the present for AI practitioners \[Image by Author\]

For engineers, that implies a different kind of leverage than the one the industry usually celebrates. The interesting work is not only model selection or prompt tweaking. It is building the envelope around the model: the tool interfaces, the path-scoped rules, the permission boundaries, the sandbox, the structured outputs, the evals, the audit trail, and the fallback logic.

For non-engineers, the lesson is almost the mirror image. The phrase “I can’t code” is becoming less predictive than it used to be. The more important question is: can you describe your work precisely? Can you split routine from exception? Can you articulate which decisions are reversible, which are regulated, which are ambiguous, and which are too sensitive to automate? In the world this post points toward, that ability may matter as much as traditional technical skill.

The deepest idea in the Japanese post is the simplest one: **the hard part is learning to write your own work down so clearly that another intelligence — human or machine — can reliably carry part of it**. That is not just a new AI skill. It is a new management skill. And it may turn out to be one of the defining literacies of this era.