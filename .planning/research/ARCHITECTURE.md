# Architecture Patterns

**Domain:** AI Web Design Discovery Agent
**Researched:** 2026-04-09

## Recommended Architecture

### Conversation Flow as State Machine

The discovery conversation should be modeled as a 5-phase state machine with adaptive transitions.

```
[INTRO] → [BUSINESS_CONTEXT] → [DESIGN_DIRECTION] → [SITE_STRUCTURE] → [WRAP_UP]
                                                                              ↓
                                                                     [SUMMARY_CONFIRMATION]
```

Each phase contains:

- A set of questions (ordered by priority)
- Completion criteria (which fields must be filled before advancing)
- Skip rules (when to move on despite incomplete answers)
- Probing rules (when to dig deeper)

### Component Boundaries

| Component            | Responsibility                                                                            | Communicates With                              |
| -------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Question Bank        | Stores all questions with metadata (phase, tier, probes, fallbacks, industry defaults)    | Flow Controller                                |
| Flow Controller      | Manages phase transitions, tracks progress, decides next question                         | Question Bank, Response Analyzer, Agent Prompt |
| Response Analyzer    | Evaluates answer quality (vague vs specific), extracts structured data from freeform text | Flow Controller, Discovery Brief               |
| Agent Prompt Builder | Assembles the system prompt with conversation context, current phase, and instructions    | LLM, Flow Controller                           |
| Discovery Brief      | Structured output document accumulating all captured information                          | Response Analyzer, Completeness Scorer         |
| Completeness Scorer  | Evaluates whether enough information exists to start mockups                              | Discovery Brief, Flow Controller               |
| Industry Defaults    | Pre-built templates (pages, features, CTAs) per industry vertical                         | Flow Controller (for "I don't know" handling)  |

### Data Flow

```
Client Message
     ↓
Response Analyzer → extracts structured fields, evaluates answer quality
     ↓
Discovery Brief → updated with new information
     ↓
Completeness Scorer → checks coverage of Tier 1/2 fields
     ↓
Flow Controller → decides: probe deeper? move to next question? advance phase?
     ↓
Agent Prompt Builder → assembles next message with:
  - Warm acknowledgment of previous answer
  - Optional connection to earlier answers
  - Next question (with context for why we're asking)
  - Phase progress indicator
     ↓
LLM → generates conversational response
     ↓
Client sees warm, natural message with embedded question
```

## Patterns to Follow

### Pattern 1: Warm Acknowledgment Before Question

**What:** Every agent response starts by reflecting the client's previous answer, then transitions to the next question.
**When:** After every client response, without exception.
**Example:**

```
Client: "We're a family-owned bakery in Portland, been around since 1985."

Agent: "A family-owned bakery with nearly 40 years of history -- that's a
wonderful story, and definitely something your website should showcase.
That heritage gives you a real advantage over newer competitors.

Now, when someone visits your website, what's the main thing you want
them to do? For example, place an order, find your location, learn about
your story, or something else?"
```

### Pattern 2: Progressive Disclosure with Phase Transitions

**What:** Natural transitions between conversation phases that orient the client.
**When:** When moving from one phase to the next.
**Example:**

```
Agent: "Great -- I have a clear picture of your business and who you're
trying to reach. Now for the fun part: let's talk about how you want
your website to look and feel."
```

### Pattern 3: "I Don't Know" Cascade

**What:** Three-step handling when client cannot answer.
**When:** Client says "I don't know," "I'm not sure," or gives a non-answer.

```
Step 1: REFRAME the question in simpler terms
Step 2: OFFER OPTIONS based on industry defaults
Step 3: SKIP and mark as incomplete, move on
```

### Pattern 4: Adaptive Probing

**What:** Dig deeper when answer quality is low on critical fields.
**When:** Tier 1 field gets a vague answer (e.g., "We want it to look nice").

```
Trigger: vague answer + Tier 1 field
Action: Ask a more specific follow-up
Limit: Maximum 2 probes per question before moving on
```

## Anti-Patterns to Avoid

### Anti-Pattern 1: Flat Question List

**What:** Asking questions in rigid order regardless of conversation context.
**Why bad:** Feels robotic. Misses opportunities to connect related topics. Cannot adapt to what client has already volunteered.
**Instead:** Use phase-based flow with adaptive question selection within each phase.

### Anti-Pattern 2: Over-Extraction

**What:** Trying to extract every possible detail in a single conversation.
**Why bad:** Conversation becomes exhausting. Diminishing returns after 15-20 minutes.
**Instead:** Focus on Tier 1 and Tier 2 fields. Flag Tier 3 gaps for follow-up only if needed.

### Anti-Pattern 3: Summary at the End Only

**What:** Waiting until the very end to confirm understanding.
**Why bad:** Misunderstandings compound through the conversation.
**Instead:** Mini-summaries at phase transitions, full summary at wrap-up.

## Discovery Brief Output Schema

The conversation should produce a structured brief:

```typescript
interface DiscoveryBrief {
  // Tier 1 (required for mockups)
  business: {
    name: string;
    description: string;
    industry: string;
    usp: string;
  };
  goals: {
    primaryGoal: string; // "generate leads" | "sell products" | "showcase portfolio" | etc.
    successMetric: string; // "What changes in 6 months if site works perfectly?"
  };
  audience: {
    description: string;
    painPoints: string[];
    devicePreference: "mobile" | "desktop" | "both";
  };
  pages: string[]; // List of pages needed
  primaryCTA: {
    action: string; // "Book a call" | "Buy now" | "Get a quote" | etc.
    buttonText: string;
  };
  visualDirection: {
    referenceSitesLiked: { url: string; whatTheyLike: string }[];
    referenceSitesDisliked: { url: string; whatTheyDislike: string }[];
    moodAdjectives: string[]; // 3-5 words
    imageryPreference: string; // "photography" | "illustration" | "abstract" | etc.
  };
  brandAssets: {
    hasLogo: boolean;
    hasColors: boolean;
    hasFonts: boolean;
    hasBrandGuide: boolean;
    notes: string;
  };

  // Tier 2 (improves mockup quality)
  content: {
    readiness: "ready" | "partial" | "needs_creation";
    whoWrites: string;
  };
  competitors: { url: string; notes: string }[];
  tone: string; // "formal" | "casual" | "playful" | "luxurious" | etc.
  features: string[]; // Special features beyond basic pages
  stakeholders: string[]; // Who else needs to approve

  // Tier 3 (deferrable)
  timeline: string;
  budget: string;
  seoNeeds: string;
  maintenancePlan: string;

  // Meta
  completenessScore: number; // 0-100 based on field coverage
  missingCritical: string[]; // List of Tier 1 fields still empty
  conversationNotes: string; // Agent observations, flags, concerns
}
```

## Sources

- Synthesized from DISCOVERY-FRAMEWORK.md research
