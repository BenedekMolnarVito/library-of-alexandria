---
title: "Tribe Dev Spec Generator Prompt"
source: "C:\\Users\\molna\\OneDrive\\Tribe\\dev specs\\prompt.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Prompt for generating developer specifications for each Tier of the Tribe what/when/where validation system"
tags:
  - clippings
---

# Look at the PDF @"Options for what_when_where validation system.pdf" and create a developer specification for each Tiers.

## Goal
- Create a developer specification that can be used later as a reference to implement each of the Tiers in the PDF
- The LLM API will be Anthropic API, so the implementation will use anthropic SDK.
- Include requirements, dependencies, architectural decisions.

## Context
- The tiers will be implemented in a Mobile native application
- The business logic of the tiers are the same: as a user types a prompt in a field, suggestion should come up on how to improve the prompt by ensuring that the prompt includes answers for WHAT/WHEN/WHERE questions.

## Example
The user wants to prompt: "I wanna go squashing" -> this is too unspecific, only answers WHAT  
The app should provide suggestions like: "I wanna go squashing in Budapest tomorrow afternoon" -> now the prompt includes WHAT + WHEN and WHERE.

## Guidelines to follow
- You must adhere to the TIER DIRECTIONS provided in the PDF and ensure that the specifications are comprehensive and clear for developers to follow:
  1. **Claude API**: The implementation will utilize the Anthropic API, specifically the Claude model, to generate suggestions for improving user prompts.
  2. **Static Guide**: React Native constant state (Ghost Labels). Static text for the suggestions should be stored in a constant state.
  3. **Hybrid Nudge**: An SML with fallback to a static nudge.
  4. **Regex (Validator)**: Implement a regex-based validator to analyze user prompts.
