---
title: "Anthropic Launches Claude Managed Agents (That Make Agentic AI Workflows Real)"
source: "https://medium.com/ai-software-engineer/anthropic-launches-claude-managed-agents-that-make-agentic-ai-workflows-real-91134b6f2b56"
author:
  - "[[Joe Njenga]]"
published: 2026-04-09
created: 2026-04-23
description: "Anthropic Launches Claude Managed Agents (That Make Agentic AI Workflows Real) Claude Managed Agents stops you from wasting time trying to string scripts together to make your agents work. I just …"
tags:
  - "clippings"
---
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*fsla9U699e789VBT85hI8g.png)

Claude Managed Agents stops you from wasting time trying to string scripts together to make your agents work.

> **I just tested the new Claude Managed Agents and discovered the missing link in AI agent workflows.**

First, if you have been working with AI agents or building them, you know the common problem.

You spend more time working on the logic than on the product.

> **The agent loop, tool execution, context management, sandboxing, and session handling; all of it falls on you to wire up from scratch before a single line of real logic gets written.**

When something breaks mid-task, you are back to debugging infrastructure instead of shipping.

> **That is the problem Claude Managed Agents promises to solve.** Instead of giving us another API to wrap your loop around, Anthropic is now handing us the runtime.

This is a fully managed cloud environment where Claude reads files, runs commands, browses the web, and executes code on its own.

Session continuity and context management are already handled. I took my time to fully review and see if it lives up to the promise.

## Claude Managed Agents

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*csH1LXlnsPT_dap-SunhBA.gif)

Anthropic shipped two things:

- **First is Claude Managed Agents** *— a fully hosted agent harness running on Anthropic’s infrastructure. You define the agent, fire off a task, and Anthropic’s cloud handles everything else: the container, the tools, the execution, the session.*
- **Second is the Claude Agent SDK** *(formerly the Claude Code SDK) — a Python and TypeScript library that embeds the same agent loop powering Claude Code into your own application. You host it yourself, but all the hard parts come pre-built.*

> **Both solve the same problem, but the difference is where the agent runs.**

- ***SDK — agent runs inside your own infrastructure***
- ***Managed Agents — agent runs on Anthropic’s cloud, fully managed***

> **For most developers reading this, Managed Agents is the more significant release, and for this article, we will focus on Clause Managed Agents.**

## Four Building Blocks

Managed Agents is built around four concepts. Once you understand these, the whole system clicks:

![Claude Managed Agents](https://miro.medium.com/v2/resize:fit:1278/format:webp/1*YiSDYP9jRfT1glUmDDul0w.png)

Your application sends events to a session running inside Anthropic’s cloud, where the agent and environment are already configured

- ***Agent*** *— your configuration: model, system prompt, tools, MCP servers, and skills. Define it once, reference it by ID across every session.*
- ***Environment*** *— a cloud container with pre-installed packages (Python, Node.js, Go, and more), network access rules, and mounted files. This is the workspace your agent operates in.*
- ***Session*** *— a running instance of your agent inside an environment, executing a specific task. Files, conversation history, and context all persist across its lifetime.*
- ***Events*** *— the messages flowing between your application and the agent: user turns, tool results, status updates, and streamed responses.*

> **Here’s how it looks in code. You create an agent once:**

```rb
import anthropic

client = anthropic.Anthropic()

# Create the agent — do this once, reuse by ID
agent = client.beta.agents.create(
    model="claude-sonnet-4-6",
    system="You are a software engineer. Fix bugs, run tests, and report results.",
    tools=[{"type": "bash"}, {"type": "file_operations"}, {"type": "web_search"}],
    name="bug-fixer"
)

print(agent.id)  # Save this — you'll reference it across sessions
```

Then start a session and send a task:

```rb
# Create an environment with the packages your agent needs
environment = client.beta.environments.create(
    packages=["pytest", "requests"]
)

# Start a session referencing your agent and environment
session = client.beta.sessions.create(
    agent_id=agent.id,
    environment_id=environment.id
)

# Send your task as an event
response = client.beta.sessions.events.create(
    session_id=session.id,
    content="Find and fix the failing tests in auth.py"
)
```

> **That’s the complete setup, which includes one agent definition, the environment, and the session; then Claude takes it from there.**

## How the Agent Loop Works

When you start a session, Claude doesn’t respond once and wait.

> **It runs a continuous loop that goes like this: receive prompt, evaluate the task, call tools, process results, repeat; until the job is done. Each full round trip is one turn.**

![Agent Loop Claude Managed Agents](https://miro.medium.com/v2/resize:fit:1364/format:webp/1*eYV7dA5w7BylALjAKeKzAQ.png)

Claude evaluates, calls tools, processes results, and repeats each turn autonomously until the task is complete or a limit is reached

Here’s what that looks like for a real task: “find and fix the failing tests in auth.py.”

- ***Turn 1*** *— Claude runs the test suite via Bash. Three failures come back.*
- ***Turn 2*** *— Claude reads* `*auth.py*` *the test file to understand the problem.*
- ***Turn 3*** *— Claude edits the file and re-runs the tests. All three pass.*
- ***Final turn*** *— Claude returns a text response with no tool calls. Task complete.*

Here’s how that session looks in code:

```rb
import anthropic

client = anthropic.Anthropic()

async for event in client.beta.sessions.stream(
    session_id=session.id,
    event={
        "type": "user",
        "content": "Find and fix the failing tests in auth.py"
    }
):
    # See what Claude is doing each turn
    if event.type == "assistant_message":
        print(event.content)

    # Capture the final result
    if event.type == "result":
        print(f"Done: {event.result}")
        print(f"Turns used: {event.num_turns}")
        print(f"Cost: ${event.total_cost_usd:.4f}")
        session_id = event.session_id  # save to resume later
```

> **This stream gives you full visibility: every tool call, result, and turn as it happens in real time.**

## Context Management

One thing that breaks most DIY agent setups is context.

> **Every turn adds to the context window: the prompt, tool definitions, file reads, command outputs, and conversation history. Once you hit the limit, the session dies.**

Managed Agents handles this automatically.

> **When the context window approaches its limit, the system compacts the conversation by summarizing older history to free up space while keeping recent exchanges and key decisions intact.**

This approach allows the session to continue without interruption.

### Three Controls

**Effort level** — controls how deeply Claude reasons on each turn.

![](https://miro.medium.com/v2/resize:fit:1120/format:webp/1*p2Z-d6bnYMWB9bFOiCu5Bw.png)

Set it deliberately since it affects token usage and cost.

**Max turns and budget** — cap the loop before it runs away.

```rb
session = client.beta.sessions.create(
    agent_id=agent.id,
    environment_id=environment.id,
    max_turns=20,           # stop after 20 tool-use turns
    max_budget_usd=0.50     # or when spend hits $0.50
)
```

When either limit is hit, the session returns a clear result subtype so you know why it stopped, and you can resume with the session ID if needed.

**Permission mode** — controls what Claude can do without asking.

- `*default*` *— gates anything not pre-approved through your callback*
- `*acceptEdits*` *— auto-approves file edits, still gates shell commands*
- `*bypassPermissions*` *— runs everything without prompting, for isolated containers and CI only*

**You Can Steer It Mid-Task**

While a session is running, you can send additional events to redirect it, add context, or stop it.

```rb
# Send a mid-session correction
client.beta.sessions.events.create(
    session_id=session.id,
    content="Actually, only fix the auth_token tests — leave the login tests alone"
)
```

If Claude is heading the wrong direction, you don’t wait for it to finish.

> **Sessions are also persistent; you can capture the session ID, and you can resume where you left off.**

```rb
# Resume a previous session
async for event in client.beta.sessions.stream(
    session_id="sess_abc123",   # from a previous run
    event={"type": "user", "content": "Continue — now fix the payment module too"}
):
    if event.type == "result":
        print(event.result)
```

## Claude Managed Agent Tools

One of the biggest time-wasters when building agents manually is tool execution.

> **Writing the wrappers, handling errors, and managing results back into context. With Managed Agents, that work is already done.**

Here’s the full toolset:

![](https://miro.medium.com/v2/resize:fit:1342/format:webp/1*vrp66x74nckD-KyWQpdhrA.png)

All built-in tools available in Claude Managed Agents, grouped by category

**File operations**

- `*Read*` *— Read any file in the container*
- `*Write*` *— create new files*
- `*Edit*` *— modify existing files*

**Search**

- `*Glob*` *— find files by pattern*
- `*Grep*` *— search content with regex*

**Execution**

- `*Bash*` *— run shell commands, scripts, git operations, install packages, run tests*

**Web**

- `*WebSearch*` *— search the internet*
- `*WebFetch*` *— fetch and parse full page content from any URL*

**Orchestration**

- `*Task*` *— spawn subagents for isolated work*
- `*Skill*` *— invoke reusable workflows*
- `*AskUserQuestion*` *— pause and request human input*
- `*TodoWrite*` *— track multi-step work across a session*

> **Beyond the built-ins, you connect external services via MCP servers and define custom tools with your own handlers.**

## Getting Started

Claude Managed Agents is currently in beta.

> **Access is enabled by default for all API accounts; if you already have a Claude API key, you can start.**

Here’s what you need:

- *A Claude API key from platform.claude.com*
- *The* `*managed-agents-2026-04-01*` *beta header on all requests*
- *Python or TypeScript SDK — the SDK sets the header automatically*

> **Install the SDK:**

```rb
pip install anthropic
```

> **Set your API key:**

```rb
export ANTHROPIC_API_KEY=your-api-key
```

Your first working agent in under 20 lines:

```rb
import anthropic
import asyncio

client = anthropic.Anthropic()

async def main():
    agent = client.beta.agents.create(
        model="claude-sonnet-4-6",
        system="You are a helpful engineering assistant.",
        tools=[{"type": "bash"}, {"type": "file_operations"}],
        name="my-first-agent"
    )

    environment = client.beta.environments.create(
        packages=["pytest"]
    )

    session = client.beta.sessions.create(
        agent_id=agent.id,
        environment_id=environment.id,
        max_turns=10,
        max_budget_usd=0.25
    )

    async for event in client.beta.sessions.stream(
        session_id=session.id,
        event={"type": "user", "content": "List all Python files in this directory"}
    ):
        if event.type == "result":
            print(event.result)
            print(f"Cost: ${event.total_cost_usd:.4f}")

asyncio.run(main())
```

Three features

- *Outcomes*
- *Multi-agent coordination,*
- *Persistent memory*

> **All are in research preview and require a separate access request at claude.com/form/claude-managed-agents.**

## Final Thoughts

Claude Managed Agents is a brilliant idea; the agent loop, context management, tool execution, and session continuity.

> **What used to be weeks of infrastructure work is now a configuration file and an API call. That’s a great step in building production agents fast.**

The trade-off is that the quality of your output still depends on the quality of your input.

> **Have you tried Claude Managed Agents, and what’s your experience? Let me know your thoughts in the comments below**.

## Claude Code Masterclass Course

![Claude Code Masterclass Course](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ocDWTJddrx76f_wrDC2B3w.png)

Claude Code Masterclass Course

***Every day, I’m working hard to build the ultimate Claude Code course, which demonstrates how to create workflows that coordinate multiple agents for complex development tasks. It’s due for release soon.***

It will take what you have learned from this article to the next level of complete automation.

***New features are added to Claude Code daily, and keeping up is tough.***

The course explores Agents, Hooks, advanced workflows, and productivity techniques that many developers may not be aware of.

***Once you join, you’ll receive all the updates as new features are rolled out.***

This course will cover:

- *Advanced subagent patterns and workflows*
- *Production-ready hook configurations*
- *MCP server integrations for external tools*
- *Team collaboration strategies*
- *Enterprise deployment patterns*
- *Real-world case studies from my consulting work*

If you’re interested in getting notified when the Claude Code courselaunches**,** [**click here to join the early access list →**](https://claudecodemasterclass.substack.com/)

**(** *Currently, I have* ***47,000+*** *already signed-up developers)*

> **I’ll share exclusive previews, early access pricing, and bonus materials with people on the list.**

## Let’s Connect!

If you are new to my content, my name is [Joe Njenga](https://medium.com/@joe.njenga)

> **Join thousands of other software engineers, AI engineers, and solopreneurs who read my content** [**daily on Mediu**](https://medium.com/@joe.njenga) **m and on** [**YouTube where I review the latest AI engineering tools and trends**](https://www.youtube.com/@aisoftwareengineer)**.** If you are more curious about my projects and want to receive detailed guides and tutorials**,** [**join thousands of other AI enthusiasts in my weekly AI Software engineer newsletter**](https://aisoftwareengineer.substack.com/)

If you would like to connect directly, you can reach out here:

## [AI Integration Software Engineer (10+ Years Experience )](https://njengah.com/?source=post_page-----91134b6f2b56---------------------------------------)

### Software Engineer specializing in AI integration and automation. Expert in building AI agents, MCP servers, RAG…

njengah.com

**Follow me on** [Medium](https://medium.com/@joe.njenga) | [YouTube Channel](https://www.youtube.com/@aisoftwareengineer) | [X](https://x.com/joenjenga_) | [LinkedIn](https://www.linkedin.com/in/njengah)