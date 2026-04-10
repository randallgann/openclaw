# Roadmap: Client Onboarding Agent

**Created:** 2026-04-10
**Milestone:** v1.0

## Phase 1: Agent Infrastructure

**Goal:** Create a working openclaw agent that receives messages from the web chat via cloudflare tunnel and responds.

**Requirements:** INFRA-01, INFRA-02, INFRA-03, INFRA-04, INFRA-05

**Plans:** 2 plans

Plans:

- [ ] 01-01-PLAN.md — Create agent, workspace, identity, auth profiles
- [ ] 01-02-PLAN.md — Add routing header to web app, restart gateway, verify connectivity

**Success criteria:**

- `openclaw agents list` shows `client-onboarding` agent
- `curl` to gateway with `x-openclaw-agent-id: client-onboarding` gets a response
- Web app sends header and routes to correct agent
- Agent has identity (name, emoji) and isolated workspace

**Key tasks:**

1. Run `openclaw agents add client-onboarding --workspace ~/.openclaw/workspace-client-onboarding --non-interactive`
2. Create workspace directories (`briefs/`, `memory/`)
3. Write IDENTITY.md with agent name and personality seed
4. Write USER.md with Randall/GannSystems context
5. Copy auth profiles from main agent
6. Add `x-openclaw-agent-id: client-onboarding` header to web app's gateway fetch call
7. Restart gateway and test connectivity

**Depends on:** Nothing

---

## Phase 2: Discovery Conversation System

**Goal:** Agent conducts a warm, structured website discovery conversation and produces a complete brief.

**Requirements:** DISC-01, DISC-02, DISC-03, DISC-04, DISC-05, CONV-01, CONV-02, CONV-03, CONV-04, CONV-05, OUT-01, OUT-02, OUT-03, OUT-04, OUT-05

**Success criteria:**

- Agent greets client warmly and guides through 5-phase discovery
- All Tier 1 + Tier 2 questions are covered naturally in conversation
- Agent adapts based on responses (e.g., skips branding questions if client has none)
- Final message includes JSON block matching OnboardingWebsiteData schema
- Markdown brief generated in `briefs/` directory
- "I don't know" answers handled gracefully with examples/defaults

**Key tasks:**

1. Write SOUL.md — warm consultant persona, tone boundaries, conversation style
2. Write AGENTS.md — full discovery protocol with 5-phase flow, question bank, probing rules, brief generation instructions, JSON emission format, completion sentinel
3. Write BOOTSTRAP.md — first-contact greeting for new sessions
4. Write TOOLS.md — available resources and references
5. Test conversation flow with sample client scenarios
6. Tune question phrasing and acknowledgment patterns

**Depends on:** Phase 1

---

## Phase 3: Integration Testing & Go-Live

**Goal:** Verify end-to-end flow works through the live web app and tune for production.

**Requirements:** COMPAT-01, COMPAT-02, COMPAT-03, COMPAT-04

**Success criteria:**

- Client receives email invite, clicks link, enters chat, completes full discovery — all through live infrastructure
- SSE streaming works without interruption through cloudflare tunnel
- Session continuity works (client can leave and resume)
- Completion flow extracts structured data from JSON block in final message
- Brief file appears in agent workspace after session
- No regressions to existing agents (main, Atlas, Beacon)

**Key tasks:**

1. End-to-end test via admin dashboard → invite → email → chat → completion
2. Verify SSE streaming compatibility through tunnel
3. Test session resume (close browser, reopen link)
4. Verify OnboardingWebsiteData extraction from JSON block
5. Verify brief file written to workspace
6. Confirm existing agents unaffected
7. Tune personality/questions based on test results

**Depends on:** Phase 2

---

_Roadmap created: 2026-04-10_
_Last updated: 2026-04-10 after Phase 1 planning_
