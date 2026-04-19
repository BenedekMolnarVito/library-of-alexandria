---
title: "Tribe Dev Spec — Tier 3: Hybrid Nudge"
source: "C:\\Users\\molna\\OneDrive\\Tribe\\dev specs\\Tier3_Hybrid_Nudge_Spec.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Developer specification for Tier 3 of the Tribe what/when/where validation system — SML model with static nudge fallback"
tags:
  - clippings
---

# Tribe Dev Spec — Tier 3: Hybrid Nudge

## Overview

Tier 3 combines a Small ML Model (SML) — specifically a lightweight on-device classifier — with a static nudge fallback. The SML classifies whether the prompt contains WHAT, WHEN, and WHERE components. If the SML is unavailable or confidence is low, a static nudge (Tier 2 text) is displayed. The key advantage over Tier 1 is offline capability and lower latency; the advantage over Tier 2 is personalized, prompt-aware feedback.

---

## Requirements

### Functional Requirements
- Classify user prompt for presence/absence of WHAT, WHEN, WHERE using an on-device SML
- If SML confidence < threshold (configurable, default 0.65): fall back to static nudge
- Display targeted nudge message based on which dimensions are missing
- Nudge message must be localized (English + Hungarian)
- Minimum prompt length before triggering: 8 characters
- Debounce: 600ms

### Non-Functional Requirements
- SML model size: < 5 MB (must not meaningfully increase app bundle)
- Inference latency: < 100ms on mid-range Android (Snapdragon 720G equivalent)
- Works fully offline
- Graceful degradation: if model fails to load → immediate Tier 2 fallback

---

## Architecture

```
UserPromptInput
    ↓ (debounced)
HybridNudgeService
    ├── SMLClassifier (on-device)
    │       ↓ (if confidence < threshold)
    └── StaticNudgeProvider (Tier 2 fallback)
            ↓
NudgeBanner (UI component)
```

### SMLClassifier

- Model type: TensorFlow Lite or ONNX (React Native compatible)
- Input: tokenized prompt (max 64 tokens, BPE tokenizer)
- Output: `{ what: float, when: float, where: float }` (probabilities 0.0–1.0)
- Training data: 2000–5000 labeled prompt examples (bootstrapped from Claude API outputs in Tier 1)
- Model file: `assets/models/prompt_classifier_v1.tflite`

### HybridNudgeService

```typescript
interface ClassificationResult {
  what: number;      // confidence 0.0–1.0
  when: number;
  where: number;
  usedFallback: boolean;
}

async function classifyPrompt(prompt: string): Promise<ClassificationResult>
```

- Loads model once at app startup (lazy + cached)
- Calls classifier; if `max(what, when, where) > threshold` → use SML result
- Otherwise → `usedFallback = true` → delegate to StaticNudgeProvider

### NudgeBanner

- Shows contextual message based on missing dimensions:
  - Missing WHERE → "Where will this happen?"
  - Missing WHEN → "When are you thinking?"
  - Missing WHAT → "What exactly do you want to do?"
  - Multiple missing → combined message

---

## Nudge Message Templates

```typescript
// src/constants/hybridNudge.ts

export const NUDGE_MESSAGES: Record<'en' | 'hu', NudgeMessages> = {
  en: {
    missingWhere: "📍 Where will this happen? (city, venue, neighbourhood)",
    missingWhen: "🕐 When are you thinking? (day, time of day)",
    missingWhat: "🎯 What exactly do you want to do?",
    missingWhenWhere: "🕐📍 Add when and where to help find the right match",
    missingWhatWhere: "🎯📍 What and where? Be more specific",
    missingAll: "💡 Try: 'I want to [activity] in [place] on [day]'",
    complete: null,  // No nudge when all dimensions present
  },
  hu: {
    missingWhere: "📍 Hol lesz? (város, helyszín, kerület)",
    missingWhen: "🕐 Mikor gondolod? (nap, napszak)",
    missingWhat: "🎯 Pontosan mit szeretnél csinálni?",
    missingWhenWhere: "🕐📍 Add meg, mikor és hol – segít megtalálni a legjobb matchet",
    missingWhatWhere: "🎯📍 Mi és hol? Légy pontosabb",
    missingAll: "💡 Próbáld így: '[tevékenység] [helyen] [napon]'",
    complete: null,
  },
};
```

---

## Model Training Pipeline

> Note: Training is a data science task, not a mobile dev task. Documented here for completeness.

1. Collect labeled data: 5000 prompts labeled `{what: 0|1, when: 0|1, where: 0|1}`
   - Bootstrap labels using Claude API (Tier 1) on user-provided prompt datasets
2. Tokenizer: BPE (sentencepiece), vocab size 8000, max length 64
3. Model architecture: 2-layer BiLSTM + linear head (3 sigmoid outputs)
4. Training: PyTorch → export to ONNX → convert to TFLite
5. Validation: F1 score per dimension ≥ 0.85 before shipping
6. Model versioning: `prompt_classifier_v{N}.tflite` — update via OTA asset update

---

## Environment Variables

```env
HYBRID_NUDGE_CONFIDENCE_THRESHOLD=0.65   # Optional. Default: 0.65
HYBRID_NUDGE_DEBOUNCE_MS=600             # Optional. Default: 600
SML_MODEL_PATH=assets/models/prompt_classifier_v1.tflite  # Optional
```

---

## Testing

### Unit Tests
- `SMLClassifier` — mock TFLite runtime, verify input preprocessing and output mapping
- `HybridNudgeService` — test fallback logic at various confidence levels
- `NudgeBanner` — snapshot tests for all nudge message combinations

### Integration Tests
- SML model loads successfully at startup
- Low-confidence prompt → static nudge appears
- High-confidence prompt with missing WHERE → WHERE nudge appears
- Complete prompt → no nudge displayed

### UI Behavior Tests (User Flow Scenarios)
1. Type "I want to play tennis" → after debounce → nudge: "📍 Where will this happen?"
2. Type "Going hiking on Sunday" → nudge: "📍 Where will this happen?"
3. Type "Swimming at Palatinus on Saturday afternoon" → no nudge (complete)
4. Model unavailable → static ghost labels from Tier 2 appear seamlessly
5. User changes language → nudge messages switch to new language

---

## File Structure

```
src/
  services/
    hybridNudge/
      HybridNudgeService.ts
      SMLClassifier.ts
      types.ts
  constants/
    hybridNudge.ts            # Nudge message templates
  components/
    NudgeBanner/
      NudgeBanner.tsx
      NudgeBanner.styles.ts
assets/
  models/
    prompt_classifier_v1.tflite
```

---

## Open Questions

- Should the SML model be shipped with the app or downloaded lazily on first use?
- What is the threshold strategy if the model reports medium confidence on all dimensions — should we show partial nudges?
- Who owns the model training pipeline? (data science team vs. mobile team)
- Should we log classification results (anonymized) for model improvement?
