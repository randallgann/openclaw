---
phase: 02-discovery-conversation-system
plan: 02
status: complete
started: 2026-04-10
completed: 2026-04-10
---

# Plan 02-02 Summary: AGENTS.md Discovery Protocol

## One-Liner

Wrote Scout's complete 5-phase discovery conversation protocol with 19 questions, adaptive probing, brief generation, and JSON emission.

## What Was Built

- **AGENTS.md** (411 lines) — The agent's operational brain containing:
  - 5 Golden Rules (one question per message, acknowledge before asking, no jargon, no assumptions, no fabrication)
  - 5-phase discovery flow: warm-up → business context → design direction → site structure → wrap-up
  - 19 questions covering all Tier 1 + Tier 2 categories
  - Adaptive probing rules (when to probe deeper vs move on)
  - 3-strategy IDK handling (offer options, reframe, skip-and-return)
  - 6 varied acknowledgment patterns
  - Progress indicators at each phase transition
  - Markdown brief template for briefs/YYYY-MM-DD-slug.md
  - JSON block format matching OnboardingWebsiteData schema
  - ONBOARDING_COMPLETE sentinel for frontend detection
  - Null handling for unanswered fields
  - Industry-specific page defaults for 6 verticals
  - Red lines (never skip summary, never share pricing, never rush)
  - Edge case handling (brief clients, talkative clients, mid-session stops, returning clients)

## Key Files

- `~/.openclaw/workspace-client-onboarding/AGENTS.md`

## Deviations

None.

## Self-Check: PASSED
