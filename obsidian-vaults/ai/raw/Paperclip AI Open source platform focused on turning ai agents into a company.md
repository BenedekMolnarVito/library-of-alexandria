---
title: "Paperclip AI: Open source platform focused on turning ai agents into a company"
source: "https://medium.com/neuralnotions/paperclip-ai-open-source-platform-focused-on-turning-ai-agents-into-a-company-de3ed4066edf"
author:
  - "[[Nikhil]]"
published: 2026-04-02
created: 2026-04-20
description: "Paperclip AI: Open source platform focused on turning ai agents into a company Why the hardest problem in AI right now isn’t making smarter agents, it’s getting them to work together without …"
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

## [Neural Notions](https://medium.com/neuralnotions?source=post_page---publication_nav-55f59ccbee61-de3ed4066edf---------------------------------------)

[![Neural Notions](https://miro.medium.com/v2/resize:fill:76:76/1*Xv_4SeKtNfCiqRNi_wDAoA.png)](https://medium.com/neuralnotions?source=post_page---post_publication_sidebar-55f59ccbee61-de3ed4066edf---------------------------------------)

Exploring Artificial Intelligence, Large Language Models, and the ideas shaping the future of intelligent systems. Follow and subscribe for AI and Technology trends

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*YDX70Eao7NFyNOxvfvkNUQ.png)

Paperclip — Opensource AI Agents company

*Why the hardest problem in AI right now isn’t making smarter agents, it’s getting them to work together without burning through your API budget overnight.*

If you’ve spent any time running AI coding agents in 2026, you’ve probably lived through this exact scenario: you open Claude Code in one terminal, OpenClaw in another, maybe Codex in a third. Each one is doing good work. Each one has no idea the others exist. You go to bed. You wake up. One of them has been looping for eight hours and your API bill is somewhere north of $400.

Nobody warned you about this part. All the demos show a single agent doing something impressive. Nobody talks about what happens when you try to run five of them at the same time on the same project.  
That’s the gap Paperclip was built to fill, and it’s a more interesting problem than it sounds.

## What is Paperclip, exactly?

Paperclip is an open-source orchestration platform, a Node.js server with a React dashboard that takes individual AI agents and wraps them in a company structure. Org charts, job titles, budgets, goals, task tracking, audit logs, the whole thing. It launched on GitHub in early March 2026, and as of this writing, the repo has crossed 43,000 stars. That makes it one of the fastest-growing open-source AI projects of the year.

> The project was created by a pseudonymous developer who goes by [@dotta](http://twitter.com/dotta).

The backstory, as he shared on *Greg Isenberg’s Startup Ideas Podcast*, is almost comically mundane: he was running an automated hedge fund and found himself juggling 20-plus Claude Code tabs at the same time. No shared context between them. No way to track what each one was spending. No recovery if his machine restarted.

The whole operation was held together by shell scripts and a HEARTBEATS.md file. So he built Paperclip. Not as a theoretical exercise in multi-agent systems, but because he was losing money and couldn’t keep track of what his own AI agents were doing.

## The coordination problem nobody talks about

> ***Here’s the thing about AI agents in 2026:*** *individually, they’re good. Really good.*

OpenClaw can manage your inbox, scrape websites, and execute recurring tasks through messaging apps without human prompting. Claude Code can take a goal, plan a series of steps, execute them, and iterate. Codex can review pull requests and write features.

But run multiple agents on the same project and the problems pile up fast. Two agents start working on the same task because neither one knows the other exists. There’s no shared context, so the output from agent A doesn’t inform agent B’s decisions. Costs are invisible you have no idea which agent burned through **$200 at 3 a.m**. or why. And if you restart your machine, every agent loses its state.

This isn’t a niche complaint. A blog post from the **founder of Purchy**, a receipt-tracking app, described the exact same experience. An Australian AI consultancy called *Flowtivity* reported that a batch outreach campaign hit 23 leads instead of the intended three because agents were feeding outputs to each other without any governance layer.

The problem isn’t that agents aren’t capable. The problem is that nobody built the management layer.

## How Paperclip actually works

When you install Paperclip (***a single npx paperclipai onboard command does it***), the first thing you do is name a company and write a mission statement. This isn’t corporate theater it’s functional. Every goal, project, and task in Paperclip traces back to that mission, creating a chain of context that each agent can see.

When an agent picks up a ticket, it doesn’t just see “ **research Facebook ads.**” It sees the full chain: the current task traces up to “ **create Facebook ads for our software**,” which traces up to “ **grow signups by 100 users,**” which traces up to “ **get revenue to $2,000 this week,**” which traces up to the company mission.

The agent knows why it’s doing the work, not just what the work is. In practice, that distinction makes agents noticeably better at prioritizing and making tradeoffs.

After the mission, you create your first agent typically a CEO.

That CEO can then “ **hire** ” other agents: engineers, marketers, QA testers, designers, whatever the project needs. Each agent gets a role, a persona, a set of skills, and a budget. The CEO delegates tasks. Engineers execute. QA reviews output.

The whole thing runs on “heartbeats”, scheduled intervals where agents wake up, check their work queue, and act.

It’s not fully automatic, though. Paperclip requires human approval at critical points. Agents can’t hire other agents without your sign-off. They can’t execute major strategies on their own. When they hit their monthly budget cap, they stop. Every conversation, tool call, and decision is logged and traceable.

## What makes it different from other multi-agent tools

If you’ve been in the AI space for a while, you might be thinking: what about CrewAI? LangChain? AutoGen? These are all legitimate tools, but they solve a different problem.

CrewAI and LangChain help you build better individual agents or chain them together in pipelines. Paperclip sits a layer above that. It doesn’t care how your agent was built. It cares about how your agents work together as an organization.

The GitHub **README** puts it bluntly:

> “Not a chatbot. Agents have jobs, not chat windows. Not an agent framework. We don’t tell you how to build agents. We tell you how to run a company made of them. Not a workflow builder. No drag-and-drop pipelines.”

Paperclip is also agent-agnostic. It works with Claude Code, OpenClaw, Codex, Cursor, OpenCode, Gemini CLI, and anything that can receive an HTTP signal. You can mix and match your CEO on Claude, your engineers on Codex, your marketer on OpenClaw. The platform ships with eight built-in adapters and a plugin system for adding more.

**Another distinction:** Paperclip is entirely self-hosted and MIT licensed. There’s no cloud account, no vendor lock-in, no usage-based pricing from Paperclip itself. You pay only for the LLM inference costs from whatever provider you’re using.

## The “Memento Man” problem

One of the most practical ideas to come out of the Paperclip community is [@dotta](http://twitter.com/dotta) ’s description of AI agents as “Memento Man” a reference to the Christopher Nolan film where the protagonist has no ability to form new long-term memories.

AI agents are similar. They wake up capable, they can code, write, spend money but they have zero memory of who they are, where they are, or what they were doing yesterday.

The heartbeat system is Paperclip’s answer to this. When an agent wakes up on its scheduled interval, it reads a checklist: who am I, what’s my role, what tasks are assigned to me, what’s the quality bar, what happened in previous sessions. You’re essentially leaving notes for a very competent amnesiac.

When an agent does something you don’t like writes code in the wrong style, takes the wrong approach to a task, you don’t retrain the model. You go into its persona prompt and add a rule. Over time, each agent accumulates a set of constraints and preferences that make its output more aligned with what you want. It’s less like programming and more like managing a new hire who learns from written feedback.

## What Paperclip can and can’t do

Let’s be honest about what this is and isn’t.

**Where it works well:** Paperclip is good for contained, goal-driven projects that require multiple types of expertise. A solo founder building a SaaS product who wants agents handling code, content, QA, and marketing simultaneously. An agency managing several digital businesses and needing data isolation between them. A content operation where one agent researches, another writes, another edits, and another publishes. Developers who’ve outgrown a single Claude Code session and need coordination across many agents.

**Where it struggles:** API costs add up. A multi-agent session working on a non-trivial project generates serious token usage, and if you’re not watching the budget controls carefully, you’ll feel it. Output quality varies by domain the engineering agent can produce solid code, but a “designer” agent is mostly producing text-based briefs, not pixel-perfect mockups. There’s no persistent memory by default; the heartbeat system works, but it’s a workaround for a fundamental limitation of current LLMs.

**And perhaps most importantly:** Paperclip requires comfort with command-line tools, API keys, and environment configuration. If you’re looking for something you can open in a browser and start clicking, this is not that. The MindStudio review put it plainly: “ *Running Paperclip requires comfort with CLI tools, setting up API keys, and configuring environment files. It’s not a point-and-click experience.*”

## Clipmart and the idea of importable companies

The most interesting item on Paperclip’s roadmap is Clipmart, a marketplace where users can download pre-built company templates. A content agency, a development shop, a trading desk, each with a full organizational structure, agent configurations, and skills already baked in. You’d import the template into your Paperclip instance with one click and start customizing.

The latest release (***v2026.325.0, from March 25***) already shipped company import/export functionality with a file browser interface, merge-history support, and GitHub shorthand references. The marketplace itself isn’t live yet, but the underlying infrastructure is there.

[@dotta](http://twitter.com/dotta) described this concept in the Startup Ideas podcast as an “acqui-hire” for agent teams. Instead of spending hours configuring agents from scratch, you’d download a battle-tested organizational template say, Gary Tan’s G-Stack or a game studio template with a creative director, producer, and technical director and drop it into your instance.

If this catches on, the implications are worth sitting with. The smallest viable unit of a knowledge business used to be one person. A freelancer. You couldn’t run an agency with fewer than one human per function. Paperclip, and tools like it, are changing that math. One person can now direct an entire organizational structure of agents, each with defined roles and budget constraints, producing real output around the clock.

## The broader picture

Paperclip didn’t appear in a vacuum. Microsoft launched Copilot Cowork. Anthropic launched Claude Marketplace. Nvidia is building NemoClaw. The “ *AI as your coworker* ” race is on, and enterprise adoption is the prize.  
But Paperclip asks a different question.

Instead of buying into an enterprise vendor’s ecosystem, what if you built the company yourself entirely open-source, entirely self-hosted, entirely under your control?

There are already people doing this in production. Business Insider profiled solo founder Aaron Sneed, who runs 15 custom GPT agents as a management council and reports saving 20-plus hours per week. AI practitioner Nat Eliason’s agent “ ***Felix*** ” has reportedly generated over $100,000 in revenue. These aren’t theoretical use cases.

Whether the “ ***zero-human company*** ” becomes the norm or stays a niche experiment is an open question. But the coordination problem Paperclip addresses how do you get multiple AI agents to work together without chaos is real, it’s getting worse as agents get more capable, and right now there aren’t many tools solving it this directly.

The name, by the way, is a nod to Nick Bostrom’s “ ***paperclip maximizer*** ” thought experiment, the one where a superintelligent AI tasked with making paperclips converts all of Earth’s resources into paperclip factories. The framework flips that idea on its head: instead of a runaway optimizer with no constraints, it’s a structured, governed system designed to keep AI agents useful without letting them go off the rails.

Whether that irony is intentional or just a good joke depends on who you ask.

## Getting started

If you want to try it, the requirements are Node.js version 20 or higher and a terminal. Run n ***px paperclipai onboard***, yes, and the app launches in your browser and walks you through setting up your first CEO agent. An embedded PostgreSQL database is created automatically no external database setup required.

The whole process takes about five minutes. The GitHub repo is at ***github.com/paperclipai/paperclip***, the documentation lives at paperclip.ing, and the community Discord is active if you get stuck.

Just keep an eye on your API budget. The agents won’t.

Well, actually, with Paperclip, they will. That’s sort of the whole point.

> *If you found this useful, follow me for more deep dives on AI tools that solve real problems instead of just demoing well.*

[![Nikhil](https://miro.medium.com/v2/resize:fill:96:96/1*8dO7SeoZ7VsNkvFUCCA5XQ.jpeg)](https://medium.com/@nkwrites?source=post_page---post_author_info--de3ed4066edf---------------------------------------)

[![Nikhil](https://miro.medium.com/v2/resize:fill:128:128/1*8dO7SeoZ7VsNkvFUCCA5XQ.jpeg)](https://medium.com/@nkwrites?source=post_page---post_author_info--de3ed4066edf---------------------------------------)

[13 following](https://medium.com/@nkwrites/following?source=post_page---post_author_info--de3ed4066edf---------------------------------------)

Human with a story to tell, a story to preserve and a story still unfolding.

## Responses (3)

Benedek Molnar

What are your thoughts?  [florinelchis](https://medium.com/@florinelchis?source=post_page---post_responses--de3ed4066edf----0-----------------------------------)

[

Apr 9

](https://florinelchis.medium.com/this-is-an-article-from-a-person-that-most-likely-did-not-even-install-paperclip-3aaa0642f31f?source=post_page---post_responses--de3ed4066edf----0-----------------------------------)

```c
this is an article from a person that most likely did not even install paperclip. yes, it can be appealing to write articles about "buzzplatforms" such as paperclip - however when you actually try to run it you face multiple issues, most of them…
```

5[boardmain](https://medium.com/@boardmain?source=post_page---post_responses--de3ed4066edf----1-----------------------------------)

[

Apr 8

](https://medium.com/@boardmain/nice-article-i-created-clipmart-it-to-share-companies-testing-it-3f43adfd66ec?source=post_page---post_responses--de3ed4066edf----1-----------------------------------)

```c
Nice article, i created clipmart.it to share companies ( testing it ... )
```

2

```c
Interesting direction.Turning agents into a “company” sounds powerful, but once you scale multiple agents, coordination becomes the real challenge. Overlap, conflicting actions, and lack of clear ownership show up quickly.That’s where most systems start to struggle.
```

3