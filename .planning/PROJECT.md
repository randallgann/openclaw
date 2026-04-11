# Client Onboarding Agent

## What This Is

A dedicated openclaw agent that conducts warm, conversational website discovery sessions with new clients. When a client clicks the onboarding link emailed from the GannSystems dashboard, they enter an AI-guided intake conversation that gathers everything needed to start website mockups — replacing the current email Q&A with a real-time, adaptive chat experience.

## Core Value

The agent must gather complete, actionable website requirements from non-technical clients through natural conversation — so Randall can start mockups without a follow-up discovery call.

## Requirements

### Validated

<!-- Shipped and confirmed valuable. -->

- Dedicated openclaw agent with isolated workspace — v1.0
- Warm-consultant personality (SOUL.md, AGENTS.md) — v1.0
- Web-design discovery framework (19 questions, 5-phase progressive disclosure) — v1.0
- Conversational flow that adapts based on client responses — v1.0
- Final markdown brief generated in agent workspace — v1.0
- Cloudflare tunnel redirect from main agent to onboarding agent — v1.0
- Compatible with existing web chat contract (SSE, /v1/responses, user:token routing) — v1.0

### Active

<!-- Current scope. Building toward these. -->

(None — v1.0 shipped. Use /gsd-new-milestone for next cycle.)

### Out of Scope

<!-- Explicit boundaries. Includes reasoning to prevent re-adding. -->

- Multi-agent collaboration (Beacon/Atlas integration) — v2, standalone for MVP
- Structured JSON output / mockup-tool integration — v2, markdown brief sufficient for now
- Branded PDF generation — v2
- Changes to gannsystems.pro-landing-page web app — routing already works, only openclaw-side changes
- Per-client workspace isolation — single agent workspace with per-session context via token

## Context

- **Existing infrastructure**: GannSystems web app (Next.js + Firebase) already handles invite flow, token generation, email sending, SSE chat UI, and structured data extraction
- **Current intake**: 10 fallback questions in welcome email (business name, industry, audience, goals, existing site, branding, competitors, features, timeline, budget)
- **Structured type**: `OnboardingWebsiteData` in `packages/types/src/onboarding.ts` defines extraction fields
- **Gateway contract**: Web app sends `POST /v1/responses` with `{ model: "openclaw", input, stream: true, user: token }` + Bearer auth
- **Completion sentinel**: Chat client detects `ONBOARDING_COMPLETE` in AI response to trigger summary flow
- **Agent model**: openclaw agents have isolated workspace (AGENTS.md/SOUL.md/USER.md/IDENTITY.md), agentDir, sessions, and channel bindings

## Constraints

- **Compatibility**: Must not break existing web chat SSE contract or token-based session routing
- **Platform**: openclaw agent system (workspace + identity + bindings), not custom code
- **Model**: Uses configured default model (currently openrouter/moonshotai/kimi-k2.5 with fallbacks)
- **Output**: Markdown brief in workspace; no external integrations for v1

## Key Decisions

| Decision                                     | Rationale                                                                | Outcome |
| -------------------------------------------- | ------------------------------------------------------------------------ | ------- |
| Standalone agent (no multi-agent)            | Simpler v1, avoid cross-agent complexity                                 | Good    |
| Warm consultant personality                  | Clients are non-technical, need approachable tone                        | Good    |
| Research-driven discovery framework          | Current 10 questions are basic; best practices will surface deeper needs | Good    |
| Markdown brief output                        | Quick to implement, Randall reads these directly                         | Good    |
| Agent routing via x-openclaw-agent-id header | Web/HTTP not a channel; header is simplest                               | Good    |
| Session continuity via user:token            | 30-day on-disk persistence, no previous_response_id needed               | Good    |

---

_Last updated: 2026-04-11 after v1.0 milestone_
