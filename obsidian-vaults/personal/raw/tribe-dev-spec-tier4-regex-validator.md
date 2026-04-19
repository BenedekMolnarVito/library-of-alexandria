---
title: "Tribe Dev Spec — Tier 4: Regex Validator"
source: "C:\\Users\\molna\\OneDrive\\Tribe\\dev specs\\Tier4_Regex_Validator_Spec.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Developer specification for Tier 4 of the Tribe what/when/where validation system — regex-based prompt validator"
tags:
  - clippings
---

# Tribe Dev Spec — Tier 4: Regex Validator

## Overview

Tier 4 implements a deterministic, rule-based validator using regular expressions to analyze user prompts for WHAT, WHEN, and WHERE completeness. No ML, no API, no assets — pure string matching. This is the most lightweight, most predictable, and most transparent tier. Particularly useful as a local pre-filter before invoking Tier 1 (Claude API) to avoid unnecessary API calls.

---

## Requirements

### Functional Requirements
- Analyze a prompt string and return which of WHAT / WHEN / WHERE are present
- Use regex patterns to detect:
  - **WHAT**: activity verbs and activity nouns (swimming, hiking, coffee, tennis, etc.)
  - **WHEN**: temporal expressions (tomorrow, next week, Monday, 3pm, weekend, etc.)
  - **WHERE**: location expressions (in Budapest, at Palatinus, 7th district, etc.)
- Return a validation result with per-dimension boolean and a confidence score (0.0–1.0 based on pattern match quality)
- Support English and Hungarian pattern sets
- Trigger on: prompt length ≥ 5 characters, no debounce (synchronous)

### Non-Functional Requirements
- Pure synchronous function — no async, no side effects
- Zero dependencies (no external regex libraries)
- Testable: each pattern group must have unit tests with ≥ 30 positive and 10 negative examples
- Execution time: < 5ms for any input ≤ 500 characters

---

## Architecture

```
userPromptText: string
    ↓
RegexValidator.validate(prompt, locale)
    ↓
ValidationResult { what, when, where, confidence }
    ↓
NudgeDisplay / API gate (Tier 1 pre-filter)
```

### RegexValidator

```typescript
interface ValidationResult {
  what: boolean;
  when: boolean;
  where: boolean;
  whatConfidence: number;    // 0.0–1.0
  whenConfidence: number;
  whereConfidence: number;
  overallConfidence: number; // average of present dimensions
  matchedPatterns: {
    what?: string;
    when?: string;
    where?: string;
  };
}

function validate(prompt: string, locale: 'en' | 'hu'): ValidationResult
```

---

## Pattern Definitions

### WHAT Patterns (English)

```typescript
const WHAT_PATTERNS_EN = [
  // Activity verbs
  /\b(go|going|want to|wanna|looking for|up for|keen on)\s+(swim|swimming|hike|hiking|run|running|cycle|cycling|play|playing|cook|cooking|eat|eating|drink|drinking|meet|meeting|watch|watching|study|studying|work|working)/i,
  // Direct activity nouns
  /\b(tennis|squash|swimming|hiking|running|cycling|yoga|gym|coffee|lunch|dinner|drinks|cinema|movie|concert|football|basketball|volleyball|chess|poker)\b/i,
  // "I want to X" pattern
  /\bI (want|wanna|would like|am looking) to \w+/i,
];
```

### WHEN Patterns (English)

```typescript
const WHEN_PATTERNS_EN = [
  // Specific days
  /\b(monday|tuesday|wednesday|thursday|friday|saturday|sunday)\b/i,
  // Relative time
  /\b(today|tonight|tomorrow|this (morning|afternoon|evening|night|weekend|week)|next (week|weekend|monday|tuesday|wednesday|thursday|friday|saturday|sunday))\b/i,
  // Time of day
  /\b(morning|afternoon|evening|night|noon|midnight|lunchtime|after work|after school)\b/i,
  // Clock times
  /\b(\d{1,2}(:\d{2})?\s*(am|pm|o'clock))\b/i,
  // Fuzzy temporal
  /\b(soon|later|eventually|sometime|this month|next month)\b/i,
];
```

### WHERE Patterns (English)

```typescript
const WHERE_PATTERNS_EN = [
  // "in [Place]" / "at [Place]"
  /\b(in|at|near|around|by)\s+[A-Z][a-z]+/,
  // Hungarian-style location (works for mixed EN/HU)
  /\b(Budapest|Pest|Buda|Óbuda|district|kerület|utca|tér|park|lake|river)\b/i,
  // Venue types
  /\b(gym|pool|park|cafe|coffee shop|restaurant|bar|court|stadium|track|office|home|my place|your place|library|university|campus)\b/i,
  // "downtown", "city centre" etc.
  /\b(downtown|city center|city centre|suburbs|outskirts|neighbourhood|area)\b/i,
];
```

### Hungarian Pattern Sets

```typescript
const WHAT_PATTERNS_HU = [
  // Activity verbs in Hungarian
  /\b(úszni|futni|kirándulni|teniszezni|kávézni|ebédelni|vacsorázni|főzni|nézni|találkozni|játszani|sportolni|edzeni)\b/i,
  // "szeretnék X-ni" pattern
  /\bszeretnék\s+\w+ni\b/i,
  // "menjünk X-ni"
  /\b(menjünk|gyerünk|mennénk)\s+\w+ni\b/i,
];

const WHEN_PATTERNS_HU = [
  // Days in Hungarian
  /\b(hétfőn|kedden|szerdán|csütörtökön|pénteken|szombaton|vasárnap)\b/i,
  // Relative time in Hungarian
  /\b(ma|ma este|holnap|holnap reggel|holnap délután|holnap este|hétvégén|jövő héten|ezen a héten)\b/i,
  // Time of day in Hungarian
  /\b(reggel|délelőtt|délben|délután|este|éjjel|éjszaka)\b/i,
];

const WHERE_PATTERNS_HU = [
  // "Budapesten", "a Palatinuson" etc. (locative case)
  /\b\w+(ban|ben|on|en|ön|nál|nél|ra|re|ba|be)\b/i,
  // Known Budapest locations
  /\b(Budapest|Buda|Pest|Óbuda|Margitsziget|Normafa|Palatinus|Városliget|Tabán|Keleti|Nyugati|Deli)\b/i,
  // Venue types in Hungarian
  /\b(uszoda|park|kávézó|étterem|bár|pálya|stadion|terem|iroda|otthon|könyvtár|egyetem|campus)\b/i,
];
```

---

## Confidence Scoring

Each dimension receives a confidence score based on pattern match quality:

| Match Type | Confidence |
|------------|-----------|
| Named specific location (e.g. "Palatinus") | 0.95 |
| Venue type (e.g. "pool") | 0.80 |
| Locative preposition + noun | 0.70 |
| Generic location term | 0.55 |
| No match | 0.0 |

Overall confidence = average of non-zero dimension scores.

---

## Usage as Tier 1 Pre-Filter

```typescript
// Before calling Claude API:
const validation = RegexValidator.validate(prompt, locale);

if (validation.what && validation.when && validation.where) {
  // Prompt is complete — no API call needed
  return { suggestions: [], isComplete: true };
}

if (validation.overallConfidence > 0.8) {
  // High confidence regex result — use targeted static nudge (Tier 2)
  return StaticNudgeProvider.getTargetedNudge(validation);
}

// Low confidence — call Claude API (Tier 1)
return ClaudeAPIClient.getSuggestions(prompt);
```

---

## Environment Variables

None required. All patterns are compile-time constants.

---

## Testing

### Unit Tests (minimum coverage)
- WHAT detection: 30 positive, 10 negative examples per language
- WHEN detection: 30 positive, 10 negative examples per language
- WHERE detection: 30 positive, 10 negative examples per language
- Confidence scoring: verify score ranges and relative ordering
- Edge cases: empty string, single word, very long prompt (> 200 chars)

### Integration Tests
- `validate()` returns correct result for 50 real-world prompt samples
- Regex pre-filter correctly suppresses Tier 1 API calls for complete prompts
- False positive rate < 10% (complete prompt incorrectly flagged as incomplete)

### UI Behavior Tests
1. Complete prompt → no nudge, no API call
2. Prompt with missing WHERE → WHERE nudge immediately (no debounce)
3. Regex correctly identifies Hungarian temporal expressions

---

## File Structure

```
src/
  services/
    regexValidator/
      RegexValidator.ts
      patterns/
        en.ts           # English pattern sets
        hu.ts           # Hungarian pattern sets
        index.ts        # Locale-aware pattern loader
      types.ts
  __tests__/
    regexValidator/
      what.test.ts
      when.test.ts
      where.test.ts
      integration.test.ts
```

---

## Open Questions

- Should regex patterns be loaded from a config file (allowing OTA updates) or compiled into the bundle?
- How do we handle mixed-language prompts (e.g. Hunglish)?
- Should false positive / false negative rates be reported to analytics for pattern improvement?
- Is the locative case regex for Hungarian too broad (matching non-location words with -ban/-ben suffixes)?
