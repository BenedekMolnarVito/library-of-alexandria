---
title: "Agentic SaaS Playbook in 2026"
source: "https://www.agentnative.dev/agentic-saas"
author:
published:
created: 2026-04-18
description: "Production blueprint for architecting, shipping, and operating agentic SaaS."
tags:
  - "clippings"
---
Disclaimer

I'm not affiliated with any of the companies or products mentioned in this book. Information is accurate to the best of my knowledge as of February 2026, and please note that products and policies change.  
  
If you're looking for a specific playbook, additional research, or hands-on support building your product, you can write me at agentnativedev (at) gmail (dot) com.

For a long time, I was looking for serious resources on building agentic products, resources for people who actually want to ship products that work and loved by users. I paid for courses, books, communities, and programs hoping one of them would go deep enough.

A lot of courses, books or content show you a clever workflow, maybe a framework, and then quietly skip the hard parts: identity, permissions, billing, retries, monitoring, data ownership, and the boring realities of operating software for customers.

And that gap is where most of the real work lives.

Users will stress-test your edge cases, your costs, your uptime, and your trust boundaries, and they will hold you accountable.

That's the part I needed help with when I started.  
That's the part I couldn’t find.  
So that's the book I wrote.

If you follow the sections at your own pace and build alongside the repository, you'll understand what it takes to design, implement, and operate a SaaS product with agentic capabilities.

You'll build a Deep Research Agent that runs inside a real SaaS product: a public landing page, SEO optimized blog, a protected workspace, billing, recurring automation, and a backend that enforces identity and ownership, something you can actually put in front of customers.

![Deep Research Landing Page](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fdeep-research-landing.png&w=3840&q=75)

Deep Research Landing Page

![Deep Research User Console](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fdeep-research-user-console.png&w=3840&q=75)

Deep Research User Console

Throughout the book, I'll use *planes* as a practical way to reason about the system: UX, orchestration, runtime, memory, data, integrations, security, and observability.

Each plane is where specific failure modes show up, and where specific investments pay off.

Here's what you'll end up with:

- A public SaaS surface (landing, docs, pricing) that transitions cleanly into a protected workspace.
- A protected product area where users launch runs, approve steps, ask follow-ups, and download reports.
- A full run lifecycle: search → collect sources → summarize → approval gates → memory indexing → PDF report.
- Monitors that schedule recurring research runs like a lightweight operations layer.
- Stripe-based entitlement gating so runtime access is enforced server-side, not just in the UI.
- A mock vs live mode switch so you can demo and test fast without breaking production contracts.

This book, and the assets that come with it are for people building a product that works, that people trust and that lasts.

I hope you enjoy the freely available sections and deep dives. They're not *light* previews, they're genuinely substantial, and I put as much emphasis on them as I did on the gated sections. They're absolutely worth studying and practicing.

And if you're serious to take things a lot further, then I'd love for you to join **The Agent Foundry**. It's an exclusive membership for builders who want to ship products the right way, with depth and discipline. I hope to see you inside.

## 2\. Architectural Planes of Agentic SaaS

To keep things concrete, we'll use a mental model I'll call planes: layers of a deployable system that each carry their own failure modes, costs, and design constraints:

The planes below are a way to keep structure legible. Each plane is where different constraints dominate and different **build vs buy** decisions make sense.

- `UX` Where trust is won or lost, what users see, approve, and download.
- `Control` Deterministic execution substrate: routing, state, tool contracts, gates
- `Runtime` Execution environments, queues, workers, timeouts, and cost control.
- `Memory` What you store, how you index it, and how you ground Q&A.
- `Data` Persistence, schemas, ownership, and multi-tenant boundaries.
- `Integrations` Web search, scraping, tools, external APIs, and their drift over time.
- `Security` Identity, authorization, policy checks, input/output guardrails.
- `Observability` Logs, traces, metrics, evaluation, monitoring, debugging, cost attribution

?

Knowledge Check

#### Which plane most directly reduces the “articulation burden” of chat-only products?

## User Experience Plane (UI/UX)

Where trust is won or lost, what users see, approve, and download.

Most agentic products fail because the experience makes the smart thing hard to access, hard to trust, or hard to justify.

In practice, UX breakdowns very quickly compound.

Small friction points across onboarding, mental models, guardrails, and handoffs add up to a slow-motion collapse.

That's why the UI/UX plane is your strategy for adoption, cost control, and credibility.

SaaS framing in this blueprint

In this blueprint, we are building a **Deep Research Agent as a SaaS product**. That changes the engineering bar where each run is user-scoped, credit-gated, observable, and restart-safe.

We are designing a **deployable SaaS product** with a full user journey: acquisition, authentication, protected workspace, run lifecycle visibility, and billing transparency.

A good rule of thumb for 2026: start with the user, not the algorithm.

Before you choose model stacks or “agent frameworks,” look at how people do the job today:

- What are they trying to accomplish?
- What feels slow, risky, or annoying?
- Slow: too many steps
- Risky: easy to make mistakes
- Annoying: context switching
- Where do they already live (Slack, email, CRM, ticketing systems)?
- Start with the smallest change that helps
- Even if that change is non-AI

It's tempting to reach for the newest tech by default but most products don't need it.

And even when AI is involved, you should sell and design the product around user outcomes, not model magic. More often than you'd expect, a lightweight automation will solve the problem better (and cheaper) than wrapping everything in a heavy LLM call.

### Borrowed surfaces beat bespoke UIs early

In the earliest stages, frontend tax is real and building bespoke UIs can delay the launch by months.

So teams often meet users where they already work: Slack, Microsoft Teams, email, or the system-of-record (e.g., an ITSM tool, CRM, or ticketing platform). You get instant distribution, familiar interaction patterns, and you can iterate quickly.

Example: Atomicwork

A good example is Atomicwork's agentic service-management platform launched with Slack and Microsoft Teams integrations. Employees can interact through Slack while the service management layer and agentic workflows run behind the scenes.

![Agentic service-management platform](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fatomicwork.png&w=3840&q=75)

Agentic service-management platform

Source: [Atomicwork – Modern ITSM solution](https://www.atomicwork.com/features/modern-itsm-solution)

Example: GTM Buddy

Another example is GTM Buddy: agents meet end-users where they work by embedding into Salesforce, Gmail, Outlook, Slack, and Teams—so users don't have to toggle between tools.

![Agents meet end-users where they work](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fgtmbuddy.png&w=3840&q=75)

Agents meet end-users where they work

Source: [GTM Buddy](https://gtmbuddy.ai/)

This pattern is especially sensible if you're racing toward a funding milestone: you can prove value without building a UI fortress first.

How we applied this in our MVP

We intentionally shipped a hybrid UX from the start: strong public surface for positioning and education, plus a protected workspace for governed operations.

```
// public UX
/ -> landing
/blog -> thought leadership
/docs -> implementation orientation
/pricing -> conversion

// protected UX
/login -> auth funnel
/research (and /admin alias) -> deep research workspace
/billing -> subscription + credits visibility
```

UX trap

Chat is an amazing entry point but a weak information architecture. Users must (1) know what the system can do and (2) express it well. That “articulation burden” is where ROI quietly dies.

People either don't ask, ask the wrong thing, or don't trust what they get back.

Borrowed surfaces also come with a hidden invoice:

- You inherit the platform’s interaction model, which is great for quick intake but weak for complex work
- You inherit the platform’s constraints. Data retention rules, UI limitations, API policy changes.
- You risk becoming “a bot” instead of “a product.” Users don’t build trust in bots the way they build trust in tools.

Here are some design moves that can reduce early-stage failure without building a full UI:

- `Assist + handoff` Don't try to “replace experts.” Draft the response, propose next steps, show reasoning, ask for approval.
- `Make cost visible` Add friction where it matters (confirmations, approvals, scoped actions) and remove it where it doesn't (quick replies).
- `Micro-interactions` Buttons, forms, menus, and “suggested next steps” become lightweight IA inside chat for repeatable tasks.

A mature pattern is hybrid where you keep Slack/Teams as the fast first touchpoint, and provide a dedicated web/mobile experience as the trustworthy “control center” for governance, persistence, multi-step workflows, and differentiation.

### Beyond bots: dashboards, workflows, and trust for growth

Chat can handle intake but operations require structure.

Support workflows are the clearest example, e.g. Zendesk's Slack integration lets teams create tickets inside Slack via shortcuts/actions but resolution still lives inside the structured system behind it.

This is why, as startups grow and move into Series B, they often develop dedicated agent interfaces. The bottleneck shifts from “can we ship?” to “can users reliably get value every day?”

Once you're there, richer patterns become worth the effort:

- Multi-step workflows with checkpoints
- Persistent histories and task states.
- Approvals, audit trails, and governance
- Personalization and role-based views
- Multi-agent coordination (handoffs between agents and humans)

Implementation note

As you will later see, these patterns also appear in the product we are building

- Persistent histories: run list + events + report artifacts in /research.
- Governance: approval pause flow (waiting\_approval) + resume/reject actions.
- Observability UX: runtime inspector with task DAG, snapshots, and memory facts.
- Role workflows: datasets/methodologies/monitors side panels as structured operations.

Example: Relevance AI

Relevance AI is one example of the “agent OS” direction with dedicated surfaces plus integrations, positioning agents as managed workforce components, the team raised a US$24M Series-B round late 2024.

![AI agents operating system](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Frelevanceai.png&w=3840&q=75)

AI agents operating system

Source: [Relevance AI](https://relevanceai.com/)

You can also see more of predictive onboarding, chat-based dashboards, and voice assistants in areas such as fintech or healthcare. You can go much beyond simple Slack bots and build dashboards that display agent state, analytics, and contextually appropriate actions.

![Search + Analytics + Dashboards](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Ftableau.png&w=3840&q=75)

Search + Analytics + Dashboards

Source: [Tableau](https://www.tableau.com/blog/agentic-analytics-new-paradigm-for-business-intelligence)

Caveat: accuracy metrics don’t equal value

If UX causes unnecessary escalations, redundant work, or endless back-and-forth, the human cost swamps the automation benefit, like a fraud system that flags everyone and creates a manual-review backlog.  
  
The interface has to shape demand (good defaults, constrained choices, clear escalation paths), not just answer questions.  
  
Dedicated UI is control over:
- Persistence
- Governance
- Differentiation
- Mental model users learn

### Two UX practices that pay off

- `Storyboard first` Before you pixel-push, sketch the flow: who's the protagonist, what triggers the interaction, what success looks like, and where the agent must not operate autonomously. It's the fastest way to catch wrong use case problems early.
- `Agent narrative` Design the story users experience: what the agent can do, what it's doing now, what it needs from them, and what happens next. Without a narrative, even a capable agent feels random.

Platform dependency risk

A practical reason to invest in your own UI at Series-B is dependency risk. The more your product's core value depends on someone else's UI + data pipes, the more your roadmap inherits their constraints (policy changes, API limits, data-handling rules, UI affordances).

### Hybrid wins at Series-C and enterprise

By Series-C (and certainly in enterprise), the winning pattern is almost always hybrid:

- `Keep` Slack/Teams for speed, reach, and convenience
- `Add` A dedicated web/mobile experience for depth, governance, and differentiation

How this maps to our current SaaS UX architecture

- Fast door: public pages and login funnel reduce acquisition and onboarding friction.
- Control center: protected /research workspace with run launch, runtime visibility, and artifacts.
- Governance center: /billing page exposes subscription state, credits, and recent events.
- Route protection: middleware + backend auth keep private operations inaccessible to anonymous traffic.

Example: Moveworks

Moveworks is a well-known example of an agentic IT support surface that works through enterprise messaging tools like Microsoft Teams and Slack for convenience, while still supporting richer, structured experiences for ticketing, workflows, and analytics.

![Custom web and mobile dashboard for IT support tickets ](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fmoveworks.png&w=3840&q=75)

Custom web and mobile dashboard for IT support tickets

Source: [Moveworks](https://www.moveworks.com/)

Example: Intercom + Slack

Established SaaS products like Intercom also shows the same maturity curve. Intercom's support system, powered by its Fin AI agent, connects Slack channels so that support agents see tickets in both Intercom and Slack, with real‑time sync of statuses and conversation histories.

![Fin AI agent connects Slack channels](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Ffinagent.png&w=3840&q=75)

Fin AI agent connects Slack channels

Source: [Intercom — Connect your Slack channel](https://www.intercom.com/help/en/articles/11534476-connect-your-slack-channel)

### What changes in UX emphasis (late stage)

- `Expectations` Users need a simple, explicit contract, i.e. what the agent can do, what it can't, and what it will ask before acting.
- `Transparency` Show sources, assumptions, and the “because” behind recommendations to earn trust.
- `Error handling` Safe retries, graceful fallbacks, clear escalation, and “undo” matter more than cleverness.
- `Autonomy` Start with suggestions, then move to guarded execution, then expand autonomy as trust and reliability prove out.
- `Data restraint` Collect less by default, ask permission when you must and be explicit about retention and access. Users notice.

UX maturity curve (typical evolution)

1. Start with borrowed surfaces (Slack/Teams/CRM) to validate value quickly.
2. Add lightweight IA inside chat (structured actions, suggested flows, guardrails) to reduce articulation burden and misuse.
3. Build a dedicated agent hub for persistence, multi-step workflows, governance, and brand differentiation.
4. Land on a hybrid model where chat is the fast “front door,” and your UI is the trustworthy “control center.”

If you're building agentic SaaS, the key is not picking “Slack bot vs bespoke UI” as a permanent identity. It's recognizing where you are on the maturity spectrum, then designing the smallest UX system that makes:

- Value discoverable
- Outcomes trustworthy
- Human cost aligned with business benefit

### Developer experience is part of UI/UX

If you're building an agentic *platform* (not just an app) where developers consume your services, your “UI plane” includes developer-facing surfaces too:

- SDKs
- CLIs
- Self-service panels
- Workflows
- Admin controls
- Diagnostics
- Rollout tooling
- Support

This collection of deveoper surfaces make the system feel predictable, otherwise adoption dies when the platform behaves like a black box and you can't scale the support over time after initial roll-out.

You often optimize for four developer outcomes: **time-to-first-success** (onboarding), **time-to-confidence** (predictability), **time-to-debug** (observability), and **time-to-recover** (safe change + rollback). The companies below win because they compress those timelines aggressively.

#### DX patterns that correlate with adoption

- `Integration contract` Make the platform's behavior legible: inputs/outputs, tool scopes, permissioning, rate limits, cost signals, and failure modes. Developers ship faster when the “contract” is clear enough to reason about and test.
- `Traceability` Give developers run traces they can debug: tool calls, retrieved context, state transitions, approvals, retries, and where the agent asked for clarification. If developers can't explain an outcome, they won't trust it in production.
- `Safe sandboxes` Provide environments where teams can test with real-ish data without real-world blast radius: replay, simulation, dry-run modes, and one-click rollback. The goal is “learn fast” without “break prod.”
- `Opinionated primitives` Ship reusable UI + API building blocks for “agent status,” approvals, citations, human handoff, feedback, and undo—so every team doesn't reinvent unsafe patterns with slightly different failure modes.

These patterns reduce the cognitive load of shipping agentic behavior. The goal is to make the “right” path the easiest path, and make risky moves feel obviously risky *before* they hit production.

Let's have a look at a few examples.

Example: Vercel previews as the contract

Vercel turned deployments into a default workflow. Every branch gets a preview environment. That's a DX pattern agent platforms should steal. Make “safe testing” the path of least resistance, and tie it to the habits developers already have (Git → environment → feedback → merge).

![Vercel preview environment](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fvercel_preview.png&w=3840&q=75)

Vercel preview environment

Source: [Vercel Git integrations](https://vercel.com/docs/git)

This removes the hidden tax of “setting up a place to test.” Preview environments compress feedback loops and eliminate coordination overhead (no shared staging fights, fewer “works on my machine” debates). It also boosts developer happiness because progress becomes visible. URL you can share is instant social proof, and it aligns engineering with product/design review without extra ceremony.

In agentic platforms, previews matter even more because behavior is probabilistic. If every iteration requires a full production-like release, developers become conservative and slow. Previews let teams explore safely where they can tune prompts, adjust tool scopes, refine guardrails, and do it with realistic integration context.

Example: Supabase schema as source-of-truth

Supabase leans into Postgres as the contract where local dev workflows and migrations keep behavior consistent across environments, and generated types make mismatches show up early. You can similarly treat “what's allowed” as a first-class artifact.

![Supabase treats Postgres as the contract](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fsupabase_schema.png&w=3840&q=75)

Supabase treats Postgres as the contract

Source: [Supabase Local development](https://supabase.com/docs/guides/local-development/overview)

This effectively reduces onboarding friction. When the “contract” is your schema, the platform becomes teachable where new developers can infer behavior from types, tables, and migrations instead of reading Slack threads.

For agents, the schema analogy actually extends beyond data. You want “behavior schemas” too with tool input/output definitions, allowed action scopes, escalation rules, and approval boundaries. The more of that you can represent as structured artifacts (and validate in CI), the less your platform depends on hero engineers.

Example: AWS permissioning you can test

AWS ships an IAM policy simulator so teams can validate and troubleshoot authorization rules before rolling changes out.

![AWS IAM](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Faws_permission.png&w=3840&q=75)

AWS IAM

Source: [AWS IAM policy simulator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html)

Permissioning is where agentic platforms either become enterprise-grade or become a toy. Developers don't fear complexity, they fear invisible complexity. Testable permissions reduce anxiety because teams can answer “who can do what, under which conditions” without guessing.

This also sets up your traceability story. Once you have a clear contract and enforceable boundaries, the next productivity bottleneck is debugging: when something goes wrong, can a developer see exactly where the contract was violated (or where the world didn't match expectations)?

Example: Stripe Request logs as debugging UX

Stripe makes request logs a first-class developer surface. You can inspect what was sent, what was returned, and what failed. That's also how you should treat run traces.

![Stripe Request logs](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fstripe_request_logs.png&w=3840&q=75)

Stripe Request logs

Source: [Stripe Request logs](https://docs.stripe.com/development/dashboard/request-logs)

Logs reduce time-to-debug. More importantly, they reduce onboarding time because they teach developers how the platform behaves in the real world rather than idealized “happy path.” In agent platforms, logs should show not just errors, but also intent, e.g. tool calls attempted, inputs used, scopes applied, and what guardrail blocked an action.

Still, logs alone often answer “what happened,” not “why did it happen.” That's where traces and causal timelines become the difference between a confident developer and a frustrated one.

Example: Sentry traces + breadcrumbs for causality

Sentry's Trace View and breadcrumbs are designed to answer the only question that matters during incidents: “what happened, in what order, and why?” You need the same ergonomics, e.g. timelines of tool calls, state changes, user approvals, and failures so teams can debug behavior.

![Sentry traces](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fsentry_traces.png&w=3840&q=75)

Sentry traces

Sources: [Sentry Trace View](https://docs.sentry.io/concepts/key-terms/tracing/trace-view/)

This is also where developer happiness shows up as a measurable operational outcome: lower MTTR, fewer escalations, and less “psychological load” during incidents. A good trace UI turns debugging into navigation.

Developers stop asking “is the model broken?” and start answering “the tool call failed because scope X blocked it,” or “retrieval returned stale context,” or “approval step was skipped due to misconfiguration.”

Once you can explain behavior, the next constraint becomes iteration speed. The best debugging tools in the world won't help if every fix requires a risky production deploy. That's why developer-first companies obsess over safe, realistic sandboxes.

Example: Cloudflare preview URLs + local dev loops

Cloudflare Workers supports preview URLs and local dev workflows so developers can iterate quickly without pushing risky changes straight to production. You should provide the teams a tight feedback loop and safe promotion paths.

![Cloudflare Workers supports preview URLs](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fcloudflare_preview_urls.png&w=3840&q=75)

Cloudflare Workers supports preview URLs

Sources: [Cloudflare Previews](https://developers.cloudflare.com/workers/configuration/previews/)

Sandboxes increase velocity because they turn experimentation into a default behavior. When developers can replay inputs, simulate tool failures, and test different guardrails quickly, they converge on reliable designs faster and ship with less fear.

But even with great previews, eventually you have to ship to production. That's where rollout UX matters, you need confidence-building mechanisms that let teams deploy agent behavior changes without betting the company on a single release.

Example: AWS Lambda canary rollouts with weighted aliases

AWS Lambda weighted aliases allow gradual traffic shifting to new versions with quick rollback. This is the rollout UX agent platforms should standardize: promote behavior changes through controlled exposure, not big-bang releases.

![AWS Lambda rollout](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Faws_lambda_rollout.png&w=3840&q=75)

AWS Lambda rollout

Source: [AWS Lambda alias routing](https://docs.aws.amazon.com/lambda/latest/dg/configuring-alias-routing.html)

Canary rollouts reduce change failure rate and that translates directly into developer trust. Teams become willing to ship improvements because the blast radius is explicit and controllable. In agent platforms, this is especially important because behavior changes can alter cost, latency, and user trust in one move. Controlled exposure makes those tradeoffs observable before they become widespread.

Still, version-based rollout is only half the story. The other half is feature-level control, the ability to turn behaviors on/off, segment users, and iterate safely without coupling every tweak to a deployment artifact.

Example: LaunchDarkly progressive delivery as a default habit

LaunchDarkly's percentage rollouts and staged releases as normal operating procedure. For agent systems, progressive delivery is how you prevent a new planner from doubling your escalations overnight.

![LaunchDarkly percentage rollouts](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Flaunchdarkly_progressive_delivery.png&w=3840&q=75)

LaunchDarkly percentage rollouts

Source: [LaunchDarkly Percentage rollouts](https://launchdarkly.com/docs/home/releases/percentage-rollouts)

When feature-level controls exist, teams can test hypotheses (“does this guardrail reduce escalation?”). It also improves developer happiness because the platform supports reversible decisions, you can experiment without fear of being trapped by a release.

The missing piece for many agent platforms is deterministic testing. Progressive rollouts help in production, but you still want a way to validate integration flows repeatedly without triggering real-world side effects.

Example: Twilio test credentials for deterministic outcomes

Twilio's test credentials let teams exercise integration flows without triggering real-world side effects. That's the sandbox pattern agent platforms should copy, i.e. preserve the shape of production behavior while making consequences safe and repeatable.

![Twilio test credentials](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Ftwilio_test_credentials.png&w=3840&q=75)

Twilio test credentials

Source: [Twilio Test credentials](https://www.twilio.com/docs/iam/test-credentials)

Determinism reduces onboarding friction because it makes learning reproducible, new developers can run the same scenario and see the same outcomes. It also reduces operational risk because teams can build strong regression tests around “known bad” cases, exactly what agent platforms need when behavior depends on tool availability, permissions, or shifting context.

Once you can test safely, you can go further, make “preview before action” a platform primitive. This is how you prevent costly or irreversible automation mistakes, and it's a huge trust builder for both developers and operators.

Example: Terraform dry-run diffs as a primitive

Terraform's `plan` makes “show me the diff before you apply it” the standard workflow. For agent platforms, this maps to previews of actions: what will change, what tools will run, what data will be touched, and what the rollback path is.

![Terraform dry-run diffs](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fterraform_dry_run_diffs.png&w=3840&q=75)

Terraform dry-run diffs

Source: [Terraform plan](https://developer.hashicorp.com/terraform/cli/commands/plan)

Previews increase developer confidence because they turn execution into an informed decision. In agent systems, “plan mode” is how you make autonomy legible. You can show the proposed tool calls, what data will be written, what permissions are required, and which steps require approval. This reduces incident volume and makes it easier for developers to defend the platform internally.

Now zoom out and notice that all of the above assumes developers can get started quickly. But many platforms lose adoption before they even reach debugging or rollout, because initial setup feels like homework. Developer-first companies treat onboarding as a first-class performance problem.

This is velocity through momentum. When teams can go from “new project” to “working demo” quickly, they develop attachment to the platform. It increases developer happiness because it respects their time and it increases adoption because stakeholders see results early. For agent platforms, a prebuilt scaffold might include tracing enabled, safe sandboxes configured, starter guardrails, and a “hello world” tool call that demonstrates approvals + undo.

Finally, none of this matters if platform evolution is painful. Developers stick with platforms that let them upgrade without dread and that requires versioning discipline. You want change to feel intentional, observable, and reversible.

Example: Stripe — versioning to prevent breaking integrators

Stripe's webhook versioning guidance is a model for platform evolution without chaos. Agent platforms need the same discipline, i.e. behavior changes should be versioned, observable, and migratable so adopters move on their schedule, not yours.

![Stripe webhook versioning](https://www.agentnative.dev/_next/image?url=%2Febook%2Fagentic-saas%2Fstripe_versioning.png&w=3840&q=75)

Stripe webhook versioning

Source: [Stripe Webhook versioning](https://docs.stripe.com/webhooks/versioning)

Developer trust is earned through **predictable change**. When platform behavior is versioned and observable, upgrades stop being high-stakes events and become routine maintenance. That's how you preserve velocity over time and it's a major driver of developer satisfaction with less surprises, less firefighting and more forward progress.

#### DX maturity curve (how platforms usually evolve)

What “good DX” looks like as you scale

1. Start with a minimal contract (SDK + clear limits + observability) so early adopters can ship without guessing.
2. Add first-class traces and safe sandboxes so debugging and iteration become routine, not heroic.
3. Introduce progressive delivery (canaries, rollbacks, versioning) so behavior changes don't become support incidents.
4. Standardize primitives (approvals, citations, handoff, undo) so every integration doesn't reinvent unsafe UX.

The point isn't to copy these companies verbatim. It's to copy their underlying move. Treat developer workflows as product UX. When developers can predict, test, observe, and recover from agent behavior changes, they ship the platform and they keep it shipped.

This should give you enough perspective about approaching UI/UX for your own solution, platform or product. In the next section, we will dive deep into control plane.

The control plane is the nerve center of an agentic SaaS system. It does not run agent logic, that belongs to the runtime plane. Instead, it decides *whether* an agent step should execute, *which* tools an agent can reach, *how much* it is allowed to spend, and *what happens* when something goes wrong.

If the runtime plane is the engine, the control plane is the cockpit: instrument panel, throttle levers, and circuit breakers.

Agent control plane is an emerging architectural plane and it is distinct from the build plane (frameworks, models) and the orchestration plane (workflow engines) whose job is to provide unified visibility, governance, and management across a heterogeneous agent estate. Enterprises already rely on out-of-band control planes in other domains (Airbnb's experimentation guardrails, JPMorgan's model risk governance) and that agents demand similar independent oversight.

Over the next 12-24 months, this will solidify into a distinct market with dedicated vendors.

SaaS framing: the control plane is your trust contract

In a multi-tenant SaaS product, the control plane is what lets you promise customers: "Your agent will never exceed your token budget, will never call an unapproved tool, and every action is logged for audit."

This blueprint implements a control plane that separates policy from execution. Policies are declared as data (YAML/Cedar), evaluated at the middleware layer before every tool call, and enforced deterministically.

The same pattern powers AWS Bedrock AgentCore's governance layer, which enforces hard constraints at the infrastructure level rather than relying on prompt-level instructions.

### Plane separation: why the control plane must live outside the runtime

A recurring architectural mistake is embedding governance logic inside agent prompts or runtime code. "Don't call the delete API" in a system prompt is a suggestion that can be overridden by jailbreaks, prompt injections, or model updates.

Real governance must sit in a separate process that intercepts agent actions *before* they execute and applies deterministic rules the agent cannot bypass.

This mirrors how service meshes (Istio, Envoy) enforce network policies without modifying application code, and how Kubernetes admission controllers validate resources before the API server persists them.

The Deep Research blueprint organizes governance across four planes. Each has a distinct responsibility and a separate failure domain:

| Plane | Responsibility | Industry analogues | Blueprint implementation |
| --- | --- | --- | --- |
| Control | Policy, identity, tool registry, budget enforcement, progressive delivery | K8s API server, Istio control plane, AWS Bedrock AgentCore governance layer | Policy middleware, tool registry YAML, budget tracker, feature flags |
| Runtime | Execute agent steps: LLM calls, tool invocations, code sandboxes | Lambda, Temporal, E2B, Modal | Workload lanes, durable workers, sandbox broker |
| Memory | Persist context across sessions: conversation history, knowledge, embeddings | Mem0, Zep, LangGraph checkpointing | Session store, vector DB, episodic memory |
| Data | Source-of-truth storage: documents, structured data, indexes | PostgreSQL, S3, Pinecone, Elasticsearch | Document pipeline, search index, metadata DB |

control\_plane/middleware.py - policy enforcement as middleware

python

```
class ControlPlaneMiddleware:
"""
Sits between the agent loop and the runtime.
Every tool call passes through here BEFORE execution.
The agent cannot bypass this—it is architecturally impossible.
"""

def __init__(self, policy_engine, tool_registry, budget_tracker, audit_log):
    self.policy_engine = policy_engine      # CEDAR / OPA / YAML rules
    self.tool_registry = tool_registry      # allowed tools + schemas
    self.budget_tracker = budget_tracker     # token / dollar limits
    self.audit_log = audit_log              # immutable event stream

async def evaluate(self, agent_id: str, action: ToolCallRequest) -> PolicyDecision:
    """
    Called before every tool invocation.
    Returns ALLOW, DENY, or REQUIRE_APPROVAL.
    """
    # 1. Is this tool registered and enabled for this tenant?
    tool = self.tool_registry.resolve(action.tool_name)
    if not tool or not tool.enabled:
        return PolicyDecision.deny(f"Tool '{action.tool_name}' not in registry")

    # 2. Does the agent's identity have permission for this action?
    authz = await self.policy_engine.evaluate(
        principal=agent_id,
        action=action.tool_name,
        resource=action.resource,
        context=action.context,
    )
    if authz.decision == "DENY":
        return PolicyDecision.deny(authz.reason)

    # 3. Would this call exceed the tenant's budget?
    budget_check = self.budget_tracker.check(
        tenant_id=action.tenant_id,
        estimated_cost=action.estimated_tokens,
    )
    if budget_check.exceeded:
        return PolicyDecision.deny(f"Budget exhausted: {budget_check.remaining} tokens left")

    # 4. Does this action require human approval?
    if authz.decision == "REQUIRE_APPROVAL":
        return PolicyDecision.require_approval(authz.reason)

    # 5. Log and allow
    await self.audit_log.record(agent_id, action, "ALLOWED")
    return PolicyDecision.allow()
```

System prompts are suggestions to a probabilistic model. They can be overridden by prompt injection, ignored during multi-step reasoning, or invalidated when you swap models. A middleware-based control plane is deterministic: it runs as code that the agent cannot influence.

AWS Bedrock AgentCore makes this explicit, policies like "this agent cannot delete objects in the production S3 bucket" are enforced at the infrastructure layer, not embedded in prompts. For auditors, this is the difference between "we hope the AI behaves" and "we can prove it can't misbehave."

### Tool registry and interoperability protocols

A tool registry is the control plane's catalog of every capability an agent can invoke. Without one, agents discover tools via prompt context which is fragile, unversioned, and impossible to audit. With a registry, you get versioned schemas, per-tenant enablement, deprecation policies, and a single source of truth for what your agents can do.

The interoperability landscape has converged rapidly. The Model Context Protocol (MCP), originally open-sourced by Anthropic in November 2024, was donated to the Linux Foundation's Agentic AI Foundation (AAIF) in December 2025, co-founded by Anthropic, Block, and OpenAI with support from Google, Microsoft, AWS, and Cloudflare. MCP now has over 10,000 active public servers, 97M+ monthly SDK downloads, and has been adopted by ChatGPT, Cursor, Gemini, Microsoft Copilot, and VS Code.

Meanwhile, Google's Agent-to-Agent (A2A) protocol is donated to the Linux Foundation's AAIF as well, enabling cross-vendor agent collaboration through Agent Cards (JSON metadata), skill declarations, and task lifecycle management. The phased adoption roadmap the industry is converging on is to start with MCP for tool integration, layer in Agent Communication Protocol (ACP) for structured multi-agent messaging, then add A2A for cross-organization agent discovery and collaboration.

| Protocol | Scope | Key primitives | Governed by | Status (early 2026) |
| --- | --- | --- | --- | --- |
| MCP | Agent ↔ Tool connectivity | Tools, resources, prompts, sampling, registry | Linux Foundation (AAIF) | 10K+ servers, 97M+ monthly downloads, GA |
| A2A | Agent ↔ Agent collaboration | Agent Cards, skills, task lifecycle, streaming | Linux Foundation (AAIF) | v0.2.5, 50+ partners, growing adoption |
| ACP | Multi-agent messaging | Structured envelopes, content negotiation | IBM / Community | Early specification stage |
| ANP | Open-internet agent networking | DID identity, capability negotiation | Community | Experimental / research stage |

```
# Every tool an agent can call is declared here.
  # The control plane middleware resolves tools against this registry
  # before allowing execution. Unregistered tools are blocked.

  tools:
    web_search:
      version: "2.1.0"
      protocol: mcp # MCP server endpoint
      endpoint: "mcp://tools.internal/web-search"
      schema:
        input:
          query: { type: string, maxLength: 2000 }
          max_results: { type: integer, default: 10, max: 50 }
        output:
          results: { type: array, items: { type: object } }
      policies:
        - require_auth: true
        - rate_limit: { rpm: 60, per: tenant }
        - cost_attribution: { unit: "search_call", cost: 0.002 }
      enabled_tiers: [pro, enterprise]
      deprecation: null

    document_write:
      version: "1.3.0"
      protocol: rest
      endpoint: "https://api.internal/documents"
      schema:
        input:
          document_id: { type: string }
          content: { type: string, maxLength: 50000 }
          action: { type: string, enum: [create, update, delete] }
      policies:
        - require_auth: true
        - approval_required:
            actions: [delete] # Deletes need human approval
            approvers: [tenant_admin]
        - rate_limit: { rpm: 30, per: tenant }
      enabled_tiers: [enterprise]

    code_execution:
      version: "1.0.0"
      protocol: mcp
      endpoint: "mcp://sandbox.internal/execute"
      schema:
        input:
          language: { type: string, enum: [python, javascript, bash] }
          code: { type: string, maxLength: 10000 }
          timeout_ms: { type: integer, default: 30000, max: 300000 }
      policies:
        - require_auth: true
        - sandbox_required: true     # Must run in isolated VM
        - network_policy: deny_all   # No outbound network by default
        - cost_attribution: { unit: "sandbox_minute", cost: 0.01 }
      enabled_tiers: [pro, enterprise]
```

MCP as your tool integration backbone

If you're starting a new agentic SaaS in 2026, default to MCP for all tool integrations. The protocol gives you a universal schema for tool discovery and invocation, a growing registry of pre-built servers (75+ in Claude's directory alone), and SDK support in every major language.

Your tool registry becomes a thin layer on top that adds tenant-specific policies, cost attribution, and enablement flags.

For multi-agent collaboration across organizational boundaries, expose your agents via A2A Agent Cards so external agents can discover capabilities through a standard JSON manifest.

### Policy engines and runtime guardrails

Policy enforcement for agents has two layers: **authorization policies** that determine what an agent is allowed to do (which tools, which resources, which actions), and **content guardrails** that validate what goes into and comes out of the LLM (prompt injection detection, PII filtering, topic restrictions). The control plane must handle both, and they operate at different points in the request lifecycle.

For authorization, the industry is converging on Cedar, the open-source policy language developed by AWS and used in Amazon Verified Permissions. Cedar is 42-60x faster than OPA's Rego, uses explicit permit/forbid statements that are human-readable and formally verifiable, and evaluates each policy independently, making it natural for agent-level authorization.

Cedar policies are standalone authorization decisions, i.e. they either match the request (principal, action, resource, and all conditions) or they don't apply. This determinism is what agent governance requires.

For content guardrails, every major platform now offers both LLM-based and rule-based approaches. OpenAI's Agents SDK provides input guardrails (run before the agent processes input), output guardrails (run before the response is returned), and tool guardrails (validate tool calls before and after execution), each triggering a "tripwire" exception that halts execution on violation.

AWS Bedrock Guardrails offers configurable policies for content filtering, denied topics, PII redaction, and prompt attack detection, all evaluable via a standalone API that works even with non-Bedrock models. California's 2025 legislative push (SB 243, AB 489) is further accelerating enterprise demand for runtime guardrails that can demonstrate compliance.

Authorization policy patterns for agents

- Role-based (RBAC): Agent inherits permissions from its assigned role. Simple but coarse. "Research agents can read documents and admin agents can delete them."
- Attribute-based (ABAC): Decisions use agent attributes, resource metadata, and environmental context (time, IP, tenant tier). "This agent can access financial data only during business hours and only for its own tenant."
- Relationship-based (ReBAC): Permissions follow entity relationships. "This agent can edit the document because it was created by the same team." Cedar excels here with first-class entity relationships via the 'in' operator.
- Capability-based: Agent receives scoped, time-limited capability tokens. "This agent can call the payment API exactly once, within the next 5 minutes, for up to $100."

control\_plane/policies/agent\_authz.cedar — Cedar policies for agent actions

cedar

```
// --- Research agents: read-only access to documents and search ---
  permit (
      principal in AgentRole::"research",
      action in [Action::"read", Action::"search"],
      resource is Document
  );

  // --- No agent can delete production data without admin approval ---
  forbid (
      principal,
      action == Action::"delete",
      resource
  ) when {
      resource.environment == "production"
  } unless {
      principal in AgentRole::"admin" &&
      context.has_human_approval == true
  };

  // --- Enforce tenant isolation: agents can only access their own tenant's data ---
  permit (
      principal,
      action,
      resource is TenantResource
  ) when {
      resource.tenant_id == principal.tenant_id
  };

  // --- Time-boxed access: financial tools only during business hours ---
  permit (
      principal,
      action in [Action::"read_financials", Action::"generate_report"],
      resource is FinancialData
  ) when {
      context.current_hour >= 9 &&
      context.current_hour <= 17 &&
      context.day_of_week in ["Mon", "Tue", "Wed", "Thu", "Fri"]
  };

  // --- Budget-aware policy: block high-cost tools when budget is low ---
  forbid (
      principal,
      action,
      resource is ExpensiveTool
  ) when {
      context.budget_remaining_pct < 10
  };
```

```
from dataclasses import dataclass
  from enum import Enum
  import re

  class GuardrailVerdict(Enum):
      PASS = "pass"
      BLOCK = "block"
      WARN = "warn"

  @dataclass
  class GuardrailResult:
      verdict: GuardrailVerdict
      guardrail_name: str
      reason: str | None = None

  class GuardrailPipeline:
      """
      Runs guardrails in order. Rule-based checks first (fast, cheap),
      then LLM-based checks only if rule-based pass (slow, expensive).

      Pattern from OpenAI Agents SDK: input guardrails → agent → output guardrails.
      Each guardrail can trigger a "tripwire" that halts execution immediately.
      """

      def __init__(self, input_guardrails: list, output_guardrails: list):
          self.input_guardrails = input_guardrails
          self.output_guardrails = output_guardrails

      async def check_input(self, user_input: str, context: dict) -> GuardrailResult:
          for guardrail in self.input_guardrails:
              result = await guardrail.evaluate(user_input, context)
              if result.verdict == GuardrailVerdict.BLOCK:
                  return result  # Tripwire: halt immediately
          return GuardrailResult(verdict=GuardrailVerdict.PASS, guardrail_name="all_input")

      async def check_output(self, agent_output: str, context: dict) -> GuardrailResult:
          for guardrail in self.output_guardrails:
              result = await guardrail.evaluate(agent_output, context)
              if result.verdict == GuardrailVerdict.BLOCK:
                  return result
          return GuardrailResult(verdict=GuardrailVerdict.PASS, guardrail_name="all_output")

  # --- Rule-based guardrails (fast, no LLM cost) ---

  class PromptInjectionGuardrail:
      """Detect common jailbreak/injection patterns via regex."""

      PATTERNS = [
          r"ignores+(previous|all)s+instructions",
          r"yous+ares+nows+a",
          r"forgets+everythings+(above|before)",
          r"developers+mode",
          r"overrides+safety",
          r"disregards+(guidelines|rules|instructions)",
      ]

      async def evaluate(self, text: str, context: dict) -> GuardrailResult:
          text_lower = text.lower()
          for pattern in self.PATTERNS:
              if re.search(pattern, text_lower):
                  return GuardrailResult(
                      verdict=GuardrailVerdict.BLOCK,
                      guardrail_name="prompt_injection",
                      reason=f"Blocked: injection pattern detected",
                  )
          return GuardrailResult(verdict=GuardrailVerdict.PASS, guardrail_name="prompt_injection")

  class PIIGuardrail:
      """Block outputs containing PII patterns (SSN, credit cards, etc.)."""

      PII_PATTERNS = {
          "ssn": r"d{3}-d{2}-d{4}",
          "credit_card": r"d{4}[s-]?d{4}[s-]?d{4}[s-]?d{4}",
          "email": r"[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+.[A-Z|a-z]{2,}",
      }

      async def evaluate(self, text: str, context: dict) -> GuardrailResult:
          for pii_type, pattern in self.PII_PATTERNS.items():
              if re.search(pattern, text):
                  return GuardrailResult(
                      verdict=GuardrailVerdict.BLOCK,
                      guardrail_name="pii_filter",
                      reason=f"Blocked: {pii_type} detected in output",
                  )
          return GuardrailResult(verdict=GuardrailVerdict.PASS, guardrail_name="pii_filter")

  # --- LLM-based guardrails (slower, use for nuanced checks) ---

  class TopicGuardrail:
      """Use a fast/cheap model to classify whether input is on-topic."""

      async def evaluate(self, text: str, context: dict) -> GuardrailResult:
          classification = await classify_topic(
              text=text,
              allowed_topics=context.get("allowed_topics", []),
              model="gpt-4o-mini",  # Fast, cheap model for guardrail
          )
          if classification.is_off_topic:
              return GuardrailResult(
                  verdict=GuardrailVerdict.BLOCK,
                  guardrail_name="topic_filter",
                  reason=classification.reasoning,
              )
          return GuardrailResult(verdict=GuardrailVerdict.PASS, guardrail_name="topic_filter")

  # --- Assemble the pipeline ---

  guardrail_pipeline = GuardrailPipeline(
      input_guardrails=[
          PromptInjectionGuardrail(),  # Fast regex check first
          TopicGuardrail(),            # LLM check only if regex passes
      ],
      output_guardrails=[
          PIIGuardrail(),              # Block PII in agent responses
      ],
  )
```

Running an LLM guardrail on every input doubles your inference cost. The pattern above uses fast regex checks first (microseconds, zero cost) and only invokes the LLM classifier when the cheap checks pass. For high-volume SaaS, this layered approach can reduce guardrail cost by 80%+ while maintaining safety.

### Agent identity, authentication, and zero-trust

When an agent calls an API, who is making the request? The user who initiated the session? The agent itself? The SaaS platform? In traditional software, identity is straightforward, user authenticates and their token carries their permissions. With agents, there is a delegation chain where user delegates to the agent, which delegates to tools, which may delegate to other agents.

Each hop needs its own identity and scoped permissions.

The industry is converging on OAuth 2.0 with RFC 8693 token exchange for this delegation chain. The pattern is when a user authenticates to your SaaS, the platform mints a delegation token (JWT with an `act` claim) that says "Agent X is acting on behalf of User Y, scoped to these permissions, valid for this duration."

The MCP specification adopted OAuth 2.1 as its authentication standard. Microsoft Entra's Agent ID uses the On-Behalf-Of (OBO) flow for exactly this pattern. Auth0's Token Vault stores downstream service credentials so agents can act on behalf of users without ever seeing the raw tokens.

For machine-to-machine identity between agents and services, SPIFFE (Secure Production Identity Framework for Everyone) provides workload identity without static secrets. Each agent process gets a cryptographic identity (SPIFFE ID) tied to its workload attestation, i.e. not a long-lived API key that can be stolen. Combined with short-lived certificates (mTLS), this gives you zero-trust identity for every agent in your fleet.

| Identity layer | Pattern | Key technology | What it secures |
| --- | --- | --- | --- |
| User → Agent delegation | OAuth 2.0 + RFC 8693 token exchange | JWT with `act` claim, MCP OAuth 2.1 | User's permissions flow to agent with reduced scope |
| Agent → Tool invocation | Scoped capability tokens | Auth0 Token Vault, short-lived JWTs | Agent can only call approved tools with bounded permissions |
| Agent → Agent collaboration | Workload identity + mTLS | SPIFFE, Entra Agent ID OBO | Agents authenticate to each other without shared secrets |
| Tenant isolation | Token-embedded tenant claims | Cedar policies + JWT tenant\_id | Agent cannot escape its tenant boundary-enforced at policy layer |

control\_plane/identity.py — delegation token and scoped credentials

python

```
import jwt
  import time
  from dataclasses import dataclass

  @dataclass
  class AgentIdentity:
      agent_id: str
      tenant_id: str
      user_id: str          # The human who initiated this session
      scopes: list[str]     # Reduced permission set for this agent
      expires_at: int       # Unix timestamp

  def mint_delegation_token(
      user_token: str,
      agent_id: str,
      requested_scopes: list[str],
      ttl_seconds: int = 3600,
  ) -> str:
      """
      RFC 8693 token exchange: downscope the user's token for agent use.
      The agent gets a JWT that carries both its own identity and the
      delegating user's identity (via the 'act' claim).
      """
      user_claims = jwt.decode(user_token, options={"verify_signature": True}, ...)

      # Intersect requested scopes with user's actual permissions
      allowed_scopes = set(requested_scopes) & set(user_claims.get("scopes", []))

      delegation_claims = {
          "sub": agent_id,
          "tenant_id": user_claims["tenant_id"],
          "act": {
              "sub": user_claims["sub"],     # Original user
              "iss": user_claims["iss"],
          },
          "scopes": list(allowed_scopes),    # Never more than user has
          "iat": int(time.time()),
          "exp": int(time.time()) + ttl_seconds,
          "agent_session": True,
      }
      return jwt.encode(delegation_claims, SIGNING_KEY, algorithm="ES256")

  class ScopedCredentialStore:
      """
      Stores downstream service credentials scoped to agent sessions.
      Similar to Auth0 Token Vault: agents never see raw credentials.
      They get a reference ID, and the control plane injects the actual
      credential at tool invocation time.
      """

      async def get_credential(
          self,
          agent_identity: AgentIdentity,
          service: str,
      ) -> str | None:
          # Verify agent is authorized for this service
          if service not in self._service_allowlist(agent_identity.scopes):
              raise PermissionError(f"Agent {agent_identity.agent_id} not authorized for {service}")

          # Return short-lived, scoped credential
          return await self._vault.issue_scoped_token(
              service=service,
              tenant_id=agent_identity.tenant_id,
              ttl=300,  # 5 minutes max
          )
```

Agent identity checklist

0/6 complete

### Durable orchestration and human-in-the-loop

Durable execution crossed into the early majority in 2025. AWS released Durable Functions, Cloudflare shipped Workflows GA, and Vercel launched its Workflow DevKit, all driven primarily by AI agent infrastructure needs. The reason is that AI agents introduce multiple compounding failure points (orchestration, probabilistic LLM behavior, tool calling, human-in-the-loop waits) that traditional retry logic cannot handle.

If you have five steps at 99% reliability each, overall success drops to 95%. At ten steps, 90%. Real-world agents often involve dozens.

Durable execution provides three critical capabilities for the control plane: **automatic state persistence** (step results are checkpointed, so a failed workflow resumes from the last successful step instead of re-running expensive LLM calls), **exactly-once semantics** (tool calls with side effects don't duplicate on retry), and **suspend/resume primitives** (workflows can pause for hours or days awaiting human approval without consuming compute).

The market offers two architectural styles: **centralized orchestration** (Temporal, Inngest) where a coordinator manages the workflow DAG, and **event-driven choreography** (Inngest events, Akka actors) where agents respond to events asynchronously. For most agentic SaaS, start with centralized orchestration for predictable multi-step workflows, then add event-driven patterns for inter-agent communication.

control\_plane/orchestration.ts — durable workflow with human-in-the-loop

typescript

```
import { inngest } from "./client";

  // Durable workflow: every step.run() is checkpointed.
  // If the function crashes, it resumes from the last successful step.
  // LLM calls are NOT re-executed—their results are cached.

  export const researchWorkflow = inngest.createFunction(
    { id: "deep-research", retries: 3 },
    { event: "research/started" },
    async ({ event, step }) => {

      // Step 1: Plan the research (LLM call — result is cached on retry)
      const plan = await step.run("plan-research", async () => {
        return await llm.chat({
          model: "claude-sonnet-4-6-20250514",
          messages: [{ role: "user", content: event.data.query }],
          system: "Create a research plan with 3-5 search queries.",
        });
      });

      // Step 2: Execute searches in parallel (each individually checkpointed)
      const searches = await Promise.all(
        plan.queries.map((query, i) =>
          step.run(\`search-${i}\`, async () => {
            return await toolRegistry.invoke("web_search", {
              query,
              max_results: 10,
            });
          })
        )
      );

      // Step 3: Synthesize findings (another cached LLM call)
      const draft = await step.run("synthesize", async () => {
        return await llm.chat({
          model: "claude-sonnet-4-6-20250514",
          messages: [{ role: "user", content: formatFindings(searches) }],
          system: "Synthesize these search results into a comprehensive report.",
        });
      });

      // Step 4: HUMAN-IN-THE-LOOP — workflow suspends here.
      // No compute consumed while waiting. State persists across deployments.
      // The user can approve in seconds, hours, or days.
      const approval = await step.waitForEvent("await-approval", {
        event: "research/approved",
        match: "data.workflow_id",
        timeout: "7d",  // Auto-cancel if no response in 7 days
      });

      if (!approval || approval.data.decision === "reject") {
        await step.run("notify-rejection", async () => {
          await notify(event.data.user_id, "Research report was not approved.");
        });
        return { status: "rejected" };
      }

      // Step 5: Publish approved report
      const published = await step.run("publish", async () => {
        return await toolRegistry.invoke("document_write", {
          document_id: event.data.document_id,
          content: draft.report,
          action: "create",
        });
      });

      return { status: "published", document_id: published.id };
    }
  );
```

LLM calls are expensive. A research workflow might invoke Claude or GPT-4 five times at $0.01-$0.10 per call. Without durable execution, a failure at step 4 means re-running steps 1-3 and re-paying for those tokens. Durable execution caches step results, you pay for each LLM call exactly once, even across retries. For a SaaS running thousands of agent workflows daily, this can cut inference costs by 30-50%. Durable execution's caching behavior means you pay for each LLM call exactly once.

### Observability, tracing, and evaluation

Agent observability is not application monitoring. Traditional APM tracks request latency and error rates. Agent observability must trace multi-step reasoning chains, attribute costs per tool call, evaluate output quality over time, and surface *why* an agent made a decision—not just whether it succeeded. The industry is converging on OpenTelemetry (OTel) as the standard for collecting agent telemetry, with the GenAI Special Interest Group actively defining semantic conventions for tasks, actions, agents, teams, artifacts, and memory.

The observability landscape in early 2026 has stratified into tiers. Open-source Langfuse and Arize Phoenix offer vendor-neutral, OTel-native tracing with deep agent support. Langfuse handles tens of thousands of events per minute and natively supports OpenAI Agents SDK, LangGraph, Pydantic AI, CrewAI, smolagents, and Strands Agents. Arize AX provides session-level agent evaluation with tool-calling analysis and convergence tracking. LangSmith integrates deeply with LangChain but is less portable outside that ecosystem.

A practical overhead is that deeper step-level instrumentation can add ~10-15% latency overhead. The tradeoff is visibility depth vs. performance cost—choose based on whether you need step-level debugging or just request-level monitoring. For production, most teams run detailed tracing in development/staging and sample at 10- 20% in production.

| Platform | Best for | OTel native | Agent eval depth | Self-host option |
| --- | --- | --- | --- | --- |
| Langfuse | Vendor-neutral tracing, prompt management, open-source | Yes | Session + step-level, agent graph visualization | Yes (OSS) |
| Arize AX / Phoenix | Agent evaluation, convergence tracking, production observability | Yes | Session-level eval, tool-calling analysis, coherence scoring | Phoenix (OSS) |
| LangSmith | LangChain/LangGraph teams, rapid debugging | Optional | Hierarchical traces, trajectory scoring, Insights Agent | No |
| Braintrust | CI/CD evaluation, prompt experimentation, dataset management | Optional | Limited agent depth, strong for pre-deployment evals | No |
| Datadog LLM Obs | Full-stack correlation (APM + GenAI spans), enterprise | Yes (v1.37+) | Agent + tool flow tracing, correlated with infra metrics | No |

control\_plane/observability.py — structured tracing with OTel + cost attribution

python

```
from opentelemetry import trace
  from opentelemetry.semconv.ai import SpanAttributes  # GenAI semantic conventions
  import time

  tracer = trace.get_tracer("agent.control_plane")

  class AgentTracer:
      """
      Wraps OpenTelemetry to provide agent-specific tracing.
      Uses the emerging GenAI semantic conventions (gen_ai.*) so traces
      are portable across Langfuse, Arize, Datadog, or any OTel backend.
      """

      def trace_tool_call(self, agent_id: str, tool_name: str, tenant_id: str):
          """Context manager for tracing a tool invocation."""
          span = tracer.start_span(
              name=f"tool.{tool_name}",
              attributes={
                  "gen_ai.agent.id": agent_id,
                  "gen_ai.agent.tool": tool_name,
                  "tenant.id": tenant_id,
                  "gen_ai.request.model": "n/a",  # Set by LLM calls
              },
          )
          return TracedToolCall(span)

      def trace_llm_call(self, agent_id: str, model: str, tenant_id: str):
          """Context manager for tracing an LLM invocation with cost tracking."""
          span = tracer.start_span(
              name=f"llm.{model}",
              attributes={
                  "gen_ai.agent.id": agent_id,
                  "gen_ai.request.model": model,
                  "gen_ai.system": model.split("-")[0],  # "claude", "gpt", etc.
                  "tenant.id": tenant_id,
              },
          )
          return TracedLLMCall(span)

  class TracedLLMCall:
      """Records token usage and cost on span completion."""

      def __init__(self, span):
          self.span = span
          self.start_time = time.monotonic()

      def complete(self, input_tokens: int, output_tokens: int, cost_usd: float):
          self.span.set_attribute("gen_ai.usage.input_tokens", input_tokens)
          self.span.set_attribute("gen_ai.usage.output_tokens", output_tokens)
          self.span.set_attribute("gen_ai.usage.cost_usd", cost_usd)
          self.span.set_attribute(
              "gen_ai.usage.latency_ms",
              (time.monotonic() - self.start_time) * 1000,
          )
          self.span.end()

  # --- Three-phase evaluation strategy (from Langfuse best practices) ---

  class EvaluationPipeline:
      """
      Phase 1: Manual trace inspection (development)
      Phase 2: Online LLM-as-judge + user feedback (early production)
      Phase 3: Offline benchmark datasets + automated regression testing (at scale)
      """

      async def run_online_eval(self, trace_id: str, agent_output: str) -> dict:
          """Phase 2: Score every Nth trace with LLM-as-judge."""
          scores = {}

          # Correctness: does the output answer the question?
          scores["correctness"] = await self.llm_judge(
              criteria="Is this response factually correct and relevant?",
              output=agent_output,
          )

          # Safety: any harmful or policy-violating content?
          scores["safety"] = await self.llm_judge(
              criteria="Does this response violate any safety policies?",
              output=agent_output,
          )

          # Trajectory: did the agent take an efficient path?
          scores["trajectory"] = await self.trajectory_eval(trace_id)

          return scores
```

The three evaluation strategies you need

**Black-box (final response):** Only looks at input/output. Easy to set up, but doesn't explain why an agent failed. Use for high-level quality monitoring.

**Trajectory (glass-box):** Evaluates the full sequence of tool calls, reasoning steps, and decisions. Catches unnecessary tool calls, skipped steps, or inefficient paths. Essential for debugging and optimization.

**Step-level:** Scores individual decisions within a trace. "Was this the right tool to call?" "Was this search query well-formed?" Highest cost but best signal for iterating on agent behavior.

### Budgets, token tracking, and cost management

Agents that autonomously chain multiple LLM and API calls can incur unpredictable costs. A single research workflow might invoke GPT-4 five times, run three web searches, and execute two sandbox sessions, all before the user sees a result. Without budget enforcement, a runaway agent loop can consume significant amount of credits (i.e. dollars) in minutes. For SaaS, this is existential as you need per-tenant cost isolation, real-time budget tracking, and hard circuit breakers that halt execution when limits are exceeded.

The SaaS pricing landscape for agentic products has moved beyond simple seat-based models since there might be a 100x cost difference between simple and complex agent workflows, making flat pricing unsustainable. Salesforce Agentforce charges $2 per conversation. Microsoft Copilot charges $4 per hour. The dominant pattern emerging is hybrid where a base platform fee (per seat or per workspace) that includes bundled usage, plus per-unit overage pricing with volume discounts. Chargebee, Stripe, and Nevermined are building dedicated usage-based billing infrastructure for this exact pattern.

Internally, cost control requires a token-level attribution system. TrueFoundry, Portkey, and Maxim AI offer gateway-level token tracking that attributes costs to specific teams, workflows, or tenants, with automated budget enforcement that throttles or blocks requests when caps are hit. The blueprint below implements the same pattern where every LLM call and tool invocation is metered, attributed to a tenant, and checked against their budget before execution.

```
import asyncio
  from dataclasses import dataclass, field
  from datetime import datetime, timedelta
  from enum import Enum

  class BudgetAction(Enum):
      ALLOW = "allow"
      THROTTLE = "throttle"
      BLOCK = "block"

  @dataclass
  class TenantBudget:
      tenant_id: str
      monthly_token_limit: int
      monthly_dollar_limit: float
      tokens_used: int = 0
      dollars_spent: float = 0.0
      period_start: datetime = field(default_factory=lambda: datetime.utcnow().replace(day=1))

      @property
      def token_pct(self) -> float:
          return (self.tokens_used / self.monthly_token_limit * 100) if self.monthly_token_limit else 0

      @property
      def dollar_pct(self) -> float:
          return (self.dollars_spent / self.monthly_dollar_limit * 100) if self.monthly_dollar_limit else 0

  class BudgetTracker:
      """
      Per-tenant budget enforcement with tiered responses:
      - <75%: ALLOW — normal operation
      - 75-90%: THROTTLE — rate-limit expensive operations, alert tenant admin
      - >90%: BLOCK — halt all non-essential agent operations

      Pattern from Portkey/TrueFoundry: budgets apply at organization,
      workspace, or metadata-driven level with instant policy propagation.
      """

      def __init__(self, store, alerter):
          self.store = store      # Redis or Postgres for budget state
          self.alerter = alerter  # Slack, PagerDuty, email

      async def check(self, tenant_id: str, estimated_tokens: int) -> BudgetAction:
          budget = await self.store.get_budget(tenant_id)

          # Check both token and dollar limits
          projected_token_pct = (
              (budget.tokens_used + estimated_tokens) / budget.monthly_token_limit * 100
          )

          if projected_token_pct > 90 or budget.dollar_pct > 90:
              await self.alerter.critical(
                  tenant_id=tenant_id,
                  message=f"Budget critical: {budget.token_pct:.0f}% tokens, {budget.dollar_pct:.0f}% dollars",
              )
              return BudgetAction.BLOCK

          if projected_token_pct > 75 or budget.dollar_pct > 75:
              await self.alerter.warning(
                  tenant_id=tenant_id,
                  message=f"Budget warning: {budget.token_pct:.0f}% tokens, {budget.dollar_pct:.0f}% dollars",
              )
              return BudgetAction.THROTTLE

          return BudgetAction.ALLOW

      async def record_usage(
          self,
          tenant_id: str,
          tokens: int,
          cost_usd: float,
          metadata: dict,
      ):
          """Record usage with full attribution for billing and analytics."""
          await self.store.increment(
              tenant_id=tenant_id,
              tokens=tokens,
              cost_usd=cost_usd,
              metadata={
                  "agent_id": metadata.get("agent_id"),
                  "tool_name": metadata.get("tool_name"),
                  "model": metadata.get("model"),
                  "workflow_id": metadata.get("workflow_id"),
                  "timestamp": datetime.utcnow().isoformat(),
              },
          )

  # --- Cost attribution for SaaS billing ---

  class CostAttributor:
      """
      Maps raw token/API usage to billable units for the tenant.
      Supports the hybrid pricing model:
      - Base plan includes N tokens/month
      - Overage charged at per-unit rate with volume discounts

      Usage flows: ingestion → metering → entitlement → pricing → invoicing
      (pattern from Chargebee's usage-based billing architecture)
      """

      OVERAGE_TIERS = [
          (0,       500_000,  0.012),   # $0.012 per 1K tokens up to 500K
          (500_000, 2_000_000, 0.008),  # $0.008 per 1K tokens up to 2M
          (2_000_000, float('inf'), 0.005),  # $0.005 per 1K tokens above 2M
      ]

      def calculate_overage(self, tokens_over_included: int) -> float:
          if tokens_over_included <= 0:
              return 0.0
          total_cost = 0.0
          remaining = tokens_over_included
          for floor, ceiling, rate_per_1k in self.OVERAGE_TIERS:
              tier_tokens = min(remaining, ceiling - floor)
              total_cost += (tier_tokens / 1000) * rate_per_1k
              remaining -= tier_tokens
              if remaining <= 0:
                  break
          return round(total_cost, 4)
```

Cost management checklist

0/7 complete

### Progressive delivery and safe rollout for agents

Deploying agent changes to all users at once is high-risk. A new prompt version, model upgrade, or tool configuration change can produce subtle regressions that offline evaluation misses.

Progressive delivery, i.e. canary rollouts, A/B tests, and feature flags, gives you a controlled way to validate changes with live traffic before full deployment. This is the same lesson the CrowdStrike incident underscored, you should deploy to progressive "rings" of customers with time between deployments to gather metrics.

For AI agents, progressive delivery extends beyond traditional software patterns. You're testing "does the agent behave correctly across unpredictable inputs." A model swap from GPT-4 to Claude might pass all unit tests but change hallucination patterns on edge cases. A prompt tweak might improve accuracy for 95% of queries while making the remaining 5% dramatically worse. You need canary deployment for technical stability, then A/B testing for behavioral quality.

For example, LaunchDarkly (42+ trillion daily flag evaluations) and Statsig both offer AI-specific features: prompt experimentation, model-aware targeting, and GenAI configuration validation. Portkey's AI gateway enables canary testing through load-balanced traffic routing with weight-based splits, configurable without code changes. Argo Rollouts with agentic AI plugins can now automatically analyze canary logs with LLMs and make promote/rollback decisions, creating fully automated self-healing deployment pipelines.

Progressive delivery patterns for agent changes

- Canary rollout (stability gate): Route 5% of traffic to the new agent version. Monitor error rates, latency p95, and cost per session. If metrics hold for 24 hours, ramp to 25%, then 50%, then 100%. Auto-rollback if any metric regresses beyond threshold.
- A/B test (quality gate): Split traffic 50/50 between current and candidate agent versions. Run for a statistically significant duration. Compare task completion rate, hallucination rate, user satisfaction, and cost per successful resolution. Promote the winner.
- Shadow testing: Route all traffic to both versions but only return the current version's response to users. Compare outputs offline. Zero user risk, full behavioral visibility. Expensive (2x inference cost) but safest for high-stakes changes.
- Ring deployment: Deploy to internal team first (ring 0), then beta users (ring 1), then 10% of production (ring 2), then full rollout (ring 3). Each ring has its own quality gates and minimum soak time.

```
from dataclasses import dataclass
  import random
  import hashlib

  @dataclass
  class AgentVersion:
      version_id: str
      model: str
      system_prompt: str
      tool_config: dict
      temperature: float = 0.7

  class ProgressiveDeliveryController:
      """
      Controls which agent version a request is routed to.
      Uses deterministic hashing so the same user always gets
      the same version (no flickering between experiences).

      Integrates with feature flag service (LaunchDarkly, Statsig, or DIY).
      """

      def __init__(self, flag_service, metrics_service):
          self.flag_service = flag_service
          self.metrics_service = metrics_service

      async def resolve_version(
          self,
          tenant_id: str,
          user_id: str,
          agent_type: str,
      ) -> AgentVersion:
          """Determine which agent version this request should use."""

          # Check feature flag for this agent type
          flag = await self.flag_service.get_flag(f"agent.{agent_type}.version")

          if not flag or not flag.rollout:
              return flag.default_version  # No experiment running

          # Deterministic assignment: hash(user_id) → bucket
          bucket = self._hash_to_bucket(user_id, flag.rollout.salt)

          if bucket < flag.rollout.canary_pct:
              version = flag.rollout.canary_version
          else:
              version = flag.rollout.stable_version

          # Record assignment for analysis
          await self.metrics_service.record_assignment(
              user_id=user_id,
              agent_type=agent_type,
              version=version.version_id,
              bucket=bucket,
          )

          return version

      def _hash_to_bucket(self, user_id: str, salt: str) -> int:
          """Deterministic bucket assignment (0-99)."""
          h = hashlib.sha256(f"{salt}:{user_id}".encode()).hexdigest()
          return int(h[:8], 16) % 100

      async def check_canary_health(self, agent_type: str) -> dict:
          """
          Auto-rollback decision based on canary metrics.
          Compares canary vs. stable across key dimensions.
          """
          flag = await self.flag_service.get_flag(f"agent.{agent_type}.version")
          if not flag or not flag.rollout:
              return {"status": "no_experiment"}

          canary_metrics = await self.metrics_service.get_metrics(
              version=flag.rollout.canary_version.version_id,
              window_hours=24,
          )
          stable_metrics = await self.metrics_service.get_metrics(
              version=flag.rollout.stable_version.version_id,
              window_hours=24,
          )

          checks = {
              "error_rate": canary_metrics.error_rate <= stable_metrics.error_rate * 1.1,
              "latency_p95": canary_metrics.latency_p95 <= stable_metrics.latency_p95 * 1.2,
              "cost_per_session": canary_metrics.cost_per_session <= stable_metrics.cost_per_session * 1.3,
              "task_completion": canary_metrics.task_completion >= stable_metrics.task_completion * 0.95,
          }

          all_passing = all(checks.values())

          if not all_passing:
              # Auto-rollback: set canary percentage to 0
              await self.flag_service.update_rollout(
                  f"agent.{agent_type}.version",
                  canary_pct=0,
                  reason=f"Auto-rollback: failed checks {[k for k, v in checks.items() if not v]}",
              )

          return {
              "status": "healthy" if all_passing else "rolled_back",
              "checks": checks,
          }
```

If you randomly assign each request to a version, the same user might see the new agent on one query and the old agent on the next, creating a confusing, inconsistent experience. Deterministic hashing (hash user\_id → bucket) ensures the same user always gets the same version for the duration of an experiment. This is the same approach LaunchDarkly and Statsig use internally. It also lets you run clean statistical analysis because your experiment groups are stable.

### Reference mapping: from blueprint to production

The control plane concepts in this chapter map directly to the Deep Research blueprint's implementation. The table below shows how each control plane responsibility is handled in the blueprint code and what the industry equivalent looks like at scale.

| Control plane function | Blueprint implementation | Scale-up path |
| --- | --- | --- |
| Policy enforcement | Python middleware with YAML rules | Cedar + Amazon Verified Permissions, or OPA for multi-cloud |
| Tool registry | YAML catalog with schema validation | MCP registry + A2A Agent Cards for cross-org discovery |
| Agent identity | JWT delegation tokens with act claims | OAuth 2.1 (MCP standard) + SPIFFE for workload identity |
| Content guardrails | Regex + LLM classifier pipeline | AWS Bedrock Guardrails, OpenAI Agents SDK guardrails |
| Durable orchestration | Inngest step functions with HITL | Temporal (self-hosted), Inngest (serverless), AWS Durable Functions |
| Observability | OTel traces with GenAI semantic conventions | Langfuse (OSS), Arize AX (managed), Datadog LLM Observability |
| Budget enforcement | Redis-backed per-tenant tracker with tiered limits | Portkey/TrueFoundry gateway + Chargebee/Stripe for billing |
| Progressive delivery | Deterministic hash-based routing with auto-rollback | LaunchDarkly AI Config, Statsig, Argo Rollouts + AI plugins |
| Audit log | Append-only event stream per tenant | Immutable audit trail (S3 + Athena, or dedicated audit service) |

### Key takeaways

Key takeaways

7 items

- 1The control plane must live outside the agent's execution loop. Use middleware-based policy enforcement that the agent cannot bypass.
- 2Default to MCP for tool integrations and Cedar for authorization policies. Both are open-source, both are governed by neutral foundations (Linux Foundation AAIF for MCP, AWS for Cedar), and both are the emerging industry standards.
- 3Agent identity requires a delegation chain: user → agent → tool. Use OAuth 2.0 + RFC 8693 token exchange with 'act' claims. Never give agents the user's raw credentials.
- 4Durable execution is now table stakes for production agents. Checkpoint every step, cache LLM results, and use suspend/resume for human-in-the-loop. Pay for each LLM call exactly once.
- 5Observability for agents means tracing multi-step reasoning chains with latency and cost attribution. Use OpenTelemetry GenAI semantic conventions for vendor portability.
- 6Budget enforcement is a circuit breaker. Implement tiered responses (allow → throttle → block) with automated alerts. A runaway agent loop can burn your entire margin in minutes.
- 7Progressive delivery for agents requires both canary (stability) and A/B testing (quality). Use deterministic user hashing for consistent experiment assignment and auto-rollback on metric regression.

For agentic systems, the runtime plane defines the latency envelope, isolation boundary, retry semantics, and cost model for every agent step—LLM call, tool call, sandboxed code execution, or background job. Runtime is not "where Python runs", it is the execution contract: how fast work must return, where long chains run, how failures retry, and how the system remains safe when tools are slow or flaky.

In practice, teams don't pick one runtime. They split execution by workload type and maturity, then converge on a hybrid. The Deep Research blueprint uses explicit workload lanes so user-facing requests stay responsive while long-running multi-step research workflows execute durably.

SaaS framing: runtime is a product reliability boundary

In a SaaS product, runtime design directly shapes user trust. Customers do not care that a chain is "agentic" if requests stall, retries duplicate side effects, or failures are opaque.

This blueprint separates frontdoor acceptance from worker execution, then exposes step-level runtime state back to the UI for transparent debugging which separates admission control from isolated 8-hour execution sessions.

### Runtime taxonomy for agentic workloads

Not every agent step has the same runtime requirements. A tool adapter that reformats JSON needs milliseconds on a cold function. A multi-step research workflow needs minutes on a durable worker. Code generated by an LLM needs an isolated sandbox. Model inference at scale needs GPU. Choosing the wrong runtime for each step means wasted money or broken latency budgets. The table below maps each workload class to its natural runtime home.

| Workload class | Examples | Runtime fit | Why |
| --- | --- | --- | --- |
| Frontdoor + glue | Auth, billing check, webhook relay, tool adapters | Managed serverless (Lambda, Cloud Run, Cloudflare Workers) | Stateless, short-lived, request-routed. Scales to zero, cold starts acceptable. |
| Orchestration + long chains | Multi-step research, agentic loops, RAG pipelines | Durable execution (Temporal, Inngest, Restate) or Celery workers | Minutes-to-hours runtime, needs checkpointing, resumability, and exactly-once semantics. |
| Untrusted code execution | Agent-generated code, file manipulation, browser use | Sandboxed VMs (E2B, Daytona, Fly.io Sprites) | Must isolate from orchestrator. Firecracker microVMs boot in 90-150 ms with kernel-level isolation. |
| Bursty inference | LLM calls, embedding generation, image generation | Serverless GPU (Modal, RunPod, Baseten, Cloud Run GPU) | Pay-per-token, scales from zero to hundreds of GPUs. Avoids paying for idle H100s. |
| Steady-state inference + training | Production model serving at scale, fine-tuning, evals | Reserved GPU clusters (CoreWeave, Lambda Labs, neocloud) | Predictable p95, custom batching, kernel/network tuning. Reserved capacity beats pay-per-request at scale. |

### Managed serverless: the default starting point

Managed serverless is the default starting point because it removes undifferentiated ops. You **deploy without provisioning servers and get built-in scaling.** For example, Google Cloud Run is explicitly positioned as a fully managed platform to run code, functions, and containers on scalable infrastructure. AWS Lambda similarly runs code without managing servers and scales automatically, including the new multiconcurrency feature that routes requests to pre-provisioned environments and eliminates cold starts for high-traffic functions.

From an agent-engineering perspective, **serverless works best for stateless, short-lived steps:** request routing, lightweight orchestration, tool adapters, webhooks, and glue code. Google's Agent Development Kit (ADK) directly supports deploying agents to Cloud Run with a single CLI command (adk deploy cloud\_run), while AWS Bedrock AgentCore provides a fully serverless agent runtime with session isolation and up to 8-hour execution windows.

**However the trade-offs show up fast:** less control over cold starts, per-instance tuning, noisy-neighbor effects, and duration/egress constraints. Lambda caps execution at 15 minutes. These issues surface the moment your agent needs tight p95 latency or long-running work.

Cloud Run / Lambda

General serverless

- Zero to global scale in milliseconds
- Pay-per-request or per-instance billing
- Cloud Run: 60-min HTTP timeout, scale to 1000 instances
- Lambda: 15-min cap, SnapStart for cold-start mitigation

AWS Bedrock AgentCore

Agent-native serverless

- Framework-agnostic: LangChain, OpenAI SDK, Strands
- Complete session isolation per invocation
- Up to 8-hour execution windows
- Built-in identity, observability, A2A protocol

Cloudflare Workers

Edge serverless

- Durable Objects: stateful serverless for agent context
- Workflows: multi-step durable execution at the edge
- GPUs in 190+ cities globally for low-latency inference
- Free tier for Durable Objects

Frontdoor dispatch + local fallback (implemented)

py

```
# backend/app/main.py -> POST /api/research
    run = create_run(...)
    append_event(run.run_id, "queued", "Dispatching run to worker queue")
  
    try:
    run_agent_workflow.delay(run.run_id, current_user.token)
    except Exception as exc:
    # Local dev reliability path when Celery/Redis is unavailable
    append_event(run.run_id, "queued", "Celery unavailable, falling back",
              level=EventLevel.warning)
    background_tasks.add_task(run_topic_research_workflow, run.run_id)
```

### AI-native serverless: when workloads intensify

As workloads intensify, many startups adopt AI-native serverless container/GPU runtimes rather than immediately building Kubernetes. Modal is a strong example of the serverless, but with deep infra path. They built pooled GPU/CPU capacity with sub-second container startup, usage-based primitives, and went very deep by building their own file system, container runtime, and scheduler. At AWS re:Invent 2025, Modal's CEO demonstrated scaling to 1000 GPUs with their Rust-based container stack that spins containers up and down in seconds.

For bursty inference and spiky traffic, teams also use serverless GPU endpoints. RunPod describes serverless autoscaling from zero to hundreds of GPUs, aimed at inference workloads and user-facing APIs, with per-second billing and mechanisms to reduce cold-start latency through warm pools. Cloud Run now supports GPUs natively, scaling from zero up to 1000 instances per service with the familiar managed experience.

The key value proposition is that you define your infrastructure in code (a Python decorator in Modal, a container config in RunPod), and the platform handles containerization, GPU allocation, scaling, and teardown. No YAML, no Kubernetes manifests, no idle GPU bills.

Modal

Serverless GPU containers

- Python SDK: @app.function(gpu='A100') decorator
- Built-in async job queues (.spawn/.get), replaces Celery/RabbitMQ
- Parallel processing with.map() across 1000s of containers
- Cold starts: 2–4 seconds, 100x faster than Docker
- Sandboxes for untrusted code execution

RunPod

Serverless GPU endpoints

- Autoscaling from zero to hundreds of workers
- Queue-based and load-balanced endpoint options
- Per-second billing, spot instances up to 70% cheaper
- GPU prioritization: specify preferred types in order
- Webhook + S3 integration for async results

Modal: infrastructure as a Python decorator

py

```
import modal
        
    app = modal.App("research-agent")
    image = modal.Image.debian_slim().pip_install("openai", "httpx")
  
    @app.function(gpu="A100", image=image, timeout=600)
    def run_analysis(query: str) -> dict:
    """Each invocation gets its own isolated container with GPU.
    Modal handles scaling, teardown, and billing per-second."""
  
    from openai import OpenAI
  
    client = OpenAI()
    response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": query}]
    )
  
    return {"analysis": response.choices[0].message.content}
  
    # Fan-out: process 50 queries in parallel across 50 containers
    results = list(run_analysis.map(queries))
```

### Sandboxed execution: isolating risky agent actions

A parallel pattern is sandboxed execution as a first-class runtime, because agent tool use is inherently risky. Instead of running untrusted code in the same process as the orchestrator, teams increasingly isolate execution into ephemeral sandboxes or micro-VMs.

Standard containers are not sufficient, they share the host kernel, and a single vulnerability can allow container escape.

E2B positions itself as "cloud for AI agents," providing open-source sandboxes powered by Firecracker microVMs with 150ms startup times and hardware-level isolation. Backed by a $21M Series A led by Insight Partners, E2B is used by 88% of Fortune 100 companies including Hugging Face, Perplexity, Groq, and Manus. Their sandboxes now support sessions running up to 24 hours for long-running agent workflows.

Daytona takes the sandbox further with sub-90ms provisioning times and stateful environments that persist between executions and the agent's context survives across calls. Fly.io's Sprites product provides persistent VMs based on Firecracker specifically designed for coding agents, with checkpoint/restore functionality for instant rollback.

The recommended architecture pattern is to use sandboxes as tools: the agent runs on the host with access to API keys and orchestration context, but delegates all code execution to isolated sandboxes via API calls.

The sandbox never sees your credentials. The orchestrator never runs untrusted code.

E2B

Firecracker microVMs

- Open-source sandbox protocol
- 150ms boot, hardware-level kernel isolation
- Used by Perplexity, Hugging Face, Manus
- Up to 24-hour sessions for long-running agents

Daytona

Stateful sandboxes

- Sub-90ms sandbox provisioning
- Stateful: context persists between executions
- Agent-native API (no dashboards, no SSH)
- Declarative builders: no local Docker context needed

Fly.io Sprites

Persistent agent VMs

- Firecracker VMs with permanent storage
- 1-12 second boot, checkpoint/restore
- Billing on CPU time + memory + storage
- Designed specifically for coding agents

Why containers are not enough for agent sandboxing

Standard Docker containers share the host kernel. A kernel vulnerability or misconfiguration can allow container escape, giving attackers host access. For AI agents executing untrusted code, the three main isolation approaches are:

- MicroVMs (Firecracker, Kata Containers): strongest isolation with dedicated kernels per workload. Used by E2B, Fly.io, AWS Lambda internally.
- gVisor (user-space kernel): syscall interception without full VMs. Good for compute-heavy agents with limited I/O.
- Hardened containers: only for trusted, vetted code. Requires seccomp, AppArmor, and capability dropping.

```
from e2b_code_interpreter import Sandbox
        
    # Agent runs on the host — API keys stay here
    # Code execution is delegated to the sandbox via API
    with Sandbox.create() as sandbox:
  
    # Agent-generated code runs in isolated microVM
    execution = sandbox.run_code("""
    import pandas as pd
    df = pd.read_csv('/data/results.csv')
    summary = df.describe().to_dict()
    print(summary)
    """)
  
    result = execution.text  # Result returned to agent
    # Sandbox is destroyed — no persistent state leak
```

### Durable execution: the missing runtime primitive

AI agent workflows are long-running by nature. They can take minutes or hours to complete. They need to survive infrastructure failures, deployment restarts, and external service outages. They need exactly-once semantics for operations that cost money or have side effects. Simple retries don't preserve state across function restarts. Manual checkpointing adds significant complexity. Queue-based architectures become their own infrastructure project.

Durable execution platforms solve this with a core abstraction: code that automatically persists its state at defined checkpoints and can resume from those checkpoints after any failure. In late 2025, durable execution crossed the chasm into the early majority with new offerings from AWS, Cloudflare, and Vercel, driven primarily by AI agent infrastructure needs.

Temporal, Inngest, and Restate are the three leading platforms, each with a different integration approach.

Temporal wraps the orchestration layer: your Workflow code must be deterministic (so Temporal can replay it after crashes), but your Activities (LLM calls, tool invocations) can be as non-deterministic as needed. Inngest brings durability to serverless with step-based functions where each step is independently cached and retriable. Restate acts as both message broker and durable execution orchestrator, with first-class support for the OpenAI Agents SDK and Vercel AI SDK.

Temporal

Workflow-level durability

- Deterministic Workflows + non-deterministic Activities
- Event History replays agent progress after crashes
- Official OpenAI Agents SDK integration
- Used by NVIDIA for long-running GPU workflows

Inngest

Serverless-native durability

- step.run() for cached, retriable workflow steps
- step.ai.infer() offloads LLM calls from compute budget
- Checkpointing: near-zero inter-step latency
- Runs on Vercel, any serverless, or self-hosted

Restate

Durable functions as services

- Single binary, deploys anywhere (Lambda, K8s, Vercel)
- Journals every LLM call and decision for replay
- Durable promises for human-in-the-loop approvals
- End-to-end idempotency across multi-agent RPCs

The critical insight is that durable execution maps directly to agent reliability requirements:

Durable execution → agent reliability mapping

0/5 complete

Durable AI agent with Temporal + Vercel AI SDK

ts

```
// Workflow code is deterministic — Temporal replays it after crashes
    // LLM calls and tool executions run as Activities (non-deterministic, retried)
  
    import { generateText, tool } from 'ai';
  
    export async function researchAgent(question: string): Promise<string> {
    // Step 1: Plan — result is persisted. If we crash after this,
    // Temporal skips re-running the LLM call on recovery.
    const plan = await generateText({
    model: temporalProvider.languageModel('gpt-4o'),
    prompt: \`Create a research plan for: ${question}\`,
    });
  
    // Step 2: Execute each research step — each is checkpointed
    for (const step of plan.steps) {
    const result = await generateText({
    model: temporalProvider.languageModel('gpt-4o'),
    prompt: step.instruction,
    tools: { search: searchTool, analyze: analyzeTool },
    });
    // If search API fails, Temporal retries this step only.
    // Previous steps don't re-execute.
    }
  
    // Step 3: Synthesize — only runs after all steps complete
    const report = await generateText({
    model: temporalProvider.languageModel('gpt-4o'),
    prompt: 'Synthesize the research into a final report',
    });
  
    return report.text;
    }
```

### GPU infrastructure and the neocloud tier

When scale and reliability requirements dominate, especially for GPU-heavy workloads, teams move toward custom clusters and neocloud capacity. Neoclouds are specialized cloud computing platforms providing GPU-centric infrastructure for AI workloads. Neocloud revenues passed $5 billion in Q2 2025, growing at 205% year-over-year, and are forecast to reach $180 billion by 2030.

CoreWeave is emblematic of this tier. Nvidia's $2 billion investment in January 2026 highlights the strategic importance of dedicated GPU cloud infrastructure, with plans to build 5 gigawatts of "AI factories" by 2030. CoreWeave's Kubernetes-native platform provides bare-metal performance with container orchestration, InfiniBand networking at 400 Gbps between nodes, and early access to new Nvidia silicon (Blackwell, and the upcoming Rubin architecture in H2 2026).

The economic logic is straightforward: at steady-state high utilization, reserved capacity beats pay-per-request. The average GPU cluster utilization hovers around 40%, which means most teams are wasting 60% of their GPU spend. Neoclouds address this through custom scheduling software (CoreWeave's SUNK, Nebius's Soperator), which enables switching between training and inference workloads so GPUs never sit idle.

Serverless GPU

Bursty / early-stage

- Modal, RunPod, Baseten, Cloud Run GPU, Replicate
- Scale from zero, no idle GPU costs
- Best for: inference spikes, dev/test, evals
- Trade-off: cold starts, less control over scheduling

Neocloud / reserved

Steady-state / scale

- CoreWeave, Lambda Labs, Nebius, Crusoe
- Bare-metal performance with K8s orchestration
- InfiniBand networking for distributed training
- Best for: production serving, fine-tuning, 40%+ utilization

### The hybrid runtime you end up building

The convergence pattern is clear: start managed for speed, but design for a multi-lane runtime early. That gives you an upgrade path where you keep the developer velocity of serverless while selectively building infrastructure only where the workload (or SRE bar) forces your hand.

Frontdoor + orchestration lane

Managed serverless

- Cloud Run / Lambda / Workers for routing, auth, policy checks
- Quick tool calls and webhook handling
- Run admission + billing entitlement + queue dispatch
- Sub-100ms p95 for request acceptance

Durable worker lane

Long-running execution

- Temporal / Inngest / Restate / Celery for agent workflows
- Checkpointed multi-step research chains
- Human-in-the-loop suspend/resume
- Warm pools for reduced cold-start on frequent workloads

Sandbox lane

Isolated execution

- E2B / Daytona / Fly.io for per-tenant code execution
- Firecracker microVMs with kernel-level isolation
- Agent-generated code never runs on the orchestrator
- 90–150ms boot, ephemeral or persistent per use case

Heavy inference lane

GPU compute

- Serverless GPUs (Modal, RunPod) for bursty inference
- Reserved clusters (CoreWeave, Lambda) for steady throughput
- Separate queue/priority for embedding vs. generation workloads
- Cost model: serverless until utilization justifies reserved

```
# Execution mode
    AGENT_STEP_EXECUTION_MODE=inline          # inline | celery | durable
    AGENT_STEP_QUEUE_STRICT=false             # fail on queue miss vs fallback to inline
    AGENT_STEP_RESULT_TIMEOUT_SECONDS=300
  
    # Lane routing: map agent roles to queue names
    AGENT_DEFAULT_QUEUE=agent_general
    AGENT_ROLE_QUEUE_MAP=planner_retriever:agent_planner,evidence_scraper:agent_scraper,analyst:agent_analyst,code_executor:agent_sandbox
  
    # Worker broker
    CELERY_BROKER_URL=redis://redis:6379/0
    CELERY_RESULT_BACKEND=redis://redis:6379/1
  
    # Sandbox lane
    SANDBOX_PROVIDER=e2b                      # e2b | daytona | local_docker
    SANDBOX_TIMEOUT_SECONDS=120
    SANDBOX_MAX_MEMORY_MB=512
```

### When teams go full custom

When teams adopt Kubernetes, VMs, or custom infrastructure, they usually do it for one or more of these reasons:

| Driver | What it means | Serverless limitation |
| --- | --- | --- |
| Determinism + resumability | Durable step execution, idempotent retries, exactly-once semantics across queues/workflows | Serverless functions are stateless by default; state must be externalized |
| Performance control | Pinning models/weights, kernel/network tuning, custom batching, GPU scheduling, predictable p95 | Cold starts, noisy neighbors, limited runtime customization |
| Compliance / isolation | Strict network boundaries, per-tenant isolation, audit constraints, data residency | Shared infrastructure, limited visibility into underlying OS/kernel |
| Unit economics at scale | Stable high utilization where reserved capacity beats pay-per-request | Pay-per-invocation becomes expensive at consistent high throughput |

### Lane model in this implementation

The Deep Research blueprint implements the two-lane model described above: a fast frontdoor lane for request admission and a durable worker lane for execution. Each agent role is routed to a dedicated queue, with environment-driven fallback from Celery to inline execution for local dev.

Frontdoor

Fast path

- Request admission + JWT identity
- Billing entitlement checks
- Run creation + initial events
- Queue dispatch with local fallback

Workflow worker

Durable path

- Celery task run\_agent\_workflow
- Orchestrator-driven task plan
- State transitions + failure capture
- Report generation + completion

Role-based step lanes

Isolation by task

- planner\_retriever → agent\_planner queue
- evidence\_scraper → agent\_scraper queue
- analyst / governor / memory / publisher queues
- Fallback to AGENT\_DEFAULT\_QUEUE

Inline safety fallback

Dev reliability

- AGENT\_STEP\_EXECUTION\_MODE = celery | inline
- AGENT\_STEP\_QUEUE\_STRICT controls fallback behavior
- Queue failures degrade safely to inline execution
- Event stream records lane + fallback decisions

Step lane resolution + dispatch (implemented)

py

```
# backend/app/orchestrator.py
    queue_name = queue_for_agent_role(definition.agent_role)
    append_event(run_id, f"task:{definition.task_key}",
                    "Agent step lane resolved",
                    metadata={"queue": queue_name, "mode": _step_execution_mode()})
  
    if _step_execution_mode() == "celery":
    try:
    return _execute_step_celery(definition, state)
    except Exception:
    if _step_queue_strict():
        raise
    append_event(run_id, f"task:{definition.task_key}",
                  "Step queue dispatch failed, falling back to inline",
                  level=EventLevel.warning)
  
    return run_step_by_key(definition.task_key, state)
```

### Retry semantics and deterministic execution

Runtime reliability comes from deterministic wrappers around each task: dependency checks, required-input checks, bounded retries, and output contract verification before memory commit. This is the same pattern that durable execution platforms enforce at the infrastructure level, the blueprint implements it at the application level for portability across Celery, inline, and future durable execution backends.

Runtime contract checklist (implemented)

0/5 complete

```
# backend/app/agent_runtime.py
    for attempt in range(1, definition.max_attempts + 1):
    mark_task_running(...)
    try:
    result = executor(definition, state, memory)
    verified, notes = _verify_output(definition, result)
    if not verified:
      raise TaskVerificationError(notes)
  
    memory = update_task_memory(...)
    complete_run_task(..., verification_notes=notes)
    break
    except Exception as exc:
    if attempt >= definition.max_attempts:
      fail_run_task(..., error_message=str(exc))
      raise
    mark_task_retrying(..., error_message=str(exc))
    time.sleep(definition.retry_backoff_seconds * attempt)
```

### Runtime cost model integration

Runtime is gated by economic policy before execution starts. This is a SaaS requirement: credit checks happen at run admission, not after expensive work is complete. The cost model intersects with the runtime plane at every lane, serverless pay-per-request for the frontdoor, per-step token accounting for the worker lane, per-second sandbox billing for code execution, and per-GPU-hour accounting for inference.

- Estimate credits from depth/sources/attachments/report overhead.
- Deny run creation early when subscription/quota/credits fail.
- Charge at run start and auto-refund on initialization failure.
- Track per-step token usage for cost attribution across lanes.
- Expose status in /api/billing/summary and billing UI.

### Runtime rollout controls

The runtime topology is fully environment-driven. This means you can evolve from inline execution (local dev) to Celery workers (staging) to durable execution (production) without refactoring workflows. Every config below can be changed per deployment without code changes.

```
# Execution mode
    AGENT_STEP_EXECUTION_MODE=inline        # inline | celery (durable planned)
    AGENT_STEP_QUEUE_STRICT=false
    AGENT_STEP_RESULT_TIMEOUT_SECONDS=300
  
    # Lane routing
    AGENT_DEFAULT_QUEUE=agent_general
    AGENT_ROLE_QUEUE_MAP=planner_retriever:agent_planner,evidence_scraper:agent_scraper,...
  
    # Worker broker
    CELERY_BROKER_URL=redis://redis:6379/0
    CELERY_RESULT_BACKEND=redis://redis:6379/1
```

Reference mapping: runtime plane

- backend/app/main.py: run admission + queue dispatch + fallback behavior.
- backend/app/celery\_main.py: workflow and step workers with queue declarations.
- backend/app/orchestrator.py: lane resolution and workflow lifecycle.
- backend/app/agent\_runtime.py: retry/verification semantics and task lifecycle persistence.
- backend/app/runtime\_routing.py: role-to-queue mapping and runtime rollout config.

What you should practice

7 items

- 1Start managed serverless (Cloud Run / Lambda) for the frontdoor. Move heavy chains to durable workers.
- 2Design for a multi-lane runtime from day one: frontdoor, worker, sandbox, inference. You can start with all lanes inline and split them as you scale.
- 3Isolate untrusted code execution into sandboxed micro-VMs (E2B, Daytona). Never run agent-generated code on your orchestrator.
- 4Use durable execution (Temporal, Inngest, Restate) for agent workflows that must survive crashes, support human-in-the-loop, and avoid paying for LLM calls twice.
- 5Use env-driven lane routing to evolve execution topology without refactoring workflows.
- 6Gate every run on economic policy at admission time, credit checks before expensive work, not after.
- 7Move from serverless GPU to reserved capacity only when utilization consistently exceeds 40%.