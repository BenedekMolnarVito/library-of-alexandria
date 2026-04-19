---
title: "Tribe Dev Spec — Tier 1: Claude API"
source: "C:\\Users\\molna\\OneDrive\\Tribe\\dev specs\\Tier1_Claude_API_Spec.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Developer specification for Tier 1 of the Tribe what/when/where validation system — Claude API implementation"
tags:
  - clippings
---

# Tribe Dev Spec — Tier 1: Claude API

## Overview

Tier 1 uses the Anthropic Claude API to provide intelligent, context-aware suggestions for improving user prompts. When a user types a prompt that lacks specificity in WHAT, WHEN, or WHERE dimensions, Claude generates natural language suggestions to enrich it.

---

## Requirements

### Functional Requirements
- Analyze user prompt text in real-time (debounced, not on every keystroke)
- Detect missing WHAT / WHEN / WHERE components
- Generate 1–3 natural-language suggestions to improve specificity
- Suggestions must be contextually appropriate and culturally aware (support Hungarian and English)
- Minimum input length before triggering: 10 characters
- Debounce delay: 800ms after last keystroke

### Non-Functional Requirements
- Response latency: < 2 seconds (p95)
- Must gracefully degrade to Tier 2 (static guide) on API failure
- Must not block the UI while waiting for API response
- Cost per suggestion call must be tracked and surfaced in admin dashboard

---

## Architecture

### Components
```
UserPromptInput (React Native TextInput)
    ↓ (debounced onChange)
PromptAnalysisService
    ↓
ClaudeAPIClient
    ↓
SuggestionDisplay (Ghost label / overlay)
```

### Service: PromptAnalysisService
- Accepts raw prompt string
- Calls `detectMissingDimensions(prompt)` → returns `{ what: bool, when: bool, where: bool }`
- If any dimension missing: calls Claude API
- Returns `SuggestionResult[]`

### Client: ClaudeAPIClient
- Wraps Anthropic SDK
- Model: `claude-3-haiku-20240307` (fast, cheap; configurable via env)
- Max tokens: 150
- Temperature: 0.3 (deterministic-ish suggestions)
- System prompt template stored in `prompts/tier1_system.txt`

---

## API Contract

### Request to Claude
```
System: You are a prompt improvement assistant for a social activity app. 
        Analyze the user's activity prompt and suggest improvements that add 
        specificity for WHAT activity, WHEN it will happen, and WHERE it will happen.
        Respond with JSON only: {"suggestions": ["...", "..."], "missing": ["what"|"when"|"where"]}

User: <user_prompt>
```

### Response Shape
```typescript
interface SuggestionResult {
  original: string;
  suggestions: string[];
  missingDimensions: ('what' | 'when' | 'where')[];
  tier: 'claude_api';
  tokensUsed: number;
  latencyMs: number;
}
```

---

## Cost Model

- Model: claude-3-haiku → ~$0.00025 per 1K input tokens, ~$0.00125 per 1K output tokens
- Avg call: ~100 input tokens + ~60 output tokens ≈ $0.00010 per suggestion
- Budget threshold: Alert if > $1/day per user (configurable)
- Implement token counter middleware to track usage

---

## Error Handling

| Scenario | Behavior |
|----------|----------|
| API timeout (>3s) | Fall back to Tier 2 static guide |
| API rate limit (429) | Exponential backoff (max 2 retries), then Tier 2 fallback |
| Invalid API key | Log error, disable Tier 1, show Tier 2 |
| Network offline | Immediate Tier 2 fallback |
| Malformed JSON response | Log warning, return empty suggestions |

---

## Environment Variables

```env
ANTHROPIC_API_KEY=sk-ant-...        # Required. Get from console.anthropic.com
CLAUDE_MODEL=claude-3-haiku-20240307 # Optional. Default: haiku
TIER1_DEBOUNCE_MS=800               # Optional. Default: 800
TIER1_MAX_TOKENS=150                # Optional. Default: 150
TIER1_TIMEOUT_MS=3000               # Optional. Default: 3000
```

### How to obtain ANTHROPIC_API_KEY
1. Sign up at https://console.anthropic.com
2. Navigate to API Keys → Create Key
3. Set usage limits to avoid unexpected charges
4. Add to `.env` file (never commit to version control)

---

## Testing

### Unit Tests
- `PromptAnalysisService.detectMissingDimensions()` — test with 20+ sample prompts
- `ClaudeAPIClient` — mock Anthropic SDK, test request formation and response parsing
- Error scenario tests — timeout, rate limit, malformed response

### Integration Tests
- End-to-end: user types prompt → suggestion appears within 2s
- Fallback: API unreachable → Tier 2 static guide renders within 100ms

### UI Behavior Tests (User Flow Scenarios)
1. User types "I want to go swimming" → suggestion appears with WHEN/WHERE additions
2. User types slowly (< debounce threshold) → no intermediate API calls fired
3. API is down → static guide appears without error flash to user
4. User selects a suggestion → prompt field updated, suggestion dismissed

---

## File Structure

```
src/
  services/
    promptAnalysis/
      PromptAnalysisService.ts
      ClaudeAPIClient.ts
      fallback.ts           # Tier 2 fallback logic
      types.ts
  prompts/
    tier1_system.txt        # System prompt template
  components/
    PromptInput/
      SuggestionOverlay.tsx
```

---

## Open Questions

- Should suggestion language match the user's input language automatically, or be set in user preferences?
- Should we store all prompts + suggestions for model fine-tuning later? (Privacy implications)
- Is Haiku fast enough or should we test Sonnet for quality comparison?
- Should cost tracking be per-user or aggregate?
