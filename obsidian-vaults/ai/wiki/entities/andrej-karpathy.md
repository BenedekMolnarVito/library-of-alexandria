---
title: "Andrej Karpathy"
type: entity
domain: ai
tags:
  - person
  - researcher
  - educator
  - openai
  - tesla
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-10x-claude-code-llm-wiki]]"
  - "[[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]"
  - "[[wiki/sources/karpathy-claude-md-file]]"
  - "[[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]]"
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
  - "[[wiki/sources/self-evolving-claude-code-memory-karpathy-llm-knowledge-bases]]"
  - "[[wiki/sources/300-dollars-auto-research-karpathy-loop]]"
  - "[[wiki/sources/claude-code-karpathy-obsidian-new-meta]]"
---

# Andrej Karpathy

Andrej Karpathy is one of the most influential AI researchers and educators of the current era — a co-founder of OpenAI, former Director of AI at Tesla, and now an independent researcher and content creator whose ideas on LLM-assisted knowledge management and agentic research loops have seeded an entire sub-ecosystem of tools and practices.

## Background / History

Karpathy completed his PhD at Stanford under Fei-Fei Li, where he developed foundational work in image captioning and convolutional neural networks. He joined OpenAI as a founding member before moving to Tesla to lead the Autopilot team's full-stack AI efforts, overseeing neural network training pipelines for autonomous driving at scale. After a return stint at OpenAI, he departed in 2023 to work independently, primarily producing educational content and publishing technical ideas via social media and long-form posts. He built and open-sourced projects like micrograd and nanoGPT, which have become canonical pedagogical resources for learning deep learning from first principles.

## Key Contributions / Features

Karpathy's most operationally impactful recent contributions are a set of conceptual patterns for working with LLMs that have inspired widespread adoption:

**The LLM Wiki Pattern**: Karpathy articulated the idea that a personal knowledge base maintained collaboratively with an LLM is analogous to a software project. His framing — "Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase" — recast note-taking and knowledge management as a programming discipline. The pattern involves ingesting raw sources, having the LLM generate structured wiki pages, and continuously refining the knowledge base through further LLM interaction. (Source: [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]])

**The Autoresearch Pattern**: Karpathy proposed a tight optimize-by-keep/discard loop where an LLM agent iteratively generates candidate outputs (e.g., research summaries, prompts, creative artifacts), evaluates them against a rubric, retains only the best, and continues. This pattern generalizes to any domain where quality can be scored — one practitioner, [[wiki/entities/nick-saraev]], applied it to text-to-image prompt optimization, reaching a score of 40/40 from 32/40 in 12 minutes. (Source: [[wiki/sources/karpathy-autoresearch-universal-skill]])

**The CLAUDE.md Pattern**: Karpathy observed that placing a structured instruction file (CLAUDE.md) at the root of a repository dramatically improves Claude Code's behavior — essentially giving the LLM persistent, project-specific context. This observation was distilled by [[wiki/entities/forrest-chang]] into a 60-line downloadable file that earned 3,500+ GitHub stars. (Source: [[wiki/sources/karpathy-claude-md-file]])

**The LLM OS Vision**: Karpathy has consistently articulated a vision of LLMs as operating-system-like substrates — coordinating memory, tools, and agents rather than acting as isolated question-answering systems. This framing underpins the entire agent-first development movement covered throughout this wiki.

## Role in AI Landscape

Karpathy occupies a rare position: he combines elite technical credibility (OpenAI founder, Tesla AI Director) with a gift for accessible explanation and a genuine curiosity that he shares openly. His ideas propagate unusually fast because they are simultaneously grounded in real engineering experience and easy for practitioners to implement immediately. The LLM wiki pattern alone spawned multiple open-source projects ([[wiki/entities/balu-kosuri]]'s llm-wiki-karpathy, [[wiki/entities/cole-medin]]'s context-portal), multiple build-along articles, and became "the new meta" for AI-assisted knowledge work. His autoresearch loop has been recognized as a general-purpose skill applicable far beyond AI research itself.

## Connections

- **Related entities**: [[wiki/entities/forrest-chang]], [[wiki/entities/balu-kosuri]], [[wiki/entities/cole-medin]], [[wiki/entities/nick-saraev]], [[wiki/entities/anthropic]], [[wiki/entities/openai]]
- **Key concepts**: [[wiki/concepts/llm-wiki-pattern]], [[wiki/concepts/autoresearch-loop]], [[wiki/concepts/claude-md-pattern]], [[wiki/concepts/llm-os-vision]], [[wiki/concepts/agentic-coding]]
- **Products**: [[wiki/entities/obsidian]], [[wiki/entities/claude-code]], [[wiki/entities/cursor]]
- **Sources**: [[wiki/sources/karpathy-10x-claude-code-llm-wiki]], [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]], [[wiki/sources/karpathy-claude-md-file]], [[wiki/sources/karpathy-llm-wiki-future-personal-knowledge]], [[wiki/sources/karpathy-autoresearch-universal-skill]], [[wiki/sources/300-dollars-auto-research-karpathy-loop]], [[wiki/sources/claude-code-karpathy-obsidian-new-meta]]
