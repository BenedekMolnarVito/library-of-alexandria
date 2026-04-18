---
title: "Context Portability"
type: concept
domain: ai
tags:
  - agent-memory
  - portability
  - vendor-lock-in
  - markdown
  - agent-patterns
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/anthropic-openai-memory-context-portability]]"
---

# Context Portability

Context portability is the ability to move an AI agent's accumulated context — memory, instructions, knowledge, and identity — between different tools and providers without loss. In practice, it is the difference between owning your accumulated AI context and being a tenant in a platform's memory system. Plain markdown files (CLAUDE.md, SOUL.md, LLM wikis) are the primary architectural mechanism for achieving portability: they work with any tool that can read a file, require no proprietary format, and are controlled entirely by the user.

## Definition

Every AI agent session accumulates context: learned preferences, project history, decision rationale, domain knowledge, and relationship-specific understanding. The portability question is: does this accumulated context belong to the user or to the platform?

In a platform-owned memory model (OpenAI's memory feature, for example), the context is stored in the provider's infrastructure. It may be accessible via API, but it is formatted for that platform's use, depends on that platform's memory retrieval algorithms, and cannot trivially be moved to a different tool. The user is a tenant.

In a file-owned memory model, the context lives in markdown files in the user's repository. Any tool that can read those files — Claude Code, GitHub Copilot, Cursor, Cline, a Python script — can use the accumulated context. Switching tools costs nothing in accumulated knowledge. The user is the owner.

## How It Works

The practical implementation of context portability is straightforward: all persistent agent context lives in files in the project repository.

- **[[claude-md]]** stores project instructions and behavioral constraints
- **[[soul-md]]** stores accumulated relationship context and agent identity
- **[[skill-md]]** stores task-specific expertise
- **[[llm-wiki]]** stores accumulated domain knowledge

These files are plain markdown, version-controlled with git, readable by humans and any LLM. When the user switches tools, they simply point the new tool at the same repository. The accumulated context is immediately available.

The key engineering discipline is ensuring that context accumulation writes to files, not to platform memory. An agent that updates SOUL.md at session end is building portable context. An agent that relies on the platform's memory system is building locked context, even if the platform provides a good memory experience today.

## Why It Matters

The AI tooling landscape is changing rapidly. Tools that are best-in-class today may be superseded next quarter. A user who has accumulated six months of agent context in a platform-owned memory system faces a genuine switching cost — not just the friction of learning a new tool, but the loss of accumulated value. This risk is asymmetric: platforms benefit from lock-in; users bear its cost.

Context portability is therefore a form of optionality: by keeping context in files, the user preserves the right to switch tools without paying a knowledge tax. As frontier models commoditize, the accumulated context (which model understands my project, my preferences, my goals) may become more valuable than the specific model or tool providing it.

The [[llm-wiki]] is the most complete expression of context portability for knowledge work: the accumulated knowledge is a git repository of markdown files, readable by any LLM, browsable by any Markdown editor, searchable by any grep tool. It is maximally portable almost by definition.

## In Practice

Context portability also enables **multi-tool workflows**: the same CLAUDE.md can be read by Claude Code for implementation tasks and by GitHub Copilot for code review. The same wiki can be queried by different agents for different purposes. Portability is not just about switching tools but about using multiple tools simultaneously without maintaining separate context for each.

The tradeoff is maintenance discipline: portable context requires the agent (and sometimes the human) to write to files deliberately. Platform memory systems handle this automatically. The choice is between the convenience of automatic memory and the freedom of portable memory — and for any work that might span multiple tools or accumulate value over months, portability is usually the right choice.

## Related Concepts

- [[wiki/concepts/agent-memory]] — the broader problem context portability addresses
- [[wiki/concepts/claude-md]] — project-level portable context
- [[wiki/concepts/soul-md]] — identity-level portable context
- [[wiki/concepts/llm-wiki]] — knowledge-level portable context
- [[wiki/concepts/markdown-first-architecture]] — why plain markdown is the portability medium

## Key Entities

- [[wiki/entities/anthropic]] — memory architecture philosophy
- [[wiki/entities/openai]] — contrasting memory-as-service approach
- [[wiki/entities/nate-b-jones]] — context portability advocate

## Sources

- [[wiki/sources/anthropic-openai-memory-context-portability]]
