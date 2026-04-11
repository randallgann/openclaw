# Feature Landscape

**Domain:** AI Web Design Discovery Agent
**Researched:** 2026-04-09

## Table Stakes

Features users expect. Missing = product feels incomplete.

| Feature                                                 | Why Expected                                    | Complexity | Notes                                      |
| ------------------------------------------------------- | ----------------------------------------------- | ---------- | ------------------------------------------ |
| Business identity capture (name, industry, description) | Cannot begin without this                       | Low        | Already in current 10 questions            |
| Website goals identification                            | Drives entire mockup direction                  | Low        | Already in current 10 questions            |
| Target audience profiling                               | Affects tone, layout, content                   | Low        | Already in current 10 questions            |
| Visual preference collection (reference sites)          | Designers cannot start without visual direction | Medium     | Missing from current questions -- must add |
| Page/sitemap definition                                 | Directly scopes the mockup                      | Medium     | Partially covered; needs industry defaults |
| Primary CTA identification                              | Without this, mockup has no conversion strategy | Low        | Missing -- critical gap                    |
| Brand asset inventory (logo, colors, fonts)             | Avoids creating conflicting visual identity     | Low        | Partially covered in current questions     |
| Conversation summary/confirmation                       | Prevents misunderstandings that cause rework    | Medium     | Not implemented -- highest ROI addition    |
| Progress indication                                     | Users need to know where they are               | Low        | Standard conversational UX                 |

## Differentiators

Features that set product apart. Not expected, but valued.

| Feature                               | Value Proposition                                                                          | Complexity | Notes                                             |
| ------------------------------------- | ------------------------------------------------------------------------------------------ | ---------- | ------------------------------------------------- |
| Industry-specific smart defaults      | When clients say "I don't know," agent proposes standard pages/features for their industry | Medium     | Reduces friction, increases completeness          |
| Adaptive probing depth                | Agent digs deeper on vague answers to critical questions, moves quickly on clear answers   | Medium     | Makes conversation feel intelligent, not scripted |
| Mood/personality extraction           | "If your website were a person..." question yields rich design direction                   | Low        | Novel framing that clients enjoy                  |
| Content readiness assessment          | Flags whether client has content ready or needs it created                                 | Low        | Prevents the #1 cause of mockup rework            |
| Stakeholder identification            | "Who else needs to approve?" prevents late-stage vetoes                                    | Low        | Simple question, massive rework prevention        |
| Mockup readiness scoring              | Agent knows when it has enough info to start vs. needs to keep asking                      | Medium     | Prevents premature or incomplete handoff          |
| "Dislike" collection alongside "like" | Knowing what client hates is as valuable as what they love                                 | Low        | Often skipped; prevents design mismatch           |
| Mobile priority assessment            | Shapes responsive design approach from the start                                           | Low        | Often assumed; should be explicit                 |

## Anti-Features

Features to explicitly NOT build.

| Anti-Feature                                   | Why Avoid                                                  | What to Do Instead                                                                     |
| ---------------------------------------------- | ---------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Technical jargon questions (CMS, CDN, hosting) | Confuses non-technical clients, breaks trust               | Ask about outcomes: "Do you need to update content yourself?"                          |
| 50+ question exhaustive intake                 | Abandonment after 15-20 questions; quality degrades        | 18-20 conversational questions with adaptive probing                                   |
| Budget question first/early                    | Creates defensiveness, feels transactional                 | Ask near the end after trust is established                                            |
| Rigid question ordering                        | Feels robotic; doesn't adapt to client context             | Flexible flow that adapts based on answers                                             |
| Assumption-based suggestions                   | "Since you're a restaurant, you need X" feels presumptuous | Offer suggestions as options: "Many restaurants include X -- would that work for you?" |
| Form-style rapid-fire questions                | Feels like filling out a government form                   | 1-2 questions at a time with acknowledgment between                                    |

## Feature Dependencies

```
Business Identity → Target Audience → Website Goals → CTA Strategy
Visual Preferences (reference sites + mood) → Design Direction
Pages Needed → Content Readiness Assessment
All Tier 1 Fields → Mockup Readiness Score
All Phases Complete → Summary Confirmation → Handoff
```

## MVP Recommendation

Prioritize:

1. Expand from 10 to 18-20 questions covering all Tier 1 and Tier 2 categories
2. Implement 5-phase conversation flow with progressive disclosure
3. Add warm acknowledgment pattern between questions
4. Add "I don't know" handling with smart defaults for top 8 industries
5. Add summary/confirmation step at end

Defer:

- Mockup readiness scoring: useful but can start with simple checklist
- Multi-stakeholder intake: complex, rare in initial usage
- Accessibility-specific discovery: important but can be added as a specialized sub-flow

## Sources

- Synthesized from DISCOVERY-FRAMEWORK.md research
