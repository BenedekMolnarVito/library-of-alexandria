---
title: "Cursor"
type: entity
domain: ai
tags:
  - product
  - ai-code-editor
  - vscode-fork
created: 2026-04-28
updated: 2026-04-28
sources:
  - "[[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]]"
  - "[[wiki/sources/karpathy-autoresearch-universal-skill]]"
---

# Cursor

Cursor is an AI-native code editor — a fork of VS Code with deep AI integration — that has become the dominant "AI-first IDE" for developers who want AI assistance beyond what VS Code extensions provide. It appears in the LLM wiki and autoresearch corpus primarily as the tool used by practitioners to build Karpathy-pattern implementations.

## Background / History

Cursor was built by Anysphere and launched in 2023. It started as a VS Code fork with tightly integrated AI features — multi-file context understanding, codebase-wide search, and AI-driven code generation — and has iterated rapidly to become the editor of choice for AI-native development among early adopters. Unlike VS Code + Copilot (where AI is an extension), Cursor integrates AI at the editor's core, enabling features like multi-file edits from a single prompt, automatic context injection from the codebase, and natural-language-driven refactoring.

Cursor occupies a different niche from [[wiki/entities/claude-code]]: where Claude Code is a terminal-based autonomous agent that works in any environment, Cursor is an interactive editor that augments a human developer's workflow. The two are complementary rather than competing: developers often use both, reaching for Claude Code for autonomous multi-step tasks and Cursor for interactive, human-in-the-loop development.

## Key Contributions / Features

**VS Code Compatibility**: Being a VS Code fork, Cursor supports all VS Code extensions, themes, and keybindings, dramatically lowering the switching cost for VS Code users. The transition is a matter of installing Cursor rather than learning a new tool from scratch.

**Multi-File Context**: Cursor's AI features are designed with multi-file context in mind — it can reference files across the codebase, understand project structure, and generate changes that span multiple files coherently. This is essential for real-world development tasks where a single logical change touches many files.

**LLM Wiki Built in 3 Prompts**: [[wiki/entities/balu-kosuri]] documented building an open-source LLM wiki implementation using Cursor in just three prompts — illustrating how AI-assisted development in a context-aware editor can collapse multi-step implementation tasks into a handful of high-level instructions. (Source: [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]])

**Autoresearch Use**: Cursor also appears in the autoresearch pattern documentation, used as the implementation environment for the optimize-by-keep/discard loop. (Source: [[wiki/sources/karpathy-autoresearch-universal-skill]])

**Cursor Extension for CLAUDE.md Pattern**: [[wiki/entities/forrest-chang]]'s andrej-karpathy-skills repository includes a Cursor extension alongside the VS Code extension, making the CLAUDE.md pattern available to Cursor users with a single install.

## Role in AI Landscape

Cursor represents the "AI-first IDE" thesis — the argument that the future of interactive coding is an editor where AI is the primary interface rather than an overlay. Its rapid growth and practitioner enthusiasm suggest it has found genuine product-market fit for developers who want more than autocomplete. As the distinction between interactive AI-assisted development (Cursor's domain) and autonomous agentic coding ([[wiki/entities/claude-code]]'s domain) becomes clearer, Cursor is well-positioned as the complement to autonomous tools for tasks where human judgment should remain in the loop.

## Connections

- **Related entities**: [[wiki/entities/claude-code]], [[wiki/entities/balu-kosuri]], [[wiki/entities/forrest-chang]], [[wiki/entities/andrej-karpathy]], [[wiki/entities/steve-yegge]]
- **Key concepts**: [[wiki/concepts/agentic-coding]], [[wiki/concepts/ai-native-ide]], [[wiki/concepts/claude-md-pattern]], [[wiki/concepts/llm-wiki-pattern]]
- **Sources**: [[wiki/sources/karpathy-llm-wiki-self-maintaining-knowledge-base]], [[wiki/sources/karpathy-autoresearch-universal-skill]]
