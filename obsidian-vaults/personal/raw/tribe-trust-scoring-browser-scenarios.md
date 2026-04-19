---
title: "Tribe Trust Scoring Phase 1 — Browser User Scenarios"
source: "C:\\Users\\molna\\OneDrive\\Programolás\\Agentic\\trust_scoring_phase1_browser_user_scenarios.md"
author: "Molnár Benedek"
published: ""
created: 2025-06-10
description: "Browser-verifiable user scenarios for Tribe's MVP Trust System — leave/rating/report flows"
tags:
  - clippings
---

# Trust Scoring Phase 1 - Browser User Scenarios

This document defines browser-verifiable user scenarios for the MVP Trust System. It is based on the detailed Phase 1 trust-system description, but written against the current web UI so an agent can execute the flows through the browser without relying on hidden backend state.

## Goal

Cover browser-visible flows for:

- happy path behavior
- error cases
- edge cases in business logic

## Browser Verification Scope

These scenarios focus on outcomes visible in the web UI.

- Use the user-facing web app for conversation, leave, rating, and report flows.
- Use the admin web UI for moderation verification.
- Treat hidden trust score changes, penalties, and trust-event writes as out of scope for browser-only verification unless an admin screen exposes the result indirectly.

## Current UI Anchors

Use these visible routes and labels during browser automation:

- User app chat options button: `⋮`
- Chat actions: `Leave Conversation`, `Report User`
- Rating modal title: `How was this interaction?`
- Rating choices: `Awful`, `Not great`, `Okay`, `Good`, `Great`
- Rating dismiss action: `Skip`
- Report modal title: `Report User`
- Report submit action: `Submit Report`
- Report success copy: `Thanks` and `Our moderation team will review this.`
- Admin login route: `/admin/login`
- Admin reports route: `/admin/reports`
- Admin moderation actions: `Validate (Penalize User)` and `Reject (No Penalty)`

## Test Data Assumptions

Prepare the following before browser execution:

- User A and User B can log into the web app.
- Admin credentials exist for `/admin/login`.
- At least one connection can be created and accepted between User A and User B.
- Some scenarios require seeded message counts.

Recommended conversation fixtures:

- Fixture F1: accepted connection with 3 or more total messages
- Fixture F2: accepted connection with fewer than 3 total messages
- Fixture F3: accepted connection with enough duration and messages to qualify as a normal leave
- Fixture F4: accepted connection that will be reported from User A against User B

## Notes On Scope Differences

The original MVP description mentions rating after natural conversation end, handshake end, or match close. The current browser-verifiable implementation exposes rating most clearly after the user explicitly leaves an eligible conversation. These scenarios document what can be verified today in the UI.

The original MVP description also frames reporting as moderation-driven trust impact. In the current UI, the browser-visible effect is immediate loss of messaging access for the reporting flow, while the actual trust effects remain backend-only.

## Happy Path Scenarios

### HP-01: Leave Eligible Conversation And Submit Positive Rating

Purpose: verify the main leave-plus-rating flow for a conversation that meets the rating threshold.

Preconditions:

- User A and User B have an accepted connection using Fixture F1.
- The chat contains at least 3 total messages.

Steps:

1. Log in as User A.
2. Open the accepted conversation with User B.
3. Confirm the `⋮` chat options button is visible.
4. Open the options menu.
5. Click `Leave Conversation`.
6. Confirm the leave action in the browser alert.
7. Wait for the rating modal with `How was this interaction?` to appear.
8. Click the `Great` rating option.

Expected browser-visible results:

- The conversation input is replaced by `This conversation has ended.`
- The rating modal appears after the leave flow.
- A success state appears with `Thanks for your feedback!`.
- The rating modal closes automatically.
- Reopening the ended conversation does not show the rating prompt again.

Business logic covered:

- leave action ends the conversation
- rating is available only when the minimum message threshold is met
- one rating submission per conversation participant

### HP-02: Report User With Description And Validate In Admin

Purpose: verify the full report flow from user submission to admin validation.

Preconditions:

- User A and User B have an accepted connection using Fixture F4.
- User A can open the active chat with User B.

Steps:

1. Log in as User A.
2. Open the accepted conversation with User B.
3. Open the `⋮` chat options menu.
4. Click `Report User`.
5. In the `Report User` flow, choose `Harassment`.
6. Enter a short description in `Additional context...`.
7. Click `Submit Report`.
8. Wait for the confirmation state with `Thanks` and `Our moderation team will review this.`.
9. Log in as admin at `/admin/login`.
10. Open `/admin/reports`.
11. Open the newly created report from the pending list.
12. Confirm the detail page shows category, reporter, reported user, and conversation context.
13. Click `Validate (Penalize User)`.

Expected browser-visible results:

- User A sees report confirmation.
- The conversation becomes unavailable for further messaging after report submission.
- The report appears in the admin pending list.
- The report detail page shows the conversation transcript.
- After validation, the report no longer behaves like a pending item.
- Returning to the pending filter no longer shows that report.

Business logic covered:

- report submission creates a moderation item
- reporting ends or blocks normal chat interaction for the reporter flow
- admin moderation can validate a pending report exactly once

### HP-03: Report User Without Description And Reject In Admin

Purpose: verify the optional-description branch of the report flow.

Steps:

1. Log in as User A.
2. Open the accepted conversation.
3. Open `⋮` and click `Report User`.
4. Choose `Spam`.
5. Leave the description field empty.
6. Click `Submit Report`.
7. Log in as admin.
8. Open the corresponding report in `/admin/reports`.
9. Confirm the report detail page renders without a description block.
10. Click `Reject (No Penalty)`.

Expected browser-visible results:

- The report can be submitted without extra text.
- The confirmation screen still appears.
- The admin detail page remains readable when no description is provided.
- After rejection, the report disappears from the pending filter and appears under rejected.

Business logic covered:

- report description is optional
- moderation supports rejection as a first-class outcome

## Error Case Scenarios

### ER-01: Rating Is Not Offered For Short Conversation

Purpose: verify the minimum-message guard for rating.

Preconditions:

- User A and User B have an accepted connection using Fixture F2.
- The chat contains fewer than 3 total messages.

Steps:

1. Log in as User A.
2. Open the accepted conversation.
3. Open `⋮` and click `Leave Conversation`.
4. Confirm the leave action.
5. Observe the chat state for 5 to 10 seconds.

Expected browser-visible results:

- The conversation ends.
- The rating modal does not appear.
- The UI does not offer any alternate rating control for that ended conversation.

Business logic covered:

- rating cannot be submitted when the conversation is below the minimum threshold

### ER-02: Invalid Admin Login Shows Clear Error

Steps:

1. Open `/admin/login`.
2. Enter an invalid email and password.
3. Submit the form.

Expected browser-visible results:

- The login page stays open.
- A visible error appears: `Invalid email or password.` or `This account does not have admin access.`
- The browser is not redirected to `/admin/reports`.

### ER-03: Moderated Report Cannot Be Moderated Again From Detail Page

Steps:

1. Log in as admin.
2. Open the reviewed report detail page directly.

Expected browser-visible results:

- The report detail page shows its final status.
- The `Validate (Penalize User)` button is absent.
- The `Reject (No Penalty)` button is absent.

### ER-04: Empty Report Filter Shows Empty State Instead Of Broken Table

Steps:

1. Log in as admin.
2. Open `/admin/reports`.
3. Click a status filter that has no matching reports.

Expected browser-visible results:

- The table is replaced by an empty-state panel.
- The page shows `No reports found`.
- The page shows `There are no reports matching the current filter.`

## Edge Case Scenarios

### EC-01: Other Participant Sees Leave Outcome In Chat History

Steps:

1. Log in as User A in one browser session.
2. Log in as User B in a second browser session.
3. User A leaves the conversation.
4. User B opens or refreshes the same conversation.

Expected browser-visible results:

- User B sees a system-style message that the other user left the conversation.
- User B sees `This conversation has ended.` in place of the active message composer.
- User B cannot continue messaging in that conversation.

### EC-02: Skip Rating Dismisses Prompt Without Error

Steps:

1. Trigger the rating modal from an eligible conversation.
2. Click `Skip`.
3. Reopen the same ended conversation.

Expected browser-visible results:

- The rating modal closes without an error message.
- The chat remains ended.
- The rating modal does not reappear for the same conversation in the same verification session.

### EC-03: Report Flow Supports Back Navigation Before Submit

Steps:

1. Open `Report User` from chat options.
2. Select `Fake Profile`.
3. On the description step, click `← Back`.
4. Select `Other`.
5. Continue to the description step again.

Expected browser-visible results:

- The category step opens first.
- The description step opens after a category is chosen.
- `← Back` returns to category selection without closing the modal.
- A different category can be selected before submission.

### EC-04: Report Description Enforces 500 Character Limit

Steps:

1. Paste text longer than 500 characters into `Additional context...`.
2. Observe the character counter.
3. Try to add more text.

Expected browser-visible results:

- The field stops accepting input at 500 characters.
- The counter reaches `500/500` and does not exceed it.
- The modal remains usable and can still submit.

### EC-05: Ended Conversation Hides Active Chat Options

Steps:

1. Open the ended conversation.
2. Inspect the chat header.

Expected browser-visible results:

- The `⋮` options button is not visible.
- The message composer is not visible.
- The ended-state banner remains visible.

## Suggested Agent Execution Order

Run the browser scenarios in this order to minimize setup churn:

1. HP-01 → 2. ER-01 → 3. EC-02 → 4. HP-02 → 5. HP-03 → 6. ER-03 → 7. ER-04 → 8. EC-01 → 9. EC-03 → 10. EC-04 → 11. EC-05 → 12. ER-02

## Pass Criteria

A scenario passes when:

- every listed browser step is executable through the current web UI
- every expected browser-visible result is observed
- no step requires hidden implementation knowledge to continue

A scenario should be marked blocked, not failed, when the required fixture state cannot be reached from the browser alone.
