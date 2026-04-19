---
title: "GitHub Copilot Instructions Template"
source: "C:\\Users\\molna\\OneDrive\\Programolás\\Github Copilot\\copilot_instructions_template.txt"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Template prompt for creating a .github/copilot-instructions.md file for any software project"
tags:
  - clippings
---

# GitHub Copilot Instructions Template

> *Source content to be synced from OneDrive: `C:\Users\molna\OneDrive\Programolás\Github Copilot\copilot_instructions_template.txt`*
>
> This raw file is a placeholder. The full template content should be pasted here from the OneDrive source file.

## Overview

A reusable template for generating `.github/copilot-instructions.md` files for software projects. The template instructs an LLM agent on how to write context-rich Copilot instructions that cover:

- **Project overview** — purpose, tech stack, key architectural decisions
- **Coding conventions** — naming, formatting, patterns specific to the codebase
- **Key services and modules** — descriptions of major components so Copilot understands the architecture
- **Data flow** — how data moves through the system
- **Development workflows** — how to build, test, lint, and deploy
- **Testing guidelines** — what to test and how
- **DO / DON'T rules** — explicit guardrails for the agent
- **Environment variables** — required config with explanation of purpose

## Intended Use

Used as a starting prompt for Claude or Copilot to generate a project-specific `copilot-instructions.md` from an existing codebase or project description.
