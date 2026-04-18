---
title: "Building an AI Agent from Scratch with pure Python"
source: "https://levelup.gitconnected.com/building-an-ai-agent-from-scratch-with-pure-python-7d4532202637"
author:
  - "[[Christian Bernecker]]"
published: 2026-02-16
created: 2026-04-18
description: "Stop using LangChain. Learn to build production-ready AI agents in Python using Plan-and-Execute, Pydantic validation, and custom tools."
tags:
  - "clippings"
---
## [Level Up Coding](https://levelup.gitconnected.com/?source=post_page---publication_nav-5517fd7b58a6-7d4532202637---------------------------------------)

## From Theory to Implementation: Building a Robust, Self-Correcting AI Agent from Scratch

In our previous article, [“Beyond the Chatbot,”](https://medium.com/gitconnected/stop-chatting-start-doing-the-shift-from-ai-chatbots-to-ai-agents-8c75977cb010) we established a simple definition:

> An **Agent** is an LLM equipped with **Tools** and a **Loop**.

While frameworks like LangChain or CrewAI are powerful, they often wrap the logic in so many layers that you lose sight of the “mechanical” reality. To truly master AI, you need to build one from the ground up using raw Python and direct API calls.

## Not a Medium member? Click here to read the full articel

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Pr8YCyspZ8B4bSH6YWXpSA.png)

In this guide, we will build a **Structured Plan-and-Execute Agent**. While often grouped under the “ReAct” umbrella, this architecture is more robust for complex workflows because it breaks down a query into a JSON-based task list before execution.

> **YOU LOOKED FOR REACT?:** Don’t worry — in the [next articel](https://levelup.gitconnected.com/building-a-react-ai-agent-from-scratch-in-pure-python-4036dbe4a507), we will cover and implement a full **ReAct Agent** from scratch. But if you are new to agents and you are serious about this field, **start with this pattern.** Plan-and-Execute provides the structural discipline and predictability required for high-accuracy, real-world systems. Starting here is how you become a true expert rather than just someone who “prompts.”

📌 **All code examples are available on my GitHub — link in the footer!**

### What we’re building:

- **The Hands:** Defining Python functions and their JSON schemas for LLM compatibility.
- **The Planner:** Using a reasoning-heavy LLM call to decompose complex queries into a task list.
- **The Executor:** Iterating through tasks and mapping them to specific tools.
- **The Safety Net:** Implementing a 3-stage retry loop to handle the “chaos” of non-deterministic JSON.

## The Architecture: Plan then Execute

Unlike the classic ReAct pattern (which thinks and acts one step at a time), our agent follows a more organized three-stage pipeline:

![A technical flowchart titled “THE ARCHITECTURE: PLAN THEN EXECUTE” showing a three-stage pipeline. Stage 1 (The Planner) deconstructs a user question into a JSON list of tasks. Stage 2 (The Executor) shows an LLM selecting tools, running Python functions, and appending results in a loop. Stage 3 (The Synthesizer) takes the execution history to generate a final conversational answer.](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*gEcF-78mWTe8heARMfKy5w.png)

AI Agent Plan Thrn Execute Pattern Architectur

1. **The Planner:** The LLM receives the user question and returns a JSON list of tasks.
2. **The Executor:** For each task, the LLM selects the appropriate tool, we run the Python function, and we append the result.
3. **The Synthesizer:** Finally, the LLM takes the entire execution history to provide the final answer.

Understanding the pipeline is our map, but a map is useless without the right equipment. To turn this blueprint into a working machine, we must first build the interface that allows the AI to touch the real world. In the agentic world, we call these “Hands.”

## Step 1: Implementing the “Hands” (The API Contract)

Before our agent can execute a plan, it needs to know what it is actually capable of doing. Step 1is all about defining the “Hands” (Tools).

Think of this as creating a **API Contract** between your Python environment and the LLM. The LLM cannot see your Python code; it can only see the **JSON Schema** you provide. Therefore, every tool consists of two parts:

1. **The Logic:** The actual Python function that does the work.
2. **The Schema:** The description that tells the LLM when and how to call that function.
![An engineering diagram titled “THE TRANSLATION BRIDGE: JSON SCHEMA” illustrating the API contract between an LLM and a Python environment. On the left, “The Brain” speaks “Text” through text-based requests. On the right, “The Hands” speak “Code” through executed functions. In the center, a scroll titled “THE API CONTRACT” shows how JSON definitions for a function like “getUserInfo” are translated into actual Python code structure.](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*go3G2s06gD2FbE7DzSuk5Q.png)

How does an LLM know how to use a function

Let’s start by building the hands of our agent: Firs we need to define the Python functions and their JSON schemas.

### Connecting the Brain (LLM) and the Hands

Before we look at the raw Python, we need to solve the biggest problem in AI engineering: **Language:** *Your Python environment speaks “Code” (functions and variables), but your LLM speaks “Text.”* To bridge this gap, we use **JSON Schemas**. Think of this as the “Translation Manual” that allows the Brain to understand how to move its Hands.

In our architecture, **Step 1** is all about creating this manual. We don’t just write a function; we write a **Function Declaration** that tells the LLM:

- **What** the tool does (The Description).
- **What** specific data it needs (The Parameters).

This is the “API Contract” that ensures when the Planner says “Get mass of Mars,” the Executor knows exactly which function to trigger. Here is an example of a **Function Declaration:**

```c
# 1. The Schema (What the LLM sees)
tools_schema = [
    {
        "type": "function",
        "name": "get_planet_mass",
        "description": "Get the mass of a given planet.",
        "parameters": {
            "type": "object",
            "properties": {
                "planet": {"type": "string", "description": "Planet name (e.g., Earth)"},
            },
            "required": ["planet"],
        },
    },
    # ... additional tools like 'calculate'
]

# 2. The Logic (What Python executes)
def get_planet_mass(planet_dict):
    planet = planet_dict["planet"].lower().strip()
    masses = {"earth": "5.972e24 kg", "mars": "6.39e23 kg", "jupiter": "1.898e27 kg"}
    return masses.get(planet, "Unknown planet.")
```

With the **API Contract** established and the agent’s hands ready, we now need to implement the reasoning engine that decides exactly when and how to move them: **The Planner.**

## Step 2: The Planner (The Internal Blueprint)

Now that our agent has its hands, we need to implement the **Planner**.

**The Planner** ’s job isn’t to *do* the work, it is to **deconstruct** the chaos of a human query into a structured, executable JSON list. We provide the LLM with a **System Prompt** that acts as its **rulebook**, forcing it to output valid JSON rather than a conversational essay.

> ***Why we use JSON here:*** *By forcing the Planner to output a structured list of* `*tasks*`*, we create a clean hand-off. The Executor doesn't have to "guess" what's next; it simply iterates through the list.*

```c
def __plan_tasks(self, user_prompt: str)-> json:
        '''This plans the task the LLM will do'''
        planner_system_prompt = (
            "You are a sophisticated planner Agent. "
            "Your job is to break down complex user questions into sequential, simple tasks. "
            "Return a JSON object with a single key  "
            " - 'tasks': list[string] #which contains a list of strings."
        )
        
        action_plan = self.call_llm(planner_system_prompt, user_prompt)
        return json.loads(action_plan.output_text)
```

A plan, however, is just a list of intentions. To turn those intentions into reality, we need a mechanism to map each task to the specific tools we defined in Step 1: This is realized in the **Executor.**

## Step 3: The Executor (Mapping & Doing)

**The Executor** is the **Workhorse** of the agent. It iterates through the Planner’s list, identifies which tool fits the specific job, and handles the literal Python execution. This is also where we implement **Retry Logic** — ensuring that if the LLM makes a formatting error, the agent self-corrects instead of crashing.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*XmHTFOzekfCcuerdYQqwzQ.png)

**Simply:** For every task in the plan, we ask the LLM: **“Which tool fits this specific task?” T** hen we execute that tool and store the result in an `execution_plan`.

Notice how we don’t just run the tool; we store the result back into an `execution_plan`. This allows the agent to "remember" what it just did, enabling later tasks to depend on earlier results.

```c
def __plan_tools(self, action_plan, tools):
    execution_plan = []
    for task in action_plan["tasks"]:
        # 1. Ask the Brain: "Which tool fits this task?"
        response = self.call_llm(execution_system_prompt, user_prompt)
        # 2. Map the LLM's string choice to our actual Python function
        function_to_call = self.available_tools_dict[response["function"]]
        response["result"] = function_to_call(*kwargs) 
    return execution_plan.append(response)
```

To get a machine to talk to a machine, we need a very specific prompt. We force the LLM to return a JSON object with specific keys. This structure is what allows our Python loop to run without human intervention.

> **Pro-Tip:** Notice the `execution_system_prompt` below. We explicitly tell the LLM: *"If no tools fit, write None."* This prevents the agent from "faking" an action when it doesn't have the right equipment.

```c
execution_system_prompt  = (
            "You are a sophisticated planner Agent. "
            "Your job is to find the correct given tools to the system to solve the given tasks."
            "The available tools and the task you will get from the user"
            "If no tools fit to Task write None"
            "Return a JSON object with a single key  "
            " - 'id: int #unique id to identify the task "
            " - 'task': {task}"
            " - 'function': string # name of the tool"
            " - 'properties: list # properties to execute the function"
            " - 'dependencies': list # id's if the needed results of other tasks"
        )

user_prompt = (f"I have the following task to do: {task}"  
               f"I can use the following tools: {tools} to solve the taks "
               "Tell me the correct tool to use for a given task"
               f"Here is the full list of tasks {action_plan}"
               F"Here are the executions that are already done {execution_plan} take the results of tasks have dependencies."
            )
```

We now have the Hands (Tools), the Plan (Blueprint), and the Execution Trace (The raw data). But an agent that just runs code and exits is just a script. To transform this into a partner, we need a “Voice” to translate these technical results back into human insight: **The Synthesizer.**

## Step 4: The Synthesizer (The Voice)

**The Synthesizer** acts as the agent’s final quality control. Its job is to look at three things:

1. **The Original Question:** What did the user actually want?
2. **The Plan:** What steps did we decide to take?
3. **The Execution Trace:** What were the literal outputs from our tools (the planet masses, the calculations, etc.)?

Instead of just dumping raw data like `5.972e24 kg`, the Synthesizer weaves this into a natural, authoritative response. It provides the "So what?" that makes the data useful.

```c
def __synthesize_answer(self, user_prompt, execution_results):
    synthesis_prompt = (
        "You are a helpful assistant. You have been given a user question"
        "and a set of execution results from various tools. "
        "Your goal is to provide a final, concise answer based on these results."
    )
    
    # We combine the history into a single 'context' string for the LLM
    context = f"User Question: {user_prompt}\nResults: {execution_results}"
    return self.call_llm(synthesis_prompt, context)
```

## Closing the Loop: Why this Matters

By separating the **Planner**, **Executor**, and **Synthesizer**, you have built an agent that is significantly more resilient than a basic chatbot:

- **Auditability:** If the answer is wrong, you can check the **Planner** to see if the logic was flawed, or the **Executor** to see if a tool failed.
- **Token Efficiency:** You aren’t forcing the LLM to “re-read” the entire conversation every single second; you are giving it specific context for specific tasks.
- **User Trust:** The final synthesis ensures the user gets a polished answer, hiding the messy JSON-heavy middle.

## EXPERT Section: Get Enterprise Ready

One of the hardest lessons in AI engineering is that LLMs are unpredictable. Even GPT-4 occasionally returns malformed JSON or “hallucinates” a parameter that doesn’t exist. In a lab, this is a minor bug; in an Enterprise environment, it’s a system failure.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*MEvelqfRLlmUqKfFo124yg.png)

To move from a prototype to a production-grade agent, you need multiple layers of defense. I will show you 3 to start with:

### 1\. Strict Schema Validation (Enter: Pydantic)

Don’t rely on the LLM to get the JSON right. Instead, use a library like **Pydantic** to enforce a “contract” at the code level. By defining your tools as Pydantic models, you can automatically validate the LLM’s output before it ever touches your functions.

```c
from pydantic import BaseModel, ValidationError

class PlanetQuery(BaseModel):
    planet: str
    include_moons: bool = False  # Default values add robustness

# If the LLM sends "world" instead of "planet", Pydantic catches it immediately.
```

More information can be found in the OpenAI Docs here: [Structured model outputs | OpenAI API](https://developers.openai.com/api/docs/guides/structured-outputs). In my code example and for simplicity I didn’t implemented it. But for enterprise it is highly recommended.

### 2\. The “Self-Correction” Retry Loop

In our implementation, we don’t just “hope” it works; we build for failure. We use a **Retry Loop** with specific error catching. If the JSON parsing fails, the agent doesn’t crash, it tries again.

If validation fails, don’t just crash. Use the error message *itself* as feedback. Send the error back to the LLM and say: *“You gave me the wrong format. Here is the error: \[ValidationError\]. Please try again.”*

```c
max_retries = 3
attempts = 0
while attempts < max_retries and not success:
    try:
        response = self.call_llm(execution_system_prompt, user_prompt)
        response_json = json.loads(response.output_text)
        success = True
    except (json.JSONDecodeError, KeyError):
        attempts += 1
```

> **Why this matters:** This 3 attempt pattern significantly increases the reliability of structured workflows, making your agent production-ready rather than just a lab experiment.

### 3\. Observability & Tracing

In enterprise, “I don’t know why it did that” is an unacceptable answer. You must log every **Thought, Action, and Observation**. This “Execution Trace” allows you to audit the agent’s decision-making process, ensuring that if a $10,000 transaction is triggered, you have a paper trail of the reasoning behind it.

### A Real World Scenario: From Planets to Profits

While our examples use planet masses and simple addition, the architecture remains identical for complex enterprise systems. In a production environment, you aren’t changing the *logic* of the agent; you are simply swapping the *tools* it holds.

Think of how this “Plan-and-Execute” pattern transforms professional workflows:

- **The Database Specialist:** Instead of `get_planet_mass()`, your tool is `query_sql_database()`. The Planner decides which columns to fetch, and the Executor handles the connection string and the raw data retrieval.
- **The Financial Analyst:** Instead of `calculate()`, your agent uses `analyze_market_trends(ticker)`. It pulls real-time data from an API, performs a sentiment analysis on recent news, and returns a risk score.
- **The Operations Manager:** A tool like `update_inventory_levels()` allows the agent to not just "chat" about stock, but to actually reconcile warehouse data after a purchase is confirmed.

> **Note:** The power of building from scratch is that you control the **Security Layer**. In an enterprise setting, your “Executor” can include permission checks — ensuring the LLM never triggers a tool it isn’t authorized to use.

## What’s Next?

As robust as this “Plan-and-Execute” model is, it has a weakness: **Static Planning.** If Task 1 returns a result that makes the rest of the plan obsolete, this agent will keep running blindly.

The “Plan-and-Execute” model is great for predictable tasks, but it lacks the **dynamic feedback** of a true ReAct loop. If Task 1 reveals information that makes Task 2 impossible, a Plan-and-Execute agent might blindly try to execute Task 2 anyway.

In the [next article](https://levelup.gitconnected.com/building-a-react-ai-agent-from-scratch-in-pure-python-4036dbe4a507), **“The Manager and the Worker,”** we will look at how to combine these two: using a Planner to start, but allowing a “Manager” agent to revise the plan in real-time based on what the “Worker” finds.

## Want to Connect?

- [**Follow me**](https://medium.com/r?url=https%3A%2F%2Fchristianbernecker.medium.com%2F) here on Medium to be the first to read [Part 2: Under the Hood](https://levelup.gitconnected.com/building-a-react-ai-agent-from-scratch-in-pure-python-4036dbe4a507), where we will write the actual Python code to build a ReAct agent from scratch.
- 👏 **Clap for this article** (you can go up to 50!) if you found the “Librarian vs. Encyclopedia” metaphor helpful — it helps other builders find this guide.
- 🤝 [**Connect with me on LinkedIn**](https://www.linkedin.com/in/christian-bernecker/) for weekly insights on AI architecture and the shift toward autonomous agents.
- 📌 **The Code of the articel GIT:** [cbernecker/AIAgentScratch](https://github.com/cbernecker/AIAgentScratch)

What’s one task you wish an AI Agent could do for you today? Let’s discuss in the comments!

## Responses (9)

Benedek Molnar

What are your thoughts?

```c
Thanks for the detailed steps and workflows! Is the workflow slower than if we use agentic frameworks?
```

60

```c
Thanks for sharing this ... really interesting read! I’m also building my own agents from scratch, so this resonated a lot 😉
```

9

```c
Great read.
What stood out to me most is how important systems are for growth.
Many people focus on posting more, but the real leverage comes from having a clear strategy behind the content.
```

2

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--7d4532202637-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)