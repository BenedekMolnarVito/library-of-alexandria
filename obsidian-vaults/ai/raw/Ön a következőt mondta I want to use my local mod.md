---
title: "Ön a következőt mondta: I want to use my local mod..."
source: "https://gemini.google.com/app/e82738166534b90c?hl=hu"
author:
published:
created: 2026-04-20
description: "Gemini conversation with 6 messages"
tags:
  - "clippings"
---
**You**

I want to use my local model 'qwen2.5-coder:7b' with claude code via ollama.

However:

\- I loaded the model and it runs fine in ollama, but hangs in Claude Code with no response:

PS C:\\Users\\molna> ollama ps

NAME ID SIZE PROCESSOR CONTEXT UNTIL

PS C:\\Users\\molna> ollama run qwen2.5-coder:7b

\>>> hi

Hello! How can I assist you today? Is there anything specific you would like to know or discuss? Please feel

free to ask me any questions, and I'll do my best to provide helpful answers. Whether it's about technology,

general knowledge, or something else, I'm here to help.

\>>>

PS C:\\Users\\molna> ollama launch claude --model qwen2.5-coder:7b

╭─── Claude Code v2.1.114 ───────────────────────────────────────────────────────────────────────────────────────────╮

│ │ Tips for getting started │

│ Welcome back! │ Run /init to create a CLAUDE.md file with instructions for Claude │

│ │ Note: You have launched claude in your home directory. For the best ex… │

│ ▐▛███▜▌ │ ─────────────────────────────────────────────────────────────────────── │

│ ▝▜█████▛▘ │ Recent activity │

│ ▘▘ ▝▝ │ No recent activity │

│ │ │

│ qwen2.5-coder:7b · API Usage Billing │ │

│ C:\\Users\\molna │ │

╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

❯ hi

✢ Whatchamacalliting… (25s)

\- I set my environment variables as such:

$env:ANTHROPIC\_BASE\_URL = "http://localhost:11434"

$env:ANTHROPIC\_AUTH\_TOKEN = "ollama"

$env:ANTHROPIC\_API\_KEY = ""

$env:ANTHROPIC\_DEFAULT\_HAIKU\_MODEL = "qwen2.5-coder:7b"

$env:ANTHROPIC\_DEFAULT\_SONNET\_MODEL = "qwen2.5-coder:7b"

$env:ANTHROPIC\_DEFAULT\_OPUS\_MODEL = "qwen2.5-coder:7b"

$env:ENABLE\_CLAUDEAI\_MCP\_SERVERS = "false"

$env:DISABLE\_TELEMETRY = "1"

What am I missing?

---

**Gemini**

The behavior you are seeing—the CLI hanging at the "Whatchamacalliting" stage—is typically caused by an **API schema mismatch**.

While you have correctly pointed the `ANTHROPIC_BASE_URL` to your local instance, there is a fundamental architectural hurdle: **Claude Code** communicates using the Anthropic Messages API schema, whereas **Ollama** natively provides its own API or an OpenAI-compatible one. They do not speak the same "dialect" out of the box.

### The Problem: API Dialects

Claude Code expects a specific response structure, including headers and metadata (like `anthropic-version`), which Ollama does not provide. When Claude Code sends a request to `localhost:11434`, Ollama likely returns a `404 Not Found` or a `400 Bad Request` because the endpoint `/v1/messages` (Anthropic style) doesn't exist on a standard Ollama server. The CLI hangs because it’s waiting for a stream that never initializes.

---

### The Solution: Using a Proxy (LiteLLM)

To bridge this gap, you need a middleware that translates Anthropic API calls into Ollama-compatible calls. **LiteLLM** is the industry standard for this.

#### 1\. Install LiteLLM

In a new terminal, install the proxy:

```
pip install litellm
```

#### 2\. Start the Proxy Server

Run LiteLLM and tell it to map an "Anthropic" model name to your local Ollama model. This creates a local endpoint that "pretends" to be Anthropic:

```
litellm --model ollama/qwen2.5-coder:7b
```

*By default, this usually runs on `http://0.0.0.0:4000`.*

#### 3\. Reconfigure Environment Variables

Update your Claude Code environment to point to the **LiteLLM proxy** instead of Ollama directly. Note the addition of `/v1` or the specific port:

```
$env:ANTHROPIC_BASE_URL = "http://localhost:4000"
$env:ANTHROPIC_API_KEY  = "sk-any-string-here" # LiteLLM needs a placeholder
```

---

### Crucial Technical Considerations

#### 1\. System Prompt Complexity

Claude Code sends an extremely dense system prompt (often several thousand tokens) that defines its tool-use capabilities (file editing, shell execution, etc.).

- **The 7B Constraint:** While `qwen2.5-coder:7b` is excellent for its size, it may struggle to follow the strict JSON formatting required for Claude Code's agentic workflows. You may see the model "hallucinate" tool calls or fail to close tags.
- **Context Window:** Ensure your Ollama configuration for Qwen has a large enough context window (at least 32k) to handle the CLI's overhead.

#### 2\. The "Whatchamacalliting" Hang

If it still hangs with LiteLLM, check the LiteLLM terminal logs. You are likely seeing one of two things:

- **Connection Refused:** Ensure the ports match.
- **Model Name Mismatch:** Claude Code might be hard-coded to check for certain model strings. If LiteLLM is receiving a request for `claude-3-5-sonnet`, ensure your LiteLLM config maps that specific name to `ollama/qwen2.5-coder:7b`.

#### 3\. Tool-Calling Support

Claude Code relies heavily on **Tool Use (Function Calling)**.

Ollama's support for tool calling via proxies can be hit-or-miss depending on the version. If the model responds but doesn't actually *do* anything (like reading files), it's because the 7B model isn't correctly triggering the tools defined in the system prompt.

### Recommendation

For a smoother experience with local models and agentic CLIs, I recommend using **Aider** or **Continue.dev** if Claude Code proves too rigid for local overrides. They are built with local-first providers like Ollama in mind and handle the schema translation more gracefully.

Does the LiteLLM log show an incoming POST request when you try to run the CLI now?

---

**You**

Okay!

1\. I installed LiteLLM with pip

2\. what do I need to insert in the PATH? --> litellm: The term 'litellm' is not recognized as the name of a cmdlet, function, script file, or operable program.

3\. Compare and contrast the best and most popular LOCAL-FIRST Agentic CLIs that work well with Ollama

---

**Gemini**

To get LiteLLM running and move beyond the configuration hurdles with local models, here is the technical breakdown for your setup.

### 1\. Fix: LiteLLM "Not Recognized" (The PATH Issue)

When you install packages via `pip`, the executable scripts are placed in a specific Python `Scripts` folder that often isn't automatically added to the Windows PATH.

**The Quick Fix (Run as Module):** You don't need to fix the PATH to start working immediately. Just use the Python module runner:

```
python -m litellm --model ollama/qwen2.5-coder:7b
```

**The Permanent Fix (Update PATH):**

1. Find your Python Scripts path by running: `pip show litellm`
	- Look for the **Location** line (e.g., `C:\Users\molna\AppData\Local\Programs\Python\Python311\Lib\site-packages`).
2. The folder you need is usually one level up in the `Scripts` directory (e.g., `C:\Users\molna\AppData\Local\Programs\Python\Python311\Scripts`).
3. Add this folder to your **User Environment Variables** under `Path`.

---

### 2\. Comparison: Local-First Agentic CLIs (2026 Edition)

Since you are using **Ollama** and **Qwen2.5-Coder**, you are looking for tools that handle "Small Model" limitations (like JSON adherence) well.

| Tool | Focus | Why it fits Ollama | Trade-off |
| --- | --- | --- | --- |
| **Aider** | Git-Centric Coding | **Best-in-class.** Has specific "edit formats" for smaller models (like `whole` or `diff`) so 7B models don't break. | Terminal-only; steep learning curve for advanced commands. |
| **Goose** (by Block) | Full-System Agent | Uses **MCP (Model Context Protocol)**. It can install dependencies and run tests natively. | Heavier system requirements; Qwen 7B might struggle with its complex system prompt. |
| **Roo Code** (VS Code) | Modal Agentic | Highly customizable. Has "Architect" vs "Code" modes which help 7B models focus on one task at a time. | Requires VS Code; not a pure standalone CLI like Claude Code. |
| **OpenCode** | Model Agnostic | Built to be a drop-in open-source alternative to Claude Code. Very lightweight. | Smaller community; less documentation for complex multi-file refactors. |

---

### 3\. Professional Guidance: Which one for your workflow?

As a developer who values deep technical context, I recommend **Aider** as your primary tool for local development with Qwen.

#### Why Aider over Claude Code for Local Models?

1. **Architect/Editor Pattern:** Aider can use a "weaker" local model (7B) for implementation while you provide the "architect" oversight, or it can use a "Diff" format that is much easier for a 7B model to generate than the complex XML/JSON blocks Claude Code expects.
2. **Git is the Undo Button:** Aider automatically commits every successful change. If the 7B model hallucinates or breaks a file, you simply `/undo`.
3. **Map Files:** It creates a "Repo Map" (a condensed CTags-based summary of your codebase) which allows the 7B model to understand your project structure without overflowing its context window.

#### How to launch Aider with your setup:

```
# No LiteLLM proxy needed; Aider speaks Ollama natively
aider --model ollama/qwen2.5-coder:7b
```

**Important Note on Qwen 7B:** While `qwen2.5-coder:7b` is the "gold standard" for its size, agentic tasks (like those in Claude Code) often fail because the model forgets to close a tag or misses a JSON comma. If you find it "hanging" or producing garbage, it's usually because the system prompt is too "loud" for a 7B parameter brain. In those cases, switching to **Aider's `--edit-format whole`** often solves the issue.

Does the `python -m litellm` command show the proxy starting up on port 4000 now?

---

**You**

Thanks for the comparison!

No! litellm cannot be executed:

PS C:\\Users\\molna> python -m litellm --model ollama/qwen2.5-coder:7b

C:\\Program Files\\Python311\\python.exe: No module named litellm.\_\_main\_\_; 'litellm' is a package and cannot be directly executed

Get me a step-by-step guide on how to create and run litellm in a Docker container on Windows. I have Docker desktop installed. The container name should be 'litellm-prox-local'

Also give me a README for later reference on how to setup and run local models from ollama

---

**Gemini**

The error you encountered is due to how the `litellm` package is structured in Python; it requires the `[proxy]` extra to run the server, and the entry point is often `litellm` rather than a runnable module. Using Docker is a much cleaner solution on Windows to avoid these environment and PATH headaches.

Here is your step-by-step guide to containerizing the proxy and a reference README for your Ollama workflow.

---

### Phase 1: Deploying the LiteLLM Proxy in Docker

To make this work, the Docker container needs to communicate "outward" to your Windows host where Ollama is running. In Docker Desktop for Windows, we use the special DNS name `host.docker.internal` to achieve this.

#### Step 1: Create a Configuration File

Create a file named `litellm_config.yaml` in a folder (e.g., `C:\Users\molna\litellm-proxy\`). This file tells the proxy to map "Claude" requests to your local Qwen model.

```
model_list:
  - model_name: "qwen2.5-coder:7b" # The name Claude Code will use
    litellm_params:
      model: "ollama/qwen2.5-coder:7b"
      api_base: "http://host.docker.internal:11434" # Connects to Windows host
```

#### Step 2: Launch the Container

Open PowerShell and navigate to the folder where you created the YAML file. Run the following command:

```
docker run -d \`
  --name litellm-prox-local \`
  -v "$(Get-Location)/litellm_config.yaml:/app/config.yaml" \`
  -p 4000:4000 \`
  -e LITELLM_MASTER_KEY="sk-1234" \`
  ghcr.io/berriai/litellm:main-latest \`
  --config /app/config.yaml
```

#### Step 3: Update Claude Code Environment

Now, point Claude Code to your new, stable proxy. Note that we use the **Master Key** defined in the Docker command.

```
$env:ANTHROPIC_BASE_URL = "http://localhost:4000"
$env:ANTHROPIC_API_KEY  = "sk-1234"
# Keep your other model overrides as they were
```

---

### Phase 2: Local LLM Setup & Maintenance README

Save this content as `OLLAMA_GUIDE.md` for your future reference.

## 🦙 Ollama Local Model Management

This guide covers the essential commands and best practices for managing local models for development and research.

## 1\. Core Commands

| Command | Action |
| --- | --- |
| `ollama pull [model]` | Downloads/updates a model from the library. |
| `ollama list` | Shows all currently installed models and their sizes. |
| `ollama ps` | Shows which models are currently loaded in VRAM. |
| `ollama rm [model]` | Deletes a model to free up disk space. |
| `ollama run [model]` | Starts an interactive chat session in the terminal. |

## 2\. Advanced Configuration (Modelfiles)

To customize a model (e.g., changing the system prompt or temperature), create a file named `Modelfile`:

```
FROM qwen2.5-coder:7b
PARAMETER temperature 0.1
SYSTEM "You are a specialist coding assistant focusing on clean, modular code."
```

Then create the custom version: `ollama create my-custom-qwen -f Modelfile`

## 3\. Performance & VRAM Tips

- **Quantization:** For 2026 hardware, **Q5\_K\_M** or **Q6\_K** are the "sweet spots." They offer near-native performance with significantly reduced VRAM usage.
- **Context Windows:** By default, some models initialize with a small context (2k-4k). For coding, you often need more. You can set this in your environment or Modelfile: `PARAMETER num_ctx 32768`
- **GPU Offloading:** If a model is slow, check `ollama ps`. If the "Processor" says `CPU`, the model is too large for your VRAM and is spilling over, which degrades speed by ~10x.

## 4\. Troubleshooting the Proxy

If Claude Code hangs again:

1. **Check Docker Logs:** `docker logs litellm-prox-local`
2. **Verify Host Access:** Ensure Ollama is listening on all interfaces. By default, it only listens to `127.0.0.1`. If Docker can't see it, set: `$env:OLLAMA_HOST = "0.0.0.0"` and restart the Ollama service.
3. **Test the Proxy Directly:**
	```
	curl http://localhost:4000/v1/models -H "Authorization: Bearer sk-1234"
	```

---

### Why this works

By moving to Docker, you've isolated the **API Translation Layer**. The LiteLLM container acts as a translator: it takes the "Claude-speak" (Anthropic Headers) and converts it into the "Ollama-speak" (OpenAI/Ollama format) that your Qwen model understands, solving the 25-second hang you experienced.