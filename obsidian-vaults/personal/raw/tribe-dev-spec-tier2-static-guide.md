---
title: "Tribe Dev Spec — Tier 2: Static Guide"
source: "C:\\Users\\molna\\OneDrive\\Tribe\\dev specs\\Tier2_Static_Guide_Spec.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Developer specification for Tier 2 of the Tribe what/when/where validation system — static ghost label guide"
tags:
  - clippings
---

# Tribe Dev Spec — Tier 2: Static Guide

## Overview

Tier 2 is a zero-cost, zero-latency fallback (and standalone option) that uses static ghost labels — placeholder text rendered in the input field — to guide users toward including WHAT, WHEN, and WHERE in their prompts. No API calls, no ML inference; purely React Native constant state.

---

## Requirements

### Functional Requirements
- Display a ghost label (placeholder text) inside the prompt input field
- Ghost label cycles through example prompts that demonstrate WHAT + WHEN + WHERE specificity
- Examples must be available in English and Hungarian
- Ghost label disappears as soon as the user starts typing
- If prompt is cleared, ghost label reappears
- Ghost label should rotate on a timer (every 3–5 seconds) when the field is empty and focused

### Non-Functional Requirements
- Zero network dependency — works fully offline
- Zero latency — renders synchronously
- Accessible: ghost label must pass WCAG AA contrast ratio (≥ 4.5:1 against background)
- Bundle size impact: < 5 KB (strings only, no assets)

---

## Architecture

### Components

```
PromptInput (React Native TextInput)
    ↑ placeholder prop (animated)
GhostLabelProvider
    ↑
StaticGuideConstants (i18n strings)
```

### GhostLabelProvider
- Reads current language setting from app context
- Selects example array for the current locale
- Rotates through examples every 4 seconds using `setInterval`
- Exposes `currentGhostLabel: string` via React context

### StaticGuideConstants

```typescript
// src/constants/staticGuide.ts

export const GHOST_LABELS: Record<'en' | 'hu', string[]> = {
  en: [
    "e.g. I want to go swimming at Palatinus on Saturday afternoon",
    "e.g. Let's grab coffee in the 7th district tomorrow morning",
    "e.g. Looking for a tennis partner in Budapest this weekend",
    "e.g. Anyone up for hiking at Normafa next Sunday?",
    "e.g. I want to cook dinner with friends at home on Friday",
  ],
  hu: [
    "pl. Úszni szeretnék a Palatinuson szombat délután",
    "pl. Kávézzunk a 7. kerületben holnap reggel",
    "pl. Teniszpartnert keresek Budapesten ezen a hétvégén",
    "pl. Ki jönne túrázni a Normafára jövő vasárnap?",
    "pl. Pénteken főznék barátokkal otthon",
  ],
};
```

---

## State Management

```typescript
interface GhostLabelState {
  currentIndex: number;
  locale: 'en' | 'hu';
  isInputFocused: boolean;
  isInputEmpty: boolean;
}
```

- `currentIndex` increments every 4s when `isInputEmpty && isInputFocused`
- Timer clears on unmount and when field is not focused
- No persistence required — resets on every mount

---

## Styling

```typescript
const styles = StyleSheet.create({
  ghostLabel: {
    color: '#9CA3AF',          // Tailwind gray-400 equivalent
    fontStyle: 'italic',
    fontSize: 14,
  },
});
```

The ghost label must visually differ from user input text to avoid confusion. Use `placeholderTextColor` prop on `TextInput`.

---

## i18n / Localization

- Language is determined by app-level language context (not device locale)
- Add new locales by extending the `GHOST_LABELS` record
- All strings stored in `src/constants/staticGuide.ts` (single source of truth)
- No external i18n library required for this tier

---

## Environment Variables

None required for Tier 2.

---

## Testing

### Unit Tests
- `GhostLabelProvider` — verify rotation logic, locale switching, timer cleanup
- `StaticGuideConstants` — verify all locales have the same number of examples

### Integration Tests
- Render `PromptInput` empty → ghost label visible
- User types → ghost label hidden
- User clears → ghost label reappears
- Locale switch → ghost labels update to new language

### UI Behavior Tests (User Flow Scenarios)
1. User opens prompt field (empty) → ghost label "e.g. swimming at Palatinus..." visible
2. After 4 seconds of focus without typing → ghost label rotates to next example
3. User types "I want to go" → ghost label disappears immediately
4. User deletes all text → ghost label reappears (starts from first example)
5. User switches language to HU → Hungarian ghost labels appear

---

## File Structure

```
src/
  constants/
    staticGuide.ts          # All static ghost label strings
  context/
    GhostLabelContext.tsx   # Provider + hook
  components/
    PromptInput/
      GhostLabelInput.tsx   # TextInput with animated ghost label
```

---

## Open Questions

- Should the ghost label animate (fade in/out on rotation) or snap?
- Should examples be sourced from real anonymized past prompts eventually?
- Is 4s rotation too fast / too slow? Consider A/B testing.
