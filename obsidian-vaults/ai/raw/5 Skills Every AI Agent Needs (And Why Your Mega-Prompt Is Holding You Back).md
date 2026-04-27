---
title: "5 Skills Every AI Agent Needs (And Why Your Mega-Prompt Is Holding You Back)"
source: "https://medium.com/@Micheal-Lanham/5-skills-every-ai-agent-needs-and-why-your-mega-prompt-is-holding-you-back-4b4ab2471c0e"
author:
  - "[[Micheal Lanham]]"
published: 2026-02-27
created: 2026-04-23
description: "5 Skills Every AI Agent Needs (And Why Your Mega-Prompt Is Holding You Back) The shift from monolithic prompts to modular skill architectures is the biggest unlock for production AI agents in 2026 …"
tags:
  - "clippings"
---
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*U8ElQhAQTNbV8N96meT9rw.png)

**The shift from monolithic prompts to modular skill architectures is the biggest unlock for production AI agents in 2026. Here’s how to make it work across any framework.**

Your agent’s system prompt is 50,000 tokens long. It carries every policy, every edge case, every workflow your organization has ever written down. And you’re paying for all of it on every single turn, whether the user asks about a refund policy or the weather.

This is the mega-prompt era. And it’s breaking.

Not slowly. Not gracefully. It’s breaking in the ways that hurt most: ballooning costs, degraded instruction-following, and mysterious failures where the model just… ignores the thing you told it to do on line 847.

There’s a better way. It’s called the Skills architecture, and it’s already converging across Claude, OpenAI Codex, GitHub Copilot, VS Code, and open-source frameworks like LangChain’s Deep Agents. The best part? You don’t need any specific vendor to use it.

**What You’ll Learn in This Article:**

- **The Mega-Prompt Problem**: Why stuffing everything into one giant system prompt is expensive, unreliable, and getting worse as agent capabilities grow
- **The Skills Architecture**: How a simple folder structure with progressive disclosure replaces monolithic prompts with modular, composable capabilities
- **Cross-Framework Implementation**: A concrete pattern for building a skills runtime in any agent framework, with a Pydantic AI walkthrough
- **Production Readiness**: Validation, monitoring, safety mitigations, and the governance model that makes skills a durable organizational asset
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*_15iIUidIGaAZYsmnJXy0g.png)

## The Mega-Prompt Problem Is Worse Than You Think

Let’s talk about what actually happens when you pile everything into one system prompt.

First, there’s the cost. Token billing is proportional to the text you send, so every instruction, every edge case, every “just in case” policy you add gets charged on every turn. That 50K-token system prompt isn’t a one-time investment. It’s a recurring tax on every interaction.

But cost isn’t even the scariest part.

The “lost-in-the-middle” effect, documented in research from Liu et al., shows that language models develop a U-shaped attention curve over long contexts. Instructions at the beginning and end get followed. Instructions buried in the middle? They get missed, under-weighted, or flat-out ignored.

Now add tool schemas to the mix. In a real-world example from Anthropic’s engineering team, 58 tools consumed roughly 55K tokens before the conversation even started. With additional MCP servers, tool-definition overhead can approach 100K+ tokens. That’s your entire context window eaten by capability descriptions before a single user message arrives.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*I9iT9VI12vqMYVh_0TrwvQ.png)

This diagram tells the whole story. Your agent is carrying a library on its back at all times, and it barely has room left to think.

The engineering lesson is clear: unnecessary tokens in context are not neutral. They consume budget, increase latency, and degrade instruction-following. We need a different architecture.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*dO4H8jItNRSpDPiA-ANkFg.png)

## Enter Skills: Progressive Disclosure for AI Agents

The fix isn’t to write better mega-prompts. It’s to stop writing mega-prompts entirely.

The Agent Skills architecture replaces one giant prompt with a library of modular capabilities, each packaged as a simple folder. The agent loads only what it needs, when it needs it. Think of it like the difference between carrying every book in the library versus carrying a card catalog and pulling books off the shelf when a topic comes up.

On disk, a skill is almost comically simple: a folder containing a required `SKILL.md` file with YAML frontmatter and a Markdown body. Optionally, you add `scripts/`, `references/`, and `assets/` directories for deeper resources.

```c
my-skill/
├── SKILL.md          # Required: instructions + metadata
├── scripts/          # Optional: executable helpers
│   └── validate.py
├── references/       # Optional: detailed docs, examples
│   └── api-guide.md
└── assets/           # Optional: templates, configs
    └── template.json
```

The YAML frontmatter requires just two fields: a `name` (kebab-case, matching the directory name) and a `description` explaining what the skill does and when to use it. That's the minimum viable skill.

But the real magic isn’t the format. It’s the loading strategy.

## The Three-Level Progressive Disclosure Model

This is the core architectural concept that makes skills work. Both the open specification at agentskills.io and Anthropic’s developer documentation describe the same three-level model.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*ObiGyaGp4yr0HDIFa_uUXA.png)

**Level One: Metadata.** At startup, the agent loads only the `name` and `description` fields from each skill. That's roughly 100 tokens per skill. Even with 50 skills in your library, you're looking at 5,000 tokens total for discovery. Compare that to 50,000+ tokens for a mega-prompt.

**Level Two: Instructions.** When the agent decides a skill is relevant to the current task, it loads the full body of `SKILL.md` into context. The spec recommends keeping this under 5,000 tokens and under 500 lines. Anything deeper gets pushed to referenced files.

**Level Three: Resources.** If the job requires detailed reference material, templates, or executable helpers, the agent loads files from `references/` or `assets/` and can run code from `scripts/`. This only happens when the instructions explicitly call for it.

The key constraint that makes this work: the spec instructs authors to keep file references “one level deep” from `SKILL.md`. No chains of nested retrieval. Progressive disclosure only works if the model can reliably find the next file when it needs it.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*R8ZcNft-yNF-IK7dTDF5zw.png)

## Why Skills Win in Practice

The architecture is elegant, but what does it actually buy you in production? Four things.

**Token efficiency that scales with relevance.** Instead of paying a permanent “organizational knowledge tax” on every request, you pay small discovery costs upfront and load deep instructions only when needed. A 50-skill library costs ~5K tokens for discovery. Loading one activated skill adds ~3–5K more. That’s 10K tokens versus 50K+ for the equivalent mega-prompt. On every turn.

**Composability.** Skills are designed to coexist. A “brand-voice” skill, a “security-review” skill, and a “release-notes” skill can be combined in different workflows without merging them into a single prompt blob. Anthropic’s guidance explicitly states that agents can load multiple skills simultaneously and that authors should write skills to work alongside each other, not assume exclusivity.

**Portability across frameworks and teams.** This is the part that surprises people. Agent Skills are not a Claude-only feature. The same folder structure with `SKILL.md` and YAML frontmatter is documented and supported across OpenAI's Codex, GitHub Copilot, VS Code agents, and LangChain's Deep Agents framework. The artifact you care about (the skill folder) is model-agnostic. Only the runtime policy (how discovery happens, what sandbox exists) ties it to a specific harness.

**Version control and governance.** File-based skills are naturally compatible with Git workflows. Code review, tagging, auditing, rollback. Your organization can treat procedural knowledge as a reviewed artifact rather than an informal behavior pasted into a UI.

## Building a Skills Runtime in Any Framework

Here’s where it gets practical. You don’t need a specific vendor’s SDK to implement skills. The generic algorithm is five steps, and it maps onto any agent framework.

Throughout the rest of this article, we’ll build a working skills runtime. We’ll start with a discovery registry, add activation logic, and finish with a complete integration pattern for Pydantic AI. By the end, you’ll have code you can adapt for your own agent stack.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*UmsdP1gT6uunTI32FUWXSg.png)

## Step 1: Skill Discovery

The first job is scanning directories for skills and parsing their metadata into a registry.

```c
import os
import yaml
from dataclasses import dataclass, field
from pathlib import Path

@dataclass
class SkillMetadata:
    name: str
    description: str
    path: Path
    metadata: dict = field(default_factory=dict)

class SkillRegistry:
    def __init__(self, skill_dirs: list[str]):
        self.skills: dict[str, SkillMetadata] = {}
        for directory in skill_dirs:
            self._scan_directory(Path(directory))
    
    def _scan_directory(self, base_path: Path):
        """Scan for */SKILL.md files and parse frontmatter."""
        for skill_dir in base_path.iterdir():
            skill_file = skill_dir / "SKILL.md"
            if skill_dir.is_dir() and skill_file.exists():
                meta = self._parse_frontmatter(skill_file)
                if meta:
                    meta.path = skill_dir
                    self.skills[meta.name] = meta
    
    def _parse_frontmatter(self, path: Path) -> SkillMetadata | None:
        """Extract YAML frontmatter from SKILL.md."""
        content = path.read_text()
        if not content.startswith("---"):
            return None
        _, fm, _ = content.split("---", 2)
        data = yaml.safe_load(fm)
        return SkillMetadata(
            name=data["name"],
            description=data["description"],
            path=path.parent,
            metadata=data.get("metadata", {})
        )
    
    def get_catalog(self) -> str:
        """Return compact catalog for model context (~100 tokens/skill)."""
        lines = []
        for skill in self.skills.values():
            lines.append(f"- {skill.name}: {skill.description}")
        return "\n".join(lines)
```

This gives us a registry that scans skill directories at startup and builds a compact catalog. Notice that `get_catalog()` returns only names and descriptions. That's Level 1: just enough for the model to know what's available.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*iFhXMIMz5PmQI7iZFzS4kA.png)

## Step 2: Skill Activation

With our registry in place, we can discover skills. But the agent needs a way to actually load one. Let’s add activation, which means reading the full `SKILL.md` body into context.

```c
class SkillRegistry:
    # ... previous methods ...
    
    def activate_skill(self, name: str) -> str:
        """Load full SKILL.md body (Level 2 activation)."""
        if name not in self.skills:
            raise ValueError(f"Unknown skill: {name}")
        
        skill = self.skills[name]
        content = (skill.path / "SKILL.md").read_text()
        
        # Strip frontmatter, return body only
        parts = content.split("---", 2)
        body = parts[2].strip() if len(parts) >= 3 else content
        return body
    
    def load_reference(self, name: str, ref_path: str) -> str:
        """Load a reference file from a skill (Level 3 resources)."""
        skill = self.skills[name]
        full_path = skill.path / ref_path
        
        # Safety: ensure path doesn't escape skill directory
        if not full_path.resolve().is_relative_to(skill.path.resolve()):
            raise ValueError("Reference path escapes skill directory")
        
        return full_path.read_text()
```

Now our registry handles all three levels. `get_catalog()` for discovery, `activate_skill()` for loading instructions, and `load_reference()` for pulling in deeper resources. Notice the path traversal check in `load_reference()`. Skills that bundle executable code introduce a supply-chain-like attack surface, and we need to be defensive from the start.

## Step 3: Wiring It Into Pydantic AI

With our discovery and activation logic ready, let’s wire this into a real agent framework. Pydantic AI’s tool registration and run graph introspection make it a natural fit.

```c
from pydantic_ai import Agent

# Initialize registry with your skill directories
registry = SkillRegistry(skill_dirs=["./skills", "./org-skills"])

# Create the agent with the skill catalog in its system prompt
agent = Agent(
    model="claude-sonnet-4-5-20250929",
    system_prompt=(
        "You are a helpful assistant with access to specialized skills.\n\n"
        "Available skills:\n"
        f"{registry.get_catalog()}\n\n"
        "When a user's request matches a skill, use the activate_skill "
        "tool to load its instructions before proceeding."
    ),
)

@agent.tool_plain
def activate_skill(name: str) -> str:
    """Load a skill's full instructions into context.
    Use when the user's request matches an available skill."""
    return registry.activate_skill(name)

@agent.tool_plain
def load_skill_reference(skill_name: str, ref_path: str) -> str:
    """Load a reference file from an activated skill.
    Only use when skill instructions direct you to a specific file."""
    return registry.load_reference(skill_name, ref_path)

@agent.tool_plain
def run_skill_script(skill_name: str, script_path: str, args: str = "") -> str:
    """Execute a script bundled with a skill.
    Only use when skill instructions explicitly require it."""
    import subprocess
    skill = registry.skills[skill_name]
    full_path = skill.path / script_path
    
    # Safety checks
    if not full_path.resolve().is_relative_to(skill.path.resolve()):
        return "Error: script path escapes skill directory"
    if not full_path.exists():
        return f"Error: script not found at {script_path}"
    
    result = subprocess.run(
        f"{full_path} {args}",
        shell=True, capture_output=True, text=True, timeout=30
    )
    return result.stdout or result.stderr
```

That’s the whole skills runtime. The agent starts with a lightweight catalog in its system prompt, uses `activate_skill` to load full instructions when needed, and can pull in references or run scripts for deeper tasks. Every piece builds on what came before.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*EPBuV5B3ZkBc4Imq1Ebj3Q.png)

## The Cross-Framework Story

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*tlerDhBzNO9YmfeYySblLA.png)

Here’s the key insight: this same pattern works everywhere. The discovery-activation-execution flow isn’t tied to Pydantic AI. LangChain’s Deep Agents describe the identical mechanism: frontmatter parsed at startup, full skill loaded on match. OpenAI’s Codex Skills documentation uses the same `SKILL.md` structure with the same progressive disclosure behavior.

Swap the `@agent.tool_plain` decorator for LangChain's `@tool`, or for OpenAI's function calling schema, or for a plain function in your custom framework. The skill folders don't change.

## Making Skills Production-Ready

Skills are powerful. They’re also code that influences agent behavior, which means they need the same rigor you’d apply to any production dependency.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*DWmOw_WwoQSIj8Wb-Fn4bw.png)

## Validation: What to Measure

Anthropic’s official guidance recommends three concrete success criteria that transfer to any framework:

**Activation accuracy.** Does the skill trigger on 90%+ of relevant queries? Test with 10–20 representative prompts and measure automatic activation versus manual invocation.

**Workflow efficiency.** Does the skill complete its task in a reasonable number of tool calls? Compare runs with and without the skill, tracking both quality and token consumption.

**Reliability.** Zero (or near-zero) failed tool calls per workflow. Track errors, retries, and fallback rates.

For framework-specific observability, Pydantic AI’s evaluation system supports span-based evaluation built on OpenTelemetry traces. This means you can evaluate internal agent behavior (tool calls, activation patterns, execution flow) rather than just final output. That’s exactly the kind of evaluation skills demand.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*W12WnBWRqgyZDCoYq1gEeQ.png)

## Safety: Skills Are Dependencies, Treat Them Like It

This is where a lot of teams get caught off guard. Because skills can bundle executable code in `scripts/` and can instruct agents to load additional resources, they introduce a supply-chain attack surface.

The research backs this up. A large-scale empirical study found that over 26% of analyzed skills contained at least one vulnerability pattern, including prompt injection, data exfiltration, and privilege escalation. Skills bundling executable scripts were 2.12x more likely to contain vulnerabilities than instruction-only skills.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*SMe1DMc7WoEIjLzJn0JhJw.png)

**Concrete mitigations:**

Use the spec’s experimental `allowed-tools` frontmatter to restrict which tools a skill can invoke. Don't grant broad execution powers when a skill only needs file reading.

Prefer deterministic scripts for critical validation steps. Anthropic’s guidance puts it well: code is deterministic while language interpretation is not. If a step must be reliable, make it a script.

Keep execution sandboxed. No network access, no runtime package installs in the skill execution environment.

Treat third-party skills like third-party dependencies. That means provenance tracking, code review, signing, and staged rollout from dev to staging to production.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*MOAJyJhQmSqsjxSC-RMQWw.png)

## The Future-Proofing Thesis

Here’s the bottom line on vendor lock-in, and it’s more optimistic than you might expect.

The skill folder format (directories + `SKILL.md` + optional resources) is explicitly standardized at agentskills.io. It's not hidden behind a proprietary UI. Multiple major platforms already converge on this exact artifact boundary. Claude, OpenAI Codex, GitHub Copilot, VS Code, and LangChain's Deep Agents all document the same structure.

So here’s the defensible thesis: **invest in skill folders as the durable unit of organizational agent knowledge.** Swap runtimes as needed. The model and agent harness will change, but your skill library is a versioned asset you can port, audit, and continuously improve.

The mega-prompt era gave us a way to get started. The skills era gives us a way to scale.

## Key Takeaways

**The mega-prompt ceiling is real.** Token costs scale linearly with prompt size, and the lost-in-the-middle effect means your carefully written instructions are being ignored. Progressive disclosure fixes both problems.

**Skills are just folders.** A `SKILL.md` with YAML frontmatter and a Markdown body. Optional scripts and references. That's it. The simplicity is the feature.

**The pattern is framework-agnostic.** Discovery, activation, execution. Five steps. Works in Pydantic AI, LangChain, OpenAI, or your custom stack. The skill folders are the portable artifact.

**Treat skills as production dependencies.** Validate activation accuracy, monitor token usage, sandbox execution, and review third-party skills the same way you review third-party code.

*What does your agent’s system prompt look like right now? Are you paying the mega-prompt tax? I’d love to hear how you’re thinking about modularizing your agent’s knowledge. Drop a comment or connect with me — let’s figure this out together.*

*If you found this useful, follow along for more deep dives on AI agent architecture, prompt optimization, and the patterns that actually work in production.*