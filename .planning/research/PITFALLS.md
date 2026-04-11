# Domain Pitfalls

**Domain:** AI Web Design Discovery Agent
**Researched:** 2026-04-09

## Critical Pitfalls

Mistakes that cause rewrites or major issues.

### Pitfall 1: The Interrogation Effect

**What goes wrong:** Agent asks questions in rapid succession without acknowledging answers. Client feels like they're filling out a form, not talking to a consultant.
**Why it happens:** Natural instinct to collect data efficiently. LLMs default to asking the next question without reflecting.
**Consequences:** Low-quality answers. Client disengagement. Abandoned conversations. Lost trust.
**Prevention:** Mandate warm acknowledgment pattern in every agent response. Reflect back what was heard before asking the next question.
**Detection:** Short client responses. Increasing "I don't know" answers. Conversation dropout.

### Pitfall 2: Missing Visual Direction

**What goes wrong:** Agent collects business info and goals but skips reference sites, mood adjectives, and imagery preferences. Designer starts mockup with zero visual guidance.
**Why it happens:** Visual direction questions feel "fluffy" compared to business questions. Easy to deprioritize.
**Consequences:** First mockup is a blind guess. Client says "this isn't what I had in mind." Complete visual redesign needed. Trust damaged.
**Prevention:** Treat visual direction (reference sites liked/disliked, mood words, imagery preference) as Tier 1 mandatory fields. Never skip this phase.
**Detection:** Discovery brief has empty visualDirection fields.

### Pitfall 3: Content Readiness Blind Spot

**What goes wrong:** Beautiful mockup created with lorem ipsum or placeholder text. Client has no content to fill it. Final site looks nothing like mockup.
**Why it happens:** Content readiness is rarely asked. Designers assume content exists or will be provided.
**Consequences:** Timeline delays. Mockup redesign when real content doesn't fit layout. Client frustration.
**Prevention:** Explicitly ask "Do you have content ready?" and "Who will write it?" Flag content creation as a separate workstream if needed.
**Detection:** Discovery brief shows content.readiness as undefined.

### Pitfall 4: Stakeholder Surprise

**What goes wrong:** Agent conducts full discovery with one person. Mockup is approved. Then a business partner, spouse, or marketing director sees it and vetoes everything.
**Why it happens:** Agent doesn't ask "Who else needs to approve this?" Client doesn't think to mention other decision-makers.
**Consequences:** Complete rework. Double the discovery process. Client relationship strained.
**Prevention:** Always ask "Is there anyone else who needs to be involved in approving the design?" early enough to include them.
**Detection:** Discovery brief has empty stakeholders field.

### Pitfall 5: No Summary Confirmation

**What goes wrong:** Agent collects all information and hands off to mockup generation. Client meant "modern" as in "minimalist." Agent interpreted "modern" as "cutting-edge animations." Mockup is wrong.
**Why it happens:** Summary step feels redundant. Tempting to skip to save time.
**Consequences:** Mockup based on misunderstood requirements. Rework. Client feels unheard.
**Prevention:** Always generate and present a structured summary at the end. Ask client to confirm or correct. This is the single highest-ROI step.
**Detection:** No summary generated or presented.

## Moderate Pitfalls

### Pitfall 6: Budget Question Too Early

**What goes wrong:** Asking budget in the first few questions creates a transactional feel. Client becomes defensive or guarded for the rest of the conversation.
**Prevention:** Save budget and timeline for the final phase, after trust and rapport are established.

### Pitfall 7: Jargon Overload

**What goes wrong:** Agent asks about CMS preferences, responsive breakpoints, or SEO strategy with non-technical clients.
**Prevention:** Always frame questions in terms of outcomes. "Do you need to update content yourself?" not "What CMS do you prefer?"

### Pitfall 8: Assumption-Based Suggestions

**What goes wrong:** "Since you're a restaurant, you'll need online ordering" when the client is a fine-dining establishment that only takes phone reservations.
**Prevention:** Frame suggestions as options. "Many restaurants include online ordering -- is that something you'd want?"

### Pitfall 9: Ignoring "Dislikes"

**What goes wrong:** Only collecting what clients like, never what they hate. Designer accidentally includes a pattern the client despises.
**Prevention:** Always pair "What do you like?" with "What do you dislike or want to avoid?" This is equally valuable information.

### Pitfall 10: One-Size-Fits-All Questions

**What goes wrong:** Asking a solopreneur "How does your marketing team coordinate content?" or asking a large company "Do you have a logo?"
**Prevention:** Adapt question depth and framing based on early signals about business size and sophistication.

## Minor Pitfalls

### Pitfall 11: Forgetting Mobile Priority

**What goes wrong:** Desktop-centric mockup for a business whose customers are 80% mobile.
**Prevention:** Explicitly ask about device split. Default to mobile-first if client doesn't know.

### Pitfall 12: No Industry Defaults for "I Don't Know"

**What goes wrong:** Client says "I don't know what pages I need." Agent stalls or moves on without helping. Missing critical information.
**Prevention:** Maintain industry-specific page templates. Offer them as starting points.

### Pitfall 13: Conversation Too Long

**What goes wrong:** 30+ minute conversation exhausts client. Quality of later answers degrades.
**Prevention:** Target 10-15 minutes. Focus on Tier 1 and Tier 2 fields. Defer Tier 3 to follow-up.

## Phase-Specific Warnings

| Phase Topic                  | Likely Pitfall                                     | Mitigation                                                           |
| ---------------------------- | -------------------------------------------------- | -------------------------------------------------------------------- |
| Question expansion (10 → 20) | Adding questions without improving quality         | Focus on Tier 1/2 gaps; don't add Tier 3                             |
| Conversational flow          | Agent acknowledgments become repetitive/robotic    | Vary acknowledgment patterns; use specific details from answers      |
| Smart defaults               | Defaults feel presumptuous or wrong for edge cases | Always frame as "most [industry] businesses include..." with opt-out |
| Summary generation           | Summary too long or too terse                      | Match detail level to conversation length; highlight key decisions   |
| Industry detection           | Misclassifying the business type                   | Confirm industry interpretation before offering defaults             |
| "I don't know" handling      | Agent pushes too hard or gives up too easily       | Max 2 reframe attempts, then offer defaults, then skip               |

## Sources

- Agency post-mortems and community wisdom
- Conversational AI UX research (Smashing Magazine, Mind the Product, Netguru)
- Discovery framework best practices (Jennifer Bourn, Axon Garside, SEOptimer)
