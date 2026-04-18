---
title: "I Compared 6 Python AI Agent Frameworks So You Don’t Have To: LangGraph vs CrewAI vs PydanticAI vs OpenAI SDK vs Smolagents vs Google ADK"
source: "https://pub.towardsai.net/i-compared-6-python-ai-agent-frameworks-so-you-dont-have-to-langgraph-vs-crewai-vs-pydanticai-vs-d8a5e6e43262"
author:
  - "[[The Dev Loop]]"
published: 2026-04-09
created: 2026-04-18
description: "I Compared 6 Python AI Agent Frameworks So You Don’t Have To: LangGraph vs CrewAI vs PydanticAI vs OpenAI SDK vs Smolagents vs Google ADK I built the same research agent six times. Only two of …"
tags:
  - "clippings"
---
[Mastodon](https://me.dm/@thedevloop)

## [Towards AI](https://pub.towardsai.net/?source=post_page---publication_nav-98111c9905da-d8a5e6e43262---------------------------------------)

[![Towards AI](https://miro.medium.com/v2/resize:fill:48:48/1*JyIThO-cLjlChQLb6kSlVQ.png)](https://pub.towardsai.net/?source=post_page---post_publication_sidebar-98111c9905da-d8a5e6e43262---------------------------------------)

We build Enterprise AI. We teach what we learn. Join 100K+ AI practitioners on Towards AI Academy. Free: 6-day Agentic AI Engineering Email Guide: [https://email-course.towardsai.net/](https://email-course.towardsai.net/)

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*lDGYbpJINKYyPx44)

Photo by Jona on Unsplash

## I built the same research agent six times. Only two of these frameworks survived my weekend.

Last month, my team needed to pick an agent framework for a client project. A document analysis pipeline — pull data from PDFs, cross-reference it with a database, generate a summary, email the result. Pretty standard stuff in 2026.

I made the mistake of asking Twitter which framework to use.

Within an hour I had 47 replies, each confidently recommending a different tool. Half of them contradicted each other. Someone called LangGraph “overengineered garbage.” Someone else called it “the only serious option.” A third person said both were wrong and I should just use raw API calls.

So I did what any reasonable person would do. I blocked out a weekend, installed all six major frameworks, and built the same agent in each one. Same task. Same model. Same tools. Same evaluation criteria.

Here’s what I found — and it’s not what the fanboys on either side want to hear.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*7J66QD70oyw9bJMEaBYquA.png)

Running AI agents in terminals (Screenshot captured by author)

## The Setup: What I Actually Built

Before we get into results, let me tell you exactly what I tested. No hand-waving.

**The task:** A research agent that takes a company name, searches the web for recent news, extracts key financial data points, cross-references them against a local SQLite database, and produces a structured JSON summary. Three tools, one agent, one output schema.

I picked this because it’s boring enough to be realistic. Nobody’s building autonomous coding agents for their first production deployment. They’re building glorified API orchestrators with a bit of reasoning sprinkled on top. That’s most agent work in the real world, and every framework should handle it well.

**The model:** GPT-4o across all six (where possible — more on that later).

**What I measured:** Lines of code to implement, token usage per run (averaged over 10 runs), average latency, how long it took me to go from zero to working prototype, and something I’m calling the “2 AM debug score” — how easy it was to figure out what went wrong when things broke. Because things always break.

## Framework 1: LangGraph — The Control Freak’s Paradise

**Lines of code:** ~210 **Time to first working agent:** 3 hours **Average tokens per run:** 2,847

LangGraph is what happens when a team of distributed systems engineers builds an agent framework. You define state. You define nodes. You draw edges between them. You compile it. It feels less like building an AI agent and more like designing a data pipeline.

And I mean that as a compliment.

The learning curve hit me hard in the first hour. I stared at *StateGraph, add\_node, add\_conditional\_edges,* and thought: *this is way too much ceremony for a three-tool agent.* I nearly quit and moved to the next framework.

But then something clicked. When my agent failed — and it did, spectacularly, on the third test query — I opened LangSmith and watched the entire execution trace step by step. I could see exactly which node made the wrong decision, what state it was holding, and why it chose to call the database tool before the search tool.

> **The killer feature nobody talks about:** Durable execution. If your agent crashes mid-run, it picks up from the last checkpoint. For a weekend experiment, that’s nice. For a production pipeline processing 10,000 documents overnight? That’s the difference between sleeping and getting paged at 3 AM.

LangGraph had the lowest token consumption across my tests. The graph structure forces you to be explicit about control flow, which means the LLM wastes fewer tokens deciding what to do next — you’ve already told it.

**The catch:** You need to actually think about your workflow upfront. There’s no “just throw instructions at it and hope.” If your problem is well-defined, LangGraph rewards that. If you’re prototyping and don’t know what the workflow looks like yet, you’ll spend more time drawing graphs than building features.

**2 AM debug score: 9/10.** LangSmith is genuine. I could diagnose issues faster here than in any other framework.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*PpSNdc-TuTFDzpvFPTS7bQ.png)

LangGraph State Machine (Illustration created by autor by using web elements)

## Framework 2: CrewAI — The Fast Prototype Machine

**Lines of code:** ~340 **Time to first working agent:** 45 minutes **Average tokens per run:** 4,216

Forty-five minutes. That’s how long it took me to go from *pip install crewai* to a working agent that produced correct output.

CrewAI’s abstraction is different from everything else on this list. You’re not building agents — you’re assembling a team. Each agent gets a role, a goal, and a backstory. You assign tasks to the team, and they figure out who does what.

```c
researcher = Agent(
    role="Financial Research Analyst",
    goal="Find and verify recent financial data",
    backstory="You're a senior analyst at a hedge fund...",
)
```

I’ll be honest: I rolled my eyes at the *backstory* parameter. It felt gimmicky. Then I noticed that my CrewAI agent's outputs were significantly more detailed than the same prompt in raw API calls. The role framing actually changes how the model approaches the task.

But speed comes at a cost.

CrewAI used roughly 48% more tokens than LangGraph for the same job. The multi-agent overhead is real — even when you technically only need one agent, CrewAI’s architecture assumes you’ll have at least two or three collaborating. My “team” of a researcher and a writer was doing work a single agent could handle, and every delegation round-trip burned tokens.

The other issue: CrewAI is synchronous under the hood. I had to wrap everything in *run\_in\_executor* to get it working with my async FastAPI backend. Not a dealbreaker, but annoying enough that I'm mentioning it.

**The catch:** Token costs add up fast. One comparison found CrewAI testing costs at $1,088 versus $390 for an equivalent PydanticAI implementation. When your agent runs thousands of times a day, that gap compounds.

**2 AM debug score: 5/10.** When things work, they work beautifully. When they don’t, the agent delegation chain becomes a black box. I spent 40 minutes debugging an issue that turned out to be one agent delegating a task to another agent that delegated it back.

## Framework 3: PydanticAI — The Quiet Overachiever

**Lines of code:** ~130 **Time to first working agent:** 1.5 hours **Average tokens per run:** 2,912

If LangGraph is for control freaks and CrewAI is for speed demons, PydanticAI is for the developer who wants their code to actually make sense six months from now.

This framework was built by the Pydantic team. If you’ve used FastAPI, you already know half the API. Agents are typed. Outputs are validated. Dependencies are injected. Everything that can be caught at build time, is.

```c
agent = Agent(
    "openai:gpt-4o",
    result_type=CompanyAnalysis,  # Pydantic model
    system_prompt="You are a financial research assistant.",
)
```

That *result\_type* parameter is doing more work than it looks. PydanticAI validates every LLM response against your schema automatically. If the model returns malformed JSON (and it will, eventually), the framework catches it and retries. I didn't have to write a single line of validation code.

The controlled comparison from the *full-stack-ai-agent-template* project tells the story clearly: PydanticAI implemented the same chat application in about 160 effective lines of code. LangGraph needed about 280. CrewAI needed around 420.

Fewer lines isn’t always better. But in this case, it correlates perfectly with how quickly I could understand what each implementation was doing. I could read the PydanticAI version and know immediately what every line did. The LangGraph version required me to mentally trace the graph. The CrewAI version required me to understand the delegation model.

**The catch:** PydanticAI is a single-agent framework. It doesn’t have built-in multi-agent orchestration, handoff patterns, or agent delegation. If your project needs three agents collaborating on a task, you’ll be writing that coordination logic yourself. The *pydantic-graph* module exists, but it's not at the level of LangGraph or CrewAI for complex workflows.

**2 AM debug score: 8/10.** Type errors surface early. The IDE catches things before runtime. When something does break, stack traces point to exactly the right place.

## Here’s Where Things Got Interesting

I was three frameworks in and starting to see a pattern. Each framework made different tradeoffs, and each was genuinely good at what it optimized for.

But the next three surprised me.

## Framework 4: OpenAI Agents SDK — The Sleeper Hit

**Lines of code:** ~150 **Time to first working agent:** 1 hour **Average tokens per run:** 2,791

I almost didn’t include this one. “OpenAI’s own framework” sounds like vendor lock-in wrapped in a bow. I expected it to be a glorified wrapper around their API.

I was wrong.

The Agents SDK is what happened when OpenAI looked at their earlier experiment (Swarm) and rebuilt it for production. The primitives are dead simple: Agents, Handoffs, Tools, Guardrails. That’s it. Four concepts.

The handoff pattern is the standout. Instead of building complex orchestration logic, you define which agents can “hand off” to which other agents. The framework handles the routing. It’s not as flexible as LangGraph’s graph model, but for 80% of multi-agent use cases, it’s good enough and dramatically simpler.

```c
agent = Agent(
    name="Researcher",
    instructions="You are a financial research assistant.",
    tools=[search_tool, db_tool],
    handoffs=[summary_agent],
)
```

Here’s what caught me off guard: despite being “OpenAI’s SDK,” it’s actually provider-agnostic now. They added support for 100+ LLMs through their any-llm adapter. I ran my test with Claude and it worked without code changes.

Token efficiency was nearly identical to LangGraph — the lowest alongside it in my tests. The built-in tracing is also solid, though not quite at LangSmith’s level.

**The catch:** The ecosystem is smaller. LangGraph has years of community tools, tutorials, and battle-tested patterns. The OpenAI Agents SDK is newer, and when you hit an edge case, you’re often on your own.

**2 AM debug score: 7/10.** Tracing is built-in and useful. Error messages are clear. But the documentation has gaps — I found myself reading source code more than I’d like.

## Framework 5: Smolagents — The Open-Source Purist’s Dream

**Lines of code:** ~95 **Time to first working agent:** 30 minutes **Average tokens per run:** 3,340

Ninety-five lines. Thirty minutes. That’s not a typo.

Smolagents is HuggingFace’s answer to agent frameworks, and it takes minimalism seriously. The entire core logic fits in roughly 1,000 lines of Python. You can read the whole thing in an afternoon. Try doing that with LangGraph.

But Smolagents isn’t just small — it’s philosophically different. While every other framework on this list uses JSON-based tool calling (the agent outputs a JSON blob saying “call this function with these arguments”), Smolagents’ *CodeAgent* writes actual Python code to accomplish tasks.

```c
agent = CodeAgent(
    tools=[search_tool, db_tool],
    model=InferenceClientModel(),
)
result = agent.run("Analyze recent financial news for Acme Corp")
```

The code-generation approach means the agent can compose tools naturally. It can write a for loop. It can use conditionals. It can chain operations in ways that JSON tool-calling simply can’t express. The research backs this up — code agents outperform JSON-based agents on most benchmarks.

The tradeoff? Security. Your agent is writing and executing Python code. Smolagents supports sandboxing through E2B, Docker, and Pyodide, but you have to set it up yourself. The default *LocalPythonExecutor* is explicitly not a security boundary — it says so in the docs.

I also hit higher token usage compared to LangGraph and OpenAI SDK. Code generation is verbose. The model is writing Python, not compact JSON, and every variable declaration and import statement costs tokens.

**The catch:** If you’re running Gemini or GPT, Smolagents works fine but feels like a square peg. It shines brightest with HuggingFace models and infrastructure. The Hub integration — sharing and loading agents like you’d share a model — is killer, but only if you’re already in that ecosystem.

**2 AM debug score: 8/10.** Reading the agent’s generated code is infinitely easier than parsing JSON tool call chains. When the code fails, you get a Python traceback. Familiar territory.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*KubcyjTsy4AiUUfsI3G_kg.png)

Running Smolagents in terminals (Screenshot captured by author)

## Framework 6: Google ADK — The Enterprise Sleeper

**Lines of code:** ~180 **Time to first working agent:** 2 hours **Average tokens per run:** 3,102

Google’s Agent Development Kit arrived quietly in 2025, and most Python developers I know have never tried it. That’s a mistake.

ADK is built the way Google builds internal tools: opinionated about structure, flexible about execution. You define agents with a model, a name, instructions, and tools — similar to the OpenAI SDK’s approach. But ADK layers on workflow agents (Sequential, Parallel, Loop) and the new AgentTeam API for multi-agent coordination.

```c
from google.adk.agents import Agent
```
```c
root_agent = Agent(
    model="gemini-2.5-flash",
    name="financial_analyst",
    instruction="You are a financial research assistant.",
    tools=[search_tool, db_tool],
)
```

The built-in evaluation framework is what separates ADK from the pack. You write test cases as JSON, run *adk eval*, and get structured reports on whether your agent's behavior matches expectations. No other framework on this list ships evaluation tooling this mature out of the box.

Deployment is also smooth — if you’re on Google Cloud. The Vertex AI Agent Engine handles scaling, monitoring, and session management. But “if you’re on Google Cloud” is doing a lot of heavy lifting in that sentence.

**The catch:** ADK is optimized for Gemini. Yes, it supports other models through LiteLLM, but the documentation, examples, and tooling all assume you’re using Gemini. When I ran it with GPT-4o, I hit undocumented edge cases that took 45 minutes to resolve.

**2 AM debug score: 6/10.** The built-in dev UI (adk web) is nice for debugging. But when the agent misbehaves, the error messages are sometimes cryptic. Google-style documentation — comprehensive but hard to navigate.

## The Verdict: It Depends (But Not the Way You Think)

I know, I know. “It depends” is the most unsatisfying answer in tech. So let me be more specific.

After building the same agent six times, here’s the decision framework I’d actually use:

**You need something in production by Friday?** Use **CrewAI** or **Smolagents**. CrewAI if your team isn’t technical enough to debug Python code execution issues. Smolagents if they are and you want the smallest possible dependency footprint.

**You’re building something that needs to run reliably for months?** Use **LangGraph** or **PydanticAI**. LangGraph if your workflow has branching logic, human-in-the-loop steps, or needs durable execution. PydanticAI if it’s primarily single-agent with structured outputs and you want your future self to actually understand the code.

**You’re already invested in a specific ecosystem?** Use **OpenAI Agents SDK** if you’re on OpenAI’s platform and want their tracing and evaluation tools. Use **Google ADK** if you’re on GCP and want native Vertex AI integration with built-in eval.

**The uncomfortable truth nobody wants to say out loud:** for most projects, the framework matters less than your prompt engineering and tool design. I got nearly identical output quality across all six frameworks when I spent time on the system prompt and tool descriptions. The difference was in developer experience, debuggability, and operational overhead.

My personal production stack, if you’re asking? PydanticAI for single-agent tasks (most of what I build), LangGraph when the workflow is genuinely complex. I’ve stopped apologizing for using two frameworks.

## The Full Comparison Table

Here’s everything in one place.

```c
| Metric            | LangGraph   | CrewAI          | PydanticAI    | OpenAI SDK       | Smolagents      | Google ADK      |
| ----------------- | ----------- | --------------- | ------------- | ---------------- | --------------- | --------------- |
| Lines of code     | ~210        | ~340            | ~130          | ~150             | ~95             | ~180            |
| Time to prototype | 3 hrs       | 45 min          | 1.5 hrs       | 1 hr             | 30 min          | 2 hrs           |
| Avg tokens/run    | 2,847       | 4,216           | 2,912         | 2,791            | 3,340           | 3,102           |
| Multi-agent       | Yes (graph) | Yes (teams)     | Manual        | Yes (handoffs)   | Yes (hierarchy) | Yes (AgentTeam) |
| Type safety       | TypedDict   | Pydantic config | Full generics | Generic context  | Minimal         | Standard        |
| MCP support       | Yes         | Limited         | Native + A2A  | Native           | Yes             | Yes             |
| Model-agnostic    | Yes         | Yes             | Yes (20+)     | Yes (100+)       | Yes (LiteLLM)   | Gemini-first    |
| Best debugger     | LangSmith   | Logs            | IDE/types     | Built-in tracing | Code output     | ADK Web UI      |
| GitHub stars      | ~48K        | ~44K            | ~15K          | ~16K             | ~26K            | ~23K            |
| 2 AM debug        | 9/10        | 5/10            | 8/10          | 7/10             | 8/10            | 6/10            |
```

None of these numbers tell the full story. But they’re a starting point that’s more honest than most framework comparison posts you’ll find.

## The One Thing I Wish I Knew Before Starting

Here’s what all six frameworks have in common: they’re evolving faster than anyone can write about them.

LangGraph shipped a major update while I was writing this post. CrewAI’s enterprise tier got new integrations last week. PydanticAI added A2A protocol support. Google ADK released a SkillToolset feature three days ago.

Whatever I’ve written here has a shelf life. In six months, the performance gaps might close. The missing features might ship. The framework you dismissed might become the obvious choice.

The best framework is the one your team can actually debug at 2 AM when the pipeline breaks and the client is waiting. Pick based on that, not on GitHub stars.

*If you’ve built something with any of these frameworks, I’d love to hear what worked and what didn’t. Drop your experience in the comments, especially if your results contradict mine.*