# Phase 3: Integration Testing & Go-Live - Context

**Gathered:** 2026-04-10
**Status:** Ready for planning

<domain>
## Phase Boundary

Verify the complete client onboarding flow works end-to-end through live infrastructure: admin dashboard invite → email with token → client chat → Scout discovery conversation → brief generation → JSON emission → completion flow. No new code — this is testing and tuning of what Phases 1 and 2 built.

</domain>

<decisions>
## Implementation Decisions

### Testing Approach

- **D-01:** Manual walkthrough — Randall sends himself a test invite and walks through the full discovery flow as a mock client
- **D-02:** Pass criteria: Scout greets warmly, follows 5-phase discovery, asks one question at a time, acknowledges answers, generates markdown brief in briefs/ directory, emits JSON block matching OnboardingWebsiteData schema, includes ONBOARDING_COMPLETE sentinel

### Session Continuity

- **D-03:** Session continuity relies on `user: token` field (onboarding token sent in every request), NOT `previous_response_id`. The user-scoped session key (`agent:client-onboarding:responses-user:<token>`) persists on disk for 30 days
- **D-04:** Test session resume: close browser mid-conversation, reopen the same onboarding link, verify conversation continues where it left off
- **D-05:** 30-minute `previous_response_id` TTL is NOT a concern — web app uses `user: token` which has a longer-lived session key

### Deploy

- **D-06:** Randall handles the web app deploy himself (gannsystems.pro-landing-page repo). Plan should NOT include deploy steps.
- **D-07:** Gateway restart already done in Phase 1. No additional gateway work needed unless issues arise.

### Go-Live

- **D-08:** No formal go-live checklist needed for v1 — once manual walkthrough passes, Scout is ready for real clients
- **D-09:** Fallback if Scout breaks: clients can still reply to the welcome email with the 10 fallback questions (existing email Q&A path)

### Claude's Discretion

- Specific test scenario details (mock business name, industry, etc.)
- Order of test verifications
- How to handle any issues discovered during testing

</decisions>

<canonical_refs>

## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Agent Setup

- `.planning/research/AGENT-SETUP.md` — Session management, HTTP routing, auth profiles
- `.planning/phases/01-agent-infrastructure/01-01-SUMMARY.md` — What Phase 1 built
- `.planning/phases/01-agent-infrastructure/01-02-SUMMARY.md` — Routing header and gateway verification

### Discovery Protocol

- `.planning/phases/02-discovery-conversation-system/02-01-SUMMARY.md` — SOUL.md and BOOTSTRAP.md
- `.planning/phases/02-discovery-conversation-system/02-02-SUMMARY.md` — AGENTS.md protocol

### Web App Contract

- `.planning/research/AGENT-SETUP.md` §3 — HTTP routing via x-openclaw-agent-id header
- `/Users/rgann/source/gannsystems.pro-landing-page/apps/web/app/api/chat/[token]/message/route.ts` — Gateway proxy with agent header
- `/Users/rgann/source/gannsystems.pro-landing-page/packages/types/src/onboarding.ts` — OnboardingWebsiteData schema
- `/Users/rgann/source/gannsystems.pro-landing-page/apps/web/app/api/chat/[token]/complete/route.ts` — Completion and extraction logic

</canonical_refs>

<code_context>

## Existing Code Insights

### Reusable Assets

- Agent `client-onboarding` (Scout) fully configured with SOUL.md, BOOTSTRAP.md, AGENTS.md
- Workspace at `~/.openclaw/workspace-client-onboarding/` with `briefs/` and `memory/` directories
- Auth profiles copied from main agent

### Established Patterns

- Session routing via `user: token` field → user-scoped session key
- SSE streaming for real-time response delivery
- ONBOARDING_COMPLETE sentinel → frontend completion detection
- JSON block extraction via regex in complete/route.ts

### Integration Points

- Web app admin dashboard → invite endpoint → email → client chat → Scout agent
- Scout agent → briefs/ directory (markdown file write)
- Scout agent → final message → JSON block → web app extraction → Firestore

</code_context>

<specifics>
## Specific Ideas

- Test with a realistic mock business (e.g., a local bakery or plumbing company) to see how Scout adapts industry-specific defaults
- Verify the brief file appears in `~/.openclaw/workspace-client-onboarding/briefs/` with the correct naming format
- Check that the JSON block in the final message has the correct field names and null handling

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

_Phase: 03-integration-testing-go-live_
_Context gathered: 2026-04-10_
