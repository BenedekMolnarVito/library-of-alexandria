---
title: "Budget Tracker Mini Features & Bug Fixes"
source: "C:\\Users\\molna\\OneDrive\\Programolás\\simple_project_prompt.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Agentic prompt for implementing mini features and bug fixes for the Budget Tracker Android app"
tags:
  - clippings
---

# Implement a set of mini-features and fix bugs

## Planning
- Create an iterate over a plan before implementing.
- When creating a plan, create tasks for each requirement.
- Each task should be implemented by SUB-AGENTS, so make the task small enough to for LLM agents to handle but large enough to be meaningful.
- When creating tasks, ask the following questions:
	1. Is this task description unambiguous enough for implementation?
	2. Is the description get into technical details enough?
	3. Does the description highlight the business rationale?
	4. Are all related requirements described, including edge cases?

-----------------------------------------------------------------------------------
## Bugs to fix

### Duplicate entries
- **Problem**: Sometimes an entry is auto-added by Notification Listener multiple times. Sometimes just 2, but occasionally 5 times.
- **Suggestion**: Implement guardrails against multiple Transaction creation when catching Revolut notifications.

### Random shutdowns
- **Problem**: Sometimes Notification Listener does not auto-start. I regularly close all apps, to maintain clean memory, and after this, the permanent notification usually auto-restarts. Not always. Also: permanent notification usually does not auto-restart after turning on and off Flight Mode. 
- **Suggestion**: Check Android auto-killing processes, and guard the permanent notifications against them.

-----------------------------------------------------------------------------------
## New features and extensions of existing ones

### Parse and Show Transaction Amount on UI
- The Transaction amount is not shown anywhere in UI. Make a box for every entry on Home page with the Transaction Amount saved in DB.
- Parse numerical data from Revolut notifications and save as Amount. Try to parse currency too. Default currency is HUF.

### Auto-tag recurring vendors
- When at least one Transaction from a Vendor is already in the DB, assign the last set of Tags to the entry automatically. Also, mark the entry as completed (green in the list)
- Exception: *AddedManually* Tag should never be auto-assigned. It is reserved for User's manual entry adding.
- Also, keep track of recurring DELETED entries. If a message MATCHES EXACTLY one that was previously deleted (NOTE: SOFT DELETED), then soft-delete the new one automatically.

### Extend Tag Management
- Right now, only the 5 most recent tags are visible on the Transaction Editing page. This is good, BUT also implement a search-as-you-type dropdown for the input field that ranks ALL previous Tags that the user can choose from.
- Use Input Debouncer logic for avoiding too many DB calls too fast at first. User should type AT LEAST 2 characters before searching existing Tags.
- Thus, Tags should be in a many-to-many relationship with transactions.
- The 5 MOST COMMON should be always there (in the existing word cloud), but also bring up suggestions as user types into the tag input field.

### Flag Income and Expense
- All Transactions should be flagged as *Income* or *Expense*. DEFAULT: Expense.
- Expense Amounts should be shown in RED, and Income Amount should be DARK GREEN.

### Add a checkbox to Home page to see Soft Deleted entries
- A button should switch between displaying *all* and *IsDeleted = false* entries.
- Default display should NOT show soft-deleted transactions.

## Additional guidance
- AVOID overhauling existing functionalities. Prefer integrating new features into existing flows and conventions.
- When uncertain about an implementation detail, run a subagent to do a WEB SEARCH on the question, asking what is the most common solution, or best practice for the matter.
- Refer to .md documentation files for existing architecture/conventions/business logic.
