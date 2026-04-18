---
title: "Stop Vibe Coding: The 4-File System That Turns AI Agents Into Reliable Engineers"
source: "https://medium.com/@creativeaininja/stop-vibe-coding-the-4-file-system-that-turns-ai-agents-into-reliable-engineers-ae1622924cd6"
author:
  - "[[Kristopher Dunham]]"
published: 2026-03-31
created: 2026-04-18
description: "Stop Vibe Coding: The 4-File System That Turns AI Agents Into Reliable Engineers AI coding agents are now capable of reading your entire codebase, writing files, running tests, and committing code …"
tags:
  - "clippings"
---
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ODjp_6UfyF0ImEHfkdxSZA.png)

AI coding agents are now capable of reading your entire codebase, writing files, running tests, and committing code without you touching the keyboard. That’s not speculation. That’s what Claude Code, Cursor, and Copilot Workspace are doing right now.

And yet, most teams are getting mediocre results from them. Code that compiles but misses the actual requirements. Security holes that weren’t there before. Duplicated logic scattered across files nobody planned. The common diagnosis is that the AI “isn’t smart enough yet.” That diagnosis is wrong.

The AI is doing exactly what it’s told. The problem is what you’re telling it.

## Vague Instructions Are the Only Bug That Matters

Here’s something that should stop you cold: a 2025 study by METR found that experienced developers using AI coding tools without structured guidance were actually 19% *slower* than developers working without AI. Those same developers believed they were 24% faster.

That gap between perceived speed and real speed is the most expensive mistake in software development right now. Teams ship slower, think they’re flying, and never understand why their codebase is quietly degrading.

What closes that gap isn’t a better model. It’s a better specification.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*2ozNyneDvsPzhwxhJm-YwA.png)

Researchers at Veracode found that 86% of AI-generated code written without structured prompts had XSS vulnerabilities. GitClear tracked a roughly fourfold increase in code duplication across the industry between 2020 and 2024, driven largely by unguided AI generation. And UserVille’s benchmarks showed model performance jumping from an F1 score of 44 to 65 when vague prompts were replaced with precise specifications.

The model didn’t change. The instructions did.

## What a Specification Actually Is

Most developers think of a spec as documentation you write after the code exists, or a product requirements doc that a product manager creates for a human engineer. Neither of those framing is useful here.

For an AI agent, a specification is context engineering. It’s curating exactly the right information for the model to make good decisions at each step.

Think of it like briefing a new contractor. If you tell a contractor “build me a kitchen,” you’ll get a kitchen. But it won’t have the cabinet heights your partner needs, it’ll use the wrong materials for your climate, and the electrician will wire outlets where you wanted a window. The contractor isn’t incompetent. You just didn’t tell them anything useful.

The contractor analogy breaks down in one important way: a good human contractor will ask you questions. AI agents, by default, won’t. They’ll fill in every gap with a plausible-sounding assumption, and those assumptions compound across hundreds of decisions until the delivered code is technically functional and practically wrong.

Your job is to close those gaps before the agent starts.

## The Four Files That Change Everything

Spec-driven development isn’t a framework or a product. It’s a practice built around four plain-text files that you keep next to your code.

==`**spec.md**`== ==is what you're building.== ==`**AGENTS.md**`== ==is how you build it.== ==`**plan.md**`== ==is the approach for this specific feature.== ==`**tasks.md**`== ==is the ordered list of atomic steps.==

Each file solves a specific failure mode.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*M1sc8iTTnsvYiFanzucspw.jpeg)

Without a `spec.md`, the agent guesses at requirements. Without an `AGENTS.md`, it rediscovers your project structure from scratch every session. Without a `plan.md`, it jumps directly from requirement to code and makes architectural decisions you never approved. Without a `tasks.md`, it tries to do everything at once and produces untestable chunks of logic.

Four files. Each one dramatically narrows the surface area for hallucination.

## Writing a spec.md That Actually Works

The spec is not a PRD. It’s not a README. It’s an executable contract for a machine that reads it at the start of every feature session.

Six things need to be in it.

**A one-sentence mandate.** Not “build a payment system.” Something like: “Build a webhook handler that processes Stripe payment events, updates order status in PostgreSQL, and guarantees exactly-once processing under concurrent load.” Specific enough that if the agent delivers something that doesn’t match, you can point to the sentence and say “this is wrong.”

**Your technology stack with exact versions.** Not “use React.” Write “React 18.3 + TypeScript 5.4, Vite 5, Tailwind CSS 3.4.” Without this, the agent pulls from its training distribution, which means it might import deprecated APIs or mix patterns from incompatible library versions. This is a constant source of subtle bugs that look like model error but are actually omission error.

**Your data models.** Markdown tables for database schemas, fenced JSON or TypeScript blocks for API payloads. Agents fail most reliably at integration points, because they’re guessing at the shape of data crossing file or service boundaries. Pin the shapes down and that failure mode collapses.

**Non-goals.** Explicitly list what you’re not building. “Non-goals: OAuth integration, admin UI, email notifications, multi-currency support.” This isn’t obvious. Without it, the agent will “helpfully” scaffold things you didn’t ask for, and you’ll spend time pruning them out.

**Boundary conditions.** Immutable rules. “Never commit secrets. Never edit `node_modules/`. Never drop database tables without explicit approval." These aren't coding conventions, they're safety rails.

**An escalation protocol.** What should the agent do when it’s stuck? If you don’t specify, it generates speculative code. Speculative code is where bugs live. Write: “If you encounter a missing dependency, conflicting schema, or ambiguous requirement, stop. Describe the blocker and ask for clarification. Do not generate speculative code.”

That last one alone will save you hours.

## Your AGENTS.md Is a Second Brain for the Agent

The spec tells the agent what to build. The `AGENTS.md` tells it who it is and how it works.

It lives in your repository root and gets read at the start of every session. Think of it as institutional knowledge that the agent never loses.

The most valuable section is your dos and don’ts. Not high-level principles. Specific, nitpicky rules that encode decisions your team already made.

```c
## Do
- Use \`emotion css={{}}\` for all component styling
- Use MobX with \`useLocalStore\` for local component state
- Name test files \`*.test.tsx\` co-located with the component
```
```c
## Don't
- Never use inline \`style={}\` props
- Never use \`any\` as a TypeScript type
- Never import from barrel files — import from the source module directly
```

Every time the agent makes a mistake you have to correct, add a new rule. The file grows over time into a complete picture of your team’s opinions, and every future session benefits from it.

Two other things belong here. File-scoped commands so the agent runs `npx vitest run path/to/file.test.tsx` instead of `npm test` across your entire monorepo. And gold-standard reference files.

That second one is underrated. Point the agent at the files in your codebase that perfectly represent the pattern you want. “Copy patterns from `src/components/shared/Button.tsx` for components. Copy patterns from `src/server/api/orders.ts` for API handlers." A concrete example is worth more than a page of abstract rules.

## The Four-Phase Workflow

You’ve written your spec. Now the instinct is to hand it to the agent and say “build it.” Don’t.

**Phase 1: Clarify.** Before the agent writes a single line of code, prompt it to generate ten clarifying questions about the requirements. This sounds slow. It surfaces edge cases and missing requirements you didn’t know existed. It’s the cheapest bug fix you’ll ever do.

**Phase 2: Plan in read-only mode.** Have the agent research your codebase and produce a `plan.md` with target file paths, pseudocode, and dependency analysis. The agent cannot write implementation files during this phase. Read the plan. If the approach is wrong, regenerate. A plan takes minutes to fix. Code scattered across twenty files does not.

**Phase 3: Break it into tasks.** Decompose the plan into atomic, ordered steps in `tasks.md`. Each task should be small enough to implement and test in isolation. "Create `OrderWebhook` Prisma model with idempotency key" is a task. "Build the payment system" is not.

**Phase 4: Implement with you reviewing.** The agent executes tasks in sequence. You shift from programmer to reviewer, validating each change as it lands. This is intentional. Your job changes.

## The Red-Green-Refactor Lock

The last structural piece that makes this work in practice is test-driven development, and the key is enforcing the order.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ZeJeZK_FWovFGU1fEOlo1w.jpeg)

The agent writes failing tests first, based on the spec. Implementation files are off-limits at this stage. The tests must fail, which proves they’re asserting logic that doesn’t exist yet.

Then the agent writes only enough code to make the tests pass. Not the full feature. Not a clean implementation. Enough to go green.

Then it refactors under the safety net.

If you skip the enforcement, agents will write the implementation and the tests simultaneously, and the tests will inevitably pass because they were written to match the code rather than the spec. That’s not testing. That’s theater.

You can configure pre-commit hooks or filesystem rules to block implementation file writes until test files exist for the target module. This is worth doing.

## Keep the Spec Alive

One last thing that most people miss.

Your spec will drift from reality the moment implementation starts. The agent discovers a schema conflict. A dependency doesn’t support the version you specified. A business rule turns out to contradict another business rule.

When that happens, the agent needs to do two things: propose a spec update, and wait for your approval before proceeding. Once you approve, it writes the decision back into `spec.md`.

This is called backward propagation. Code-to-spec, not just spec-to-code. It’s what separates a one-time planning exercise from a production-grade practice. Your spec stays synchronized with your actual codebase, and every future session starts from truth instead of fiction.

## Where to Start Today

You don’t need to do all of this at once. The research is clear, but the practice has to be incremental or it won’t stick.

Pick your next feature. Write a `spec.md` for it using the six sections above. That's the whole starting point. Don't worry about `AGENTS.md` yet. Don't worry about the four-phase workflow.

Just write the spec. Use the mandate, the tech stack with versions, the non-goals, and the escalation protocol. That alone will change what you get back.

Then, after that session, take the mistakes the agent made and add them to your `AGENTS.md`. You'll build the institutional knowledge file from real failures rather than from guesses about what might go wrong.

The agents are capable. The specifications are the gap.

Close that gap and you’ll spend a lot less time cleaning up code that was plausible but wrong.

[![Kristopher Dunham](https://miro.medium.com/v2/resize:fill:60:60/1*PsZLmtO9Go4TeJeVRy5FSQ.jpeg)](https://medium.com/@creativeaininja?source=post_page---post_author_info--ae1622924cd6---------------------------------------)[7 following](https://medium.com/@creativeaininja/following?source=post_page---post_author_info--ae1622924cd6---------------------------------------)

Published author, developer, creative who builds worlds. [Fervorlife.com](http://fervorlife.com/). Join the fun at [CreativeAiDojo.com](http://creativeaidojo.com/) or [CreativeAi.Ninja](http://creativeai.ninja/)

## Responses (2)

Benedek Molnar

What are your thoughts?

```c
been using these agents in real repos and honestly the 4-file ritual is lipstick on a pig if your domain model and tests are trash
```

2

```c
This was incredibly useful. I’m shocked how well the results turned out from using this approach.
```

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--ae1622924cd6-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)