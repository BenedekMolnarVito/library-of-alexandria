---
title: "Tool Smithy MCP Project Brief"
source: "C:\\Users\\molna\\OneDrive\\Programolás\\Agentic\\MCP_prompt.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Project brief for Tool Smithy — a custom MCP server running in Docker for personal AI agent tooling"
tags:
  - clippings
---

# Project Brief: **Tool Smithy**

## My persona
- I am a mid-senior Python software engineer who loves automation and experimenting with new technologies.

## What I'm trying to solve

- I want to use my own MCP tools in Claude Code and other Agentic Frameworks. 
- I want my agents to interact with programs on my computer.
- I need a custom set of tools that I can extend/manage easily.

---

## What I need it to do

- Should be used in Docker MCP Toolkit.
- Should run in Docker itself.
- After the MCP server is added to my MCP Toolkit, Claude code and other Agentic Framework Apps should connect to it as clients.
- This Docker container should run on my Ubuntu Server and I should be able to connect to it remotely.
- Should be model agnostic

---

## Who will use this and how

- Only I will use it.
- I want to write custom tools (e.g. sticky-notes-summarize, browser-use, email-automation, file-organize) in Python.
- I want my Claude and other agents to be able to call these tools.
- I want it to run on a server so I can always use them from any machine.

---

## What I don't want

- Avoid subscription-based or expensive dependencies.
- Avoid an overengineered solution, just simple connection with Docker MCP Toolkit.
