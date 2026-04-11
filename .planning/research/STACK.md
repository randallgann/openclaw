# Technology Stack

**Project:** AI Web Design Discovery Agent
**Researched:** 2026-04-09

## Recommended Stack

### Core Framework

| Technology                           | Version | Purpose                                                        | Why                                                                           |
| ------------------------------------ | ------- | -------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Conversational state machine         | N/A     | Manage 5-phase conversation flow                               | Progressive disclosure requires tracking phase, asked questions, completeness |
| Structured question bank (JSON/YAML) | N/A     | Store questions with metadata (phase, tier, probes, fallbacks) | Enables adaptive questioning, smart defaults, and completeness scoring        |

### Data Model

| Technology                | Version | Purpose                                        | Why                                                    |
| ------------------------- | ------- | ---------------------------------------------- | ------------------------------------------------------ |
| Discovery brief schema    | N/A     | Structured output from conversation            | Must map to mockup generation inputs; needs validation |
| Industry defaults library | N/A     | Pre-built page templates per industry vertical | Handles "I don't know" for site structure questions    |

### Conversation Patterns

| Pattern                | Purpose                                    | When to Use                                     |
| ---------------------- | ------------------------------------------ | ----------------------------------------------- |
| Progressive disclosure | Funnel broad to specific                   | Always -- core conversation architecture        |
| Warm acknowledgment    | Reflect understanding before next question | After every client response                     |
| Adaptive probing       | Dig deeper on vague/critical answers       | When answer is vague or field is Tier 1         |
| Graceful skip          | Handle "I don't know" without stalling     | When client cannot answer after reframe attempt |
| Summary confirmation   | Read back all captured information         | End of conversation, before handoff             |

## Alternatives Considered

| Category                | Recommended                           | Alternative                            | Why Not                                                                            |
| ----------------------- | ------------------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------- |
| Question format         | Conversational (1-2 at a time)        | Long-form questionnaire (50 questions) | Research shows quality degrades after 15-20 form fields; abandonment is high       |
| Flow structure          | 5-phase progressive                   | Flat/random order                      | No progressive disclosure; budget/timeline too early kills rapport                 |
| "I don't know" handling | Reframe then offer defaults then skip | Force an answer                        | Clients give bad data when forced; better to use smart defaults                    |
| Visual preferences      | Reference sites + mood words          | Technical design specs                 | Clients cannot articulate "I want 16px Helvetica"; they can say "clean and modern" |

## Sources

- Synthesized from DISCOVERY-FRAMEWORK.md research
