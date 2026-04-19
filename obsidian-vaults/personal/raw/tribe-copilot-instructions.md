---
title: "Tribe Copilot Instructions"
source: "C:\\Users\\molna\\OneDrive\\Tribe\\copilot-instructions_verbose.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Verbose GitHub Copilot instructions for the Tribe app — architecture, key services, data flow, and development workflows"
tags:
  - clippings
---

# Tribe — GitHub Copilot Instructions

> Source: `C:\Users\molna\OneDrive\Tribe\copilot-instructions_verbose.md`

---

## Project Overview

**Tribe** is a social activity-matching mobile application built in React Native (Expo). Its core mission is to connect people around shared real-world activities — not profiles, not interests, but *specific, actionable moments*: "I want to go swimming at Palatinus on Saturday afternoon."

The app uses AI (Claude API) to:
1. Help users craft specific, time- and place-anchored prompts (the what/when/where validation system)
2. Match users based on semantic similarity of their activity prompts
3. Facilitate introductions and coordinate logistics

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Mobile | React Native (Expo SDK 51+) |
| Language | TypeScript (strict mode) |
| State management | Zustand + React Query |
| Backend | Node.js + Express (REST API) |
| Database | PostgreSQL + pgvector (embeddings) |
| AI/LLM | Anthropic Claude API |
| Auth | Clerk (OAuth + magic link) |
| Notifications | Expo Notifications + APNs/FCM |
| Storage | Expo SecureStore (tokens), AsyncStorage (preferences) |
| Testing | Jest + React Native Testing Library + Detox (E2E) |
| CI/CD | GitHub Actions |
| Deployment | Railway (backend), Expo EAS (mobile) |

---

## Repository Structure

```
tribe/
├── mobile/                    # React Native Expo app
│   ├── app/                   # Expo Router (file-based routing)
│   │   ├── (auth)/            # Authentication screens
│   │   ├── (tabs)/            # Main tab navigation
│   │   │   ├── home.tsx       # Activity feed
│   │   │   ├── prompt.tsx     # Prompt input screen
│   │   │   ├── matches.tsx    # Matches list
│   │   │   └── profile.tsx    # User profile
│   │   └── _layout.tsx
│   ├── src/
│   │   ├── components/        # Reusable UI components
│   │   ├── services/          # Business logic services
│   │   │   ├── promptAnalysis/ # Tier 1-5 what/when/where system
│   │   │   ├── matching/      # Match discovery service
│   │   │   └── notifications/ # Push notification service
│   │   ├── stores/            # Zustand stores
│   │   ├── hooks/             # Custom React hooks
│   │   ├── constants/         # Static data (ghost labels, nudge messages)
│   │   ├── utils/             # Pure utility functions
│   │   └── types/             # Shared TypeScript types
│   ├── assets/                # Images, fonts, ML models
│   └── __tests__/
├── backend/                   # Node.js Express API
│   ├── src/
│   │   ├── routes/            # API routes
│   │   ├── services/          # Business logic
│   │   ├── models/            # Database models (Prisma)
│   │   ├── middleware/        # Auth, validation, rate limiting
│   │   └── utils/
│   ├── prisma/
│   │   └── schema.prisma      # Database schema
│   └── __tests__/
└── shared/                    # Shared types between mobile and backend
    └── types/
```

---

## Key Services

### PromptAnalysisService (mobile/src/services/promptAnalysis/)

The what/when/where validation system. Five tiers from most to least intelligent:

- **Tier 1** (`ClaudeAPIClient.ts`): Claude API → full NL suggestions
- **Tier 2** (`StaticGuide.ts`): Static ghost label rotation
- **Tier 3** (`HybridNudgeService.ts`): SML classifier + static fallback
- **Tier 4** (`RegexValidator.ts`): Pure regex pattern matching
- **Tier 5** (`NERService.ts`): On-device DistilBERT NER

Active tier is controlled by `ACTIVE_VALIDATION_TIER` env var (default: 4 for MVP).

```typescript
// Usage
const analysis = await PromptAnalysisService.analyze(promptText, locale);
// Returns: { suggestions, missingDimensions, tier, confidence }
```

### MatchingService (mobile/src/services/matching/)

Finds compatible users based on semantic similarity of activity prompts:
1. Embed user prompt via Claude or local embedding model
2. Query pgvector (backend) for nearest neighbors within time/location window
3. Apply compatibility filters (mutual availability, distance, preferences)
4. Return ranked match list

### NotificationService (mobile/src/services/notifications/)

Handles:
- Match found notifications (push)
- Activity reminder notifications
- Background refresh for new matches

Uses Expo Notifications + backend scheduling via Bull queue.

---

## Data Flow: Prompt Submission

```
User types prompt
    → PromptInput (UI)
    → PromptAnalysisService.analyze() [on-device, per tier]
    → NudgeBanner shows if incomplete
    → User confirms/submits
    → PromptStore.submit(prompt)
    → Backend API: POST /prompts
    → Backend: embed prompt (Claude embeddings or local)
    → Store in PostgreSQL + pgvector index
    → Trigger async matching job (Bull queue)
    → Matching: query pgvector for similar prompts in time/location window
    → Create match records
    → Push notification to matched users
```

---

## Data Flow: Authentication

```
User opens app
    → Clerk auth check
    → If authenticated: load profile + active prompt
    → If not: redirect to (auth)/login
    → OAuth (Google/Apple) or magic link
    → Clerk issues session token
    → Token stored in SecureStore
    → All API calls include Bearer token
    → Backend validates via Clerk JWT middleware
```

---

## Database Schema (Key Tables)

```prisma
model User {
  id          String   @id @default(cuid())
  clerkId     String   @unique
  displayName String
  locale      String   @default("en")
  createdAt   DateTime @default(now())
  prompts     Prompt[]
  matches     Match[]
}

model Prompt {
  id          String   @id @default(cuid())
  userId      String
  text        String
  embedding   Float[]  // pgvector
  activityAt  DateTime // extracted WHEN
  location    String   // extracted WHERE (free text)
  lat         Float?
  lng         Float?
  isActive    Boolean  @default(true)
  expiresAt   DateTime
  createdAt   DateTime @default(now())
  user        User     @relation(fields: [userId], references: [id])
  matches     Match[]
}

model Match {
  id           String   @id @default(cuid())
  prompt1Id    String
  prompt2Id    String
  score        Float    // cosine similarity
  status       MatchStatus @default(PENDING)
  createdAt    DateTime @default(now())
}

enum MatchStatus {
  PENDING
  ACCEPTED
  DECLINED
  EXPIRED
}
```

---

## Development Workflows

### Setup
```bash
# Install dependencies
cd mobile && npm install
cd backend && npm install

# Environment
cp mobile/.env.example mobile/.env
cp backend/.env.example backend/.env
# Fill in: ANTHROPIC_API_KEY, DATABASE_URL, CLERK_SECRET_KEY

# Database
cd backend && npx prisma migrate dev

# Start development
cd mobile && npx expo start
cd backend && npm run dev
```

### Running Tests
```bash
# Mobile unit tests
cd mobile && npm test

# Mobile E2E (Detox)
cd mobile && npm run test:e2e

# Backend tests
cd backend && npm test
```

### Building for Production
```bash
# Backend (Docker)
cd backend && docker build -t tribe-backend .

# Mobile (EAS)
cd mobile && eas build --platform all --profile production
```

---

## Coding Conventions

### TypeScript
- Strict mode always on (`"strict": true` in tsconfig)
- No `any` — use `unknown` and narrow
- Prefer `interface` over `type` for object shapes
- Use `z.infer<typeof Schema>` for Zod-validated API responses

### React Native
- Expo Router for navigation (file-based)
- Zustand for global state, React Query for server state
- `StyleSheet.create()` for all styles (no inline styles in JSX)
- Functional components only (no class components)
- Custom hooks prefixed with `use` (e.g., `useMatchList`)

### API Design
- REST with standard HTTP verbs
- All responses: `{ data: T, error: string | null }`
- Pagination: cursor-based (`?cursor=&limit=`)
- Errors: always include `code` field for client-side handling

### Testing
- Unit: Jest + RNTL for components
- Integration: Supertest for API routes
- E2E: Detox for critical user flows
- Minimum coverage: 80% for services, 60% overall

---

## Environment Variables Reference

### Mobile (.env)
```env
EXPO_PUBLIC_API_URL=http://localhost:3000
EXPO_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
ANTHROPIC_API_KEY=sk-ant-...
ACTIVE_VALIDATION_TIER=4
NER_MODEL_PATH=assets/models/ner_model_v1.tflite
```

### Backend (.env)
```env
DATABASE_URL=postgresql://...
CLERK_SECRET_KEY=sk_test_...
ANTHROPIC_API_KEY=sk-ant-...
REDIS_URL=redis://localhost:6379
PORT=3000
NODE_ENV=development
```

---

## Important Rules for Copilot

### DO
- Always use TypeScript strict types — no `any`
- Use Zustand `create` with typed slices
- Handle all async operations with try/catch and user-facing error states
- Write tests for every new service function
- Use `StyleSheet.create()` for all RN styles
- Validate all API inputs with Zod schemas
- Check that NudgeBanner always has a dismiss/close mechanism

### DON'T
- Never store sensitive data in AsyncStorage (use SecureStore)
- Never call Claude API without checking `ACTIVE_VALIDATION_TIER` first
- Never skip the what/when/where validation before submitting a prompt
- Never use `console.log` in production code (use structured logger)
- Never hardcode strings visible to users — all go through i18n constants
- Never modify the pgvector index schema without a migration
- Never block the UI thread with synchronous NER inference

---

## Key Business Rules

1. A prompt is only eligible for matching if it has WHAT + WHEN + WHERE (all three dimensions)
2. Prompts expire after 7 days (configurable) or when the activity time passes
3. A user can only have 1 active prompt at a time (soft limit — warn, don't block)
4. Matches are bidirectional — both users must see and can accept/decline
5. Match score threshold for notification: cosine similarity > 0.75 (configurable)
6. Location matching radius: 50km default (configurable per user)
7. Time window for matching: ±48 hours around `activityAt`

---

## Known Technical Debt

- pgvector re-indexing on schema changes requires downtime (not yet solved)
- Tier 3 SML model not yet trained (falls back to Tier 4 regex)
- Tier 5 NER model in research phase (expected Q3 2026)
- Hungarian NER accuracy on locative case patterns needs improvement
- Push notification delivery rate not yet measured
