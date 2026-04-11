# Web Design Client Discovery Framework for AI Onboarding Agent

**Researched:** 2026-04-09
**Overall confidence:** HIGH (synthesized from multiple agency frameworks, UX research, and conversational AI best practices)

---

## 1. Industry-Standard Website Discovery Frameworks

### The Two-Phase Discovery Model

Top agencies separate discovery into two distinct phases (per Jennifer Bourn's framework):

1. **Brand Discovery** -- emotional, identity-focused questions (who you are, what you stand for, how you want to be perceived)
2. **Website Discovery** -- logical, operational questions (what the site needs to do, what pages exist, what actions visitors should take)

This separation matters for an AI agent because it creates natural conversation segments with different tones: empathetic/exploratory for brand, structured/concrete for website.

### Comprehensive Discovery Categories

Synthesized from Axon Garside (50 questions), SEOptimer (17 questions), Jennifer Bourn, and multiple agency frameworks, the industry consensus covers these categories ranked by importance for mockup generation:

#### Tier 1: Must-Have for Any Mockup

| Category          | What It Covers                                                        | Why Critical                                                  |
| ----------------- | --------------------------------------------------------------------- | ------------------------------------------------------------- |
| Business Identity | What the business does, USP, mission                                  | Drives headline copy, hero messaging                          |
| Target Audience   | Who the visitors are, demographics, pain points                       | Determines tone, layout complexity, content level             |
| Website Goals     | Primary purpose (sell, inform, generate leads, portfolio)             | Determines page types, CTA strategy, information architecture |
| Pages & Sitemap   | Which pages are needed, navigation structure                          | Directly defines mockup scope                                 |
| Design Direction  | Visual preferences, reference sites liked/disliked, existing branding | Drives all visual decisions                                   |

#### Tier 2: Strongly Improves Mockup Quality

| Category             | What It Covers                                                | Why Important                                     |
| -------------------- | ------------------------------------------------------------- | ------------------------------------------------- |
| Calls to Action      | What visitors should do on each page                          | Defines button placement, forms, conversion flow  |
| Content Readiness    | Does copy exist? Photos? Logo?                                | Determines placeholder vs real content in mockups |
| Competitor Landscape | 2-3 competitor URLs, what they do well/poorly                 | Provides design differentiation context           |
| Tone & Personality   | Formal vs casual, playful vs serious, luxurious vs accessible | Drives typography, color temperature, spacing     |

#### Tier 3: Nice-to-Have (Can Be Deferred)

| Category            | What It Covers                        | When Needed          |
| ------------------- | ------------------------------------- | -------------------- |
| SEO Requirements    | Keywords, search visibility goals     | Implementation phase |
| Technical Platform  | CMS preference, hosting, integrations | Development phase    |
| Maintenance Plan    | Who updates content, how often        | Post-launch planning |
| Budget & Timeline   | Project constraints                   | Scoping, not design  |
| Analytics & Metrics | Current traffic, conversion rates     | Optimization phase   |

### The "Creative Brief" Framework

The creative brief distills discovery into a single-page artifact:

- **Objective:** One sentence on what the site must achieve
- **Audience:** Who and what they care about
- **Key Message:** The single most important takeaway
- **Tone:** 3-5 adjectives describing the feel
- **Deliverables:** Specific pages/features
- **References:** 2-3 aspirational sites with annotations on what to borrow
- **Constraints:** Brand guidelines, technical limitations, budget

---

## 2. Questions That Matter for Mockups Specifically

### What a Designer Needs to Start Wireframes

Based on wireframing best practices from Figma, HubSpot, and IxDF, a designer needs these to produce useful wireframes without a follow-up call:

#### A. Information Architecture (Page Structure)

```
Required:
- List of pages needed (home, about, services, contact, blog, etc.)
- Primary navigation structure (what goes in the main menu?)
- Most important page (where should most design effort go?)

Example questions:
- "If your website were a building, what rooms would it have? Think of each page as a room."
- "When someone arrives at your homepage, what's the FIRST thing they should understand?"
- "Which page is the most important for your business goals?"
```

#### B. Content Hierarchy (Per-Page Priority)

```
Required:
- Hero section message (what's the headline?)
- Primary CTA per page (what should visitors DO?)
- Content sections in priority order

Example questions:
- "Imagine a new visitor lands on your homepage. In 5 seconds, what should they know?"
- "What's the single most important action you want someone to take on your site?"
- "After the main headline, what information should come next? And after that?"
```

#### C. Visual Direction

```
Required:
- 2-3 websites they admire (with WHY they like them)
- 2-3 websites they dislike (with WHY)
- Existing brand assets (logo, colors, fonts) or lack thereof
- Mood adjectives (3-5 words describing desired feel)

Example questions:
- "Share 2-3 websites you love. What specifically draws you to them -- the colors? Layout? Photography style? The way text reads?"
- "Now share 1-2 websites you dislike. What turns you off?"
- "Pick 3-5 words that describe how your website should feel. Examples: bold, minimal, warm, corporate, playful, luxurious, approachable, edgy."
```

#### D. Above-the-Fold Strategy

```
Required:
- Hero imagery preference (photo, illustration, video, abstract, none)
- Headline messaging direction
- Primary CTA button text/action

Example questions:
- "What type of imagery best represents your brand? Real photography of your team/products, illustrations, abstract graphics, or something else?"
- "If your homepage had one big button, what would it say? 'Get Started'? 'Shop Now'? 'Book a Call'? 'Learn More'?"
```

#### E. Mobile Priorities

```
Required:
- Mobile importance (what percentage of visitors are mobile?)
- Mobile-specific needs (click-to-call, maps, simplified navigation)

Example questions:
- "Do most of your customers find you on their phone or computer?"
- "When someone visits on their phone, what's the ONE thing they should be able to do easily?"
```

#### F. Special Functional Needs

```
Required:
- E-commerce (yes/no, product count)
- Forms (contact, booking, quote request)
- Blog/content section
- User accounts/login
- Third-party integrations (booking systems, payment, CRM)
- Accessibility requirements

Example questions:
- "Will you be selling products or services directly on the website?"
- "Do visitors need to fill out any forms? What information do you need from them?"
- "Are there any tools your business already uses that the website needs to connect with? Think booking systems, email marketing, payment processors."
```

---

## 3. Conversational UX for AI-Driven Intake

### Core Principles

Based on research from Smashing Magazine, Mind the Product, and multiple conversational AI guides:

#### Principle 1: Progressive Disclosure (Funnel from Broad to Specific)

Start with open-ended questions that let the client talk freely, then narrow based on their answers.

```
Flow structure:
1. WARM-UP: Open, easy questions (business name, what you do)
2. EXPLORE: Broader discovery (goals, audience, vision)
3. SPECIFY: Concrete details (pages, features, preferences)
4. CONFIRM: Summarize and validate understanding

Each phase should feel like a natural narrowing, not an interrogation.
```

#### Principle 2: Chunk Questions (Never More Than 2 at a Time)

Research shows users abandon after the third consecutive question without engagement. The agent should:

- Ask 1-2 questions maximum before acknowledging/reflecting
- Group related questions naturally ("Let's talk about your audience...")
- Provide transitions between topic shifts

```
BAD:  "What's your business name? What industry? Who's your audience? What are your goals?"
GOOD: "Let's start with the basics -- what's your business called, and what do you do?"
      [response]
      "Got it! [Reflect back]. Now tell me about the people you're trying to reach..."
```

#### Principle 3: Warm Acknowledgment Before Next Question

Every client response should be acknowledged before moving on. This is the single biggest differentiator between a bot that feels like a form and one that feels like a consultant.

```
Pattern:
1. Client answers
2. Agent reflects/validates ("That makes sense -- a lot of [industry] businesses find that...")
3. Optional: brief insight or connection to earlier answer
4. Next question with context for why you're asking
```

#### Principle 4: Handle "I Don't Know" Gracefully

Three strategies based on the Smashing Magazine framework:

```
Strategy A: OFFER OPTIONS
Client: "I don't know what pages I need."
Agent: "No problem! Most [industry type] websites include a homepage, about page,
        services page, and contact page. Some also add a blog, testimonials,
        or portfolio. Does that starting point sound right, or would you
        add/remove anything?"

Strategy B: REFRAME THE QUESTION
Client: "I'm not sure about my target audience."
Agent: "Let me ask it differently -- think about your best customer ever.
        What were they like? What problem did you solve for them?"

Strategy C: SKIP AND RETURN
Client: "I really can't answer that right now."
Agent: "Totally fine -- we can come back to that later, or skip it entirely.
        Let's move on to something more fun..."
```

#### Principle 5: Show Progress

Users appreciate knowing where they are in the process:

```
"Great progress! We've covered your business and audience.
 Next, I'd love to hear about your design preferences -- this is the fun part."
```

#### Principle 6: Set Expectations Upfront

```
Opening: "I'm going to ask you some questions to understand your business and
          what you need from your website. This usually takes about 10-15 minutes.
          There are no wrong answers -- if you're unsure about anything, just
          say so and I'll help guide you."
```

### Recommended Conversation Flow

```
Phase 1: INTRODUCTION (1-2 minutes)
  - Set expectations (time, purpose, "no wrong answers")
  - Ask business name and what they do
  - Reflect back, show understanding

Phase 2: BUSINESS CONTEXT (3-4 minutes)
  - Target audience / ideal customer
  - Business goals for the website
  - Current website situation (new vs redesign)
  - Competitive landscape (2-3 competitors)

Phase 3: DESIGN DIRECTION (3-4 minutes)
  - Reference websites (liked and disliked)
  - Existing brand assets (logo, colors, guidelines)
  - Mood/tone adjectives
  - Imagery preferences

Phase 4: SITE STRUCTURE (3-4 minutes)
  - Pages needed
  - Primary calls to action
  - Special features/functionality
  - Content readiness

Phase 5: WRAP-UP (1-2 minutes)
  - Summarize everything captured
  - Ask "Is there anything I missed or you'd like to add?"
  - Set expectations for next steps
  - Timeline and budget (if not covered)
```

---

## 4. Information Completeness: Minimum Viable Discovery

### The "Start Mockups Without a Follow-Up Call" Checklist

These are the absolute minimum fields needed to produce a useful first mockup. Missing any of these virtually guarantees a follow-up conversation:

| #   | Information                                      | Why Non-Negotiable                                             |
| --- | ------------------------------------------------ | -------------------------------------------------------------- |
| 1   | Business name + what they do                     | Cannot create any content without this                         |
| 2   | Primary website goal                             | Determines entire page structure and CTA strategy              |
| 3   | Target audience description                      | Drives tone, complexity, and visual choices                    |
| 4   | Pages needed (at minimum: list)                  | Defines mockup scope                                           |
| 5   | Primary CTA / desired visitor action             | Without this, the mockup has no conversion strategy            |
| 6   | Visual direction (reference sites OR mood words) | Without this, design is a blind guess                          |
| 7   | Existing brand assets (logo, colors) or "none"   | Avoids creating a brand that conflicts with existing materials |

### Most Commonly Missed Items That Cause Rework

Based on agency post-mortems and community wisdom:

| Rank | Missed Item                                     | Consequence                                                                                                         |
| ---- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| 1    | **Content readiness not assessed**              | Designer creates layout for content that doesn't exist; client can't fill it. Mockup looks nothing like final site. |
| 2    | **Stakeholder alignment not confirmed**         | Designer builds for one person's vision; another stakeholder vetoes everything. Complete rework.                    |
| 3    | **Mobile priority not discussed**               | Desktop-first mockup shown to client whose customers are 80% mobile. Fundamental layout rethink.                    |
| 4    | **CTA strategy undefined**                      | Beautiful mockup with no conversion path. "But where do they sign up?"                                              |
| 5    | **Reference sites not collected**               | Designer's taste vs client's taste mismatch. "This isn't what I had in mind at all."                                |
| 6    | **Existing brand guidelines not requested**     | Mockup uses wrong colors/fonts; client has a 40-page brand book they didn't mention.                                |
| 7    | **Page count / scope creep**                    | "Can we also add a blog? And a members area? And an events calendar?" after mockup is done.                         |
| 8    | **Industry-specific requirements missed**       | Regulatory needs (HIPAA, accessibility, disclaimers) discovered after mockup phase.                                 |
| 9    | **Hero imagery direction unclear**              | Stock photos in mockup; client wanted custom photography. Or vice versa.                                            |
| 10   | **"Who else needs to approve this?" not asked** | The real decision-maker hasn't been part of the conversation.                                                       |

### Smart Defaults by Industry

When a client says "I don't know" to structural questions, the agent can propose industry-standard defaults:

```
Restaurant:    Home, Menu, About, Reservations, Contact, Gallery
E-commerce:    Home, Shop, Product Pages, Cart, About, Contact, FAQ
Professional:  Home, Services, About, Case Studies/Portfolio, Contact, Blog
Local Service: Home, Services, Service Areas, Reviews, About, Contact, Free Quote
Portfolio:     Home, Work/Projects, About, Contact
SaaS:          Home, Features, Pricing, About, Blog, Contact, Login
Nonprofit:     Home, Mission, Programs, Get Involved, Donate, Contact, News
```

---

## 5. Anti-Patterns: What NOT to Do in Client Intake

### Critical Anti-Patterns

#### Anti-Pattern 1: The Interrogation

**What it looks like:** Rapid-fire questions with no acknowledgment or reflection.
**Why it fails:** Clients feel like they're filling out a form, not having a conversation. Engagement drops after 3-4 unanswered questions. Trust is not built.
**Instead:** Acknowledge every answer. Reflect understanding. Make connections between answers.

#### Anti-Pattern 2: The Jargon Dump

**What it looks like:** "What CMS do you prefer? Do you need a CDN? Headless or monolithic? REST or GraphQL?"
**Why it fails:** Most clients are not technical. Asking technical questions makes them feel stupid and undermines confidence.
**Instead:** Ask about outcomes, not implementation. "Do you need to update your website content yourself, or will someone handle that for you?"

#### Anti-Pattern 3: The Assumptions Trap

**What it looks like:** "Since you're a restaurant, you'll want an online ordering system and reservation widget."
**Why it fails:** Clients feel unheard. Their business may be different from assumptions. Creates scope expectations that may not match budget.
**Instead:** Propose suggestions as options, not assumptions. "Many restaurants include online ordering -- is that something you'd want?"

#### Anti-Pattern 4: The Everything Upfront Dump

**What it looks like:** A 50-question form sent before any conversation.
**Why it fails:** Overwhelming. Clients procrastinate or rush through it. Quality of answers degrades dramatically after question 15-20.
**Instead:** Conversational intake with progressive disclosure. 15-20 well-placed conversational questions yield better data than 50 form fields.

#### Anti-Pattern 5: Skipping the "Why"

**What it looks like:** Jumping straight to "What pages do you need?" without understanding business goals.
**Why it fails:** Client asks for a 20-page website when they really need a 5-page site with a strong CTA. Or they ask for a brochure site when they need e-commerce.
**Instead:** Always start with goals and audience before features and pages.

#### Anti-Pattern 6: Not Asking for Dislikes

**What it looks like:** Only asking "What do you like?" for reference sites.
**Why it fails:** Knowing what they hate is as valuable as knowing what they like. Prevents accidental inclusion of despised patterns.
**Instead:** Always pair "What do you like?" with "What do you dislike or want to avoid?"

#### Anti-Pattern 7: Treating All Clients the Same

**What it looks like:** Same questions in same order for a solo freelancer and a 50-person company.
**Why it fails:** A solopreneur doesn't have "stakeholders to align." A large company doesn't need "do you have a logo?" framed the same way.
**Instead:** Adapt question depth and framing based on early signals about business size and sophistication.

#### Anti-Pattern 8: No Summary or Confirmation

**What it looks like:** Collecting all information and immediately starting work.
**Why it fails:** Misunderstandings compound. Client said "modern" meaning "minimalist"; designer heard "modern" meaning "cutting-edge animations."
**Instead:** Always summarize what was heard and confirm before proceeding. This is the single highest-ROI step in the entire process.

### Question Ordering Anti-Patterns

```
BAD ORDER:
1. Budget (too personal too early, creates defensiveness)
2. Timeline (feels transactional before trust is built)
3. Technical requirements (intimidating)
4. Business goals (should be first)

GOOD ORDER:
1. Business identity and story (easy, builds rapport)
2. Goals and audience (strategic, shows you care about outcomes)
3. Design preferences (fun, visual, engaging)
4. Structure and features (concrete, builds on established context)
5. Practical constraints: timeline, budget (trust already built)
```

---

## 6. Recommended Question Set for the AI Agent

### The Complete Discovery Question Bank (Organized by Conversation Phase)

#### Phase 1: Warm-Up and Business Context

```
Q1: "What's your business called, and what do you do?"
    [Probe if vague]: "Can you walk me through what a typical customer
     experience looks like with your business?"

Q2: "What's the main goal for your website? For example, are you looking to
     get more customers, sell products online, showcase your work, or
     something else?"
    [Probe]: "If the website does its job perfectly, what changes for
     your business in 6 months?"

Q3: "Who are you trying to reach? Describe your ideal customer or visitor."
    [Probe]: "What problem are they trying to solve when they find you?"
    [I don't know]: "Think of your best customer. What are they like?
     How did they find you?"
```

#### Phase 2: Current Situation

```
Q4: "Do you currently have a website? If so, what's working and what isn't?"
    [If yes]: "What's the URL? What do you wish was different about it?"
    [If no]: "That's totally fine -- we're starting fresh! Have you had
     one in the past?"

Q5: "Are there 2-3 competitor or similar businesses whose websites you've
     noticed? What stood out to you about them -- good or bad?"
```

#### Phase 3: Design Direction

```
Q6: "Share 2-3 websites you love -- they don't have to be in your industry.
     What specifically do you like about each one?"
    [Probe]: "Is it the colors? The layout? The photography? The way the
     text reads? The overall vibe?"

Q7: "Now the flip side -- any websites you've seen that you really don't
     like? What turned you off?"

Q8: "If your website were a person, how would you describe their personality?
     Pick 3-5 words. For example: bold, minimal, warm, corporate, playful,
     luxurious, approachable, edgy, clean, sophisticated."

Q9: "Do you have existing brand materials -- a logo, specific colors, fonts,
     or a brand style guide?"
    [If yes]: "Could you share those with me?"
    [If no]: "No problem -- we'll establish a visual direction from scratch."

Q10: "What kind of imagery fits your brand? Real photography of your
      team/products, professional stock photos, illustrations, icons,
      abstract graphics, or a mix?"
```

#### Phase 4: Site Structure and Content

```
Q11: "What pages do you think your website needs?"
     [I don't know]: "Here's what most [industry] websites include:
      [industry-specific defaults]. Does that sound right, or would you
      add or remove anything?"

Q12: "When someone visits your homepage, what's the ONE most important
      thing you want them to do? Examples: call you, fill out a form,
      buy something, book an appointment, learn about your services."

Q13: "Beyond the basics, are there any special features you need? Things
      like online booking, e-commerce, a blog, client login area, photo
      gallery, event calendar, or live chat?"

Q14: "Do you have the content ready for your website -- things like text
      for each page, photos of your team or products, testimonials? Or
      will that need to be created?"
     [Probe]: "Who will be responsible for writing the content?"
```

#### Phase 5: Practical Details

```
Q15: "Do most of your customers find you on their phone or computer?
      This helps us prioritize the mobile experience."

Q16: "What's your timeline? Is there a specific date or event you're
      working toward?"

Q17: "Do you have a budget range in mind for this project?"
     [Reluctant]: "Even a rough range helps me make sure I'm proposing
      something that fits. Would you say under $X, $X-$Y, or $Y+?"

Q18: "Is there anyone else who needs to be involved in approving the
      design? A business partner, marketing team, or other stakeholder?"
```

#### Phase 6: Wrap-Up

```
Q19: "Is there anything else about your business or vision for the
      website that I haven't asked about but should know?"

Q20: [SUMMARY] "Let me make sure I've got everything right..."
     [Read back key points, ask for confirmation/corrections]
```

### Adaptive Probing Rules

The agent should probe deeper when:

- The answer is vague or single-word ("We want it to look nice")
- The answer reveals complexity ("We sell both B2B and B2C")
- The answer contradicts an earlier answer
- A critical field (goals, audience, CTA) gets a weak response

The agent should move on when:

- The client gives a clear, specific answer
- The client says "I don't know" twice on the same topic
- The topic is Tier 3 (deferrable)
- The conversation has been on one topic for more than 3 exchanges

---

## 7. Sources

- [Jennifer Bourn -- Website Discovery Questionnaire](https://jenniferbourn.com/website-discovery-questionnaire/)
- [SEOptimer -- The Ultimate Website Design Questionnaire](https://www.seoptimer.com/blog/website-design-questionnaire/)
- [Axon Garside -- 50 Questions for Your Website Brief](https://www.axongarside.com/guides/website-brief-template)
- [Smashing Magazine -- Designing Effective Conversational AI Experiences](https://www.smashingmagazine.com/2024/07/how-design-effective-conversational-ai-experiences-guide/)
- [Mind the Product -- Nine UX Best Practices for AI Chatbots](https://www.mindtheproduct.com/deep-dive-ux-best-practices-for-ai-chatbots/)
- [Figma -- What is Wireframing](https://www.figma.com/resource-library/what-is-wireframing/)
- [Figma -- Wireframe vs Mockup](https://www.figma.com/resource-library/wireframe-vs-mockup/)
- [HubSpot -- Website Wireframes](https://blog.hubspot.com/website/website-wireframe)
- [Webflow -- 7 Essential Things to Ask Clients](https://webflow.com/blog/questionnaire-for-website-design)
- [WebFX -- Client Design Brief Questions](https://www.webfx.com/blog/web-design/client-design-brief-questions/)
- [Marker.io -- Website Design Questionnaire](https://marker.io/blog/website-design-questionnaire)
- [NN/g -- Mood Boards in UX](https://www.nngroup.com/articles/mood-boards/)
- [Netguru -- Chatbot UX Tips 2025](https://www.netguru.com/blog/chatbot-ux-tips)
- [TELUS Digital -- 7 UX/UI Rules for Conversational AI](https://www.willowtreeapps.com/insights/willowtrees-7-ux-ui-rules-for-designing-a-conversational-ai-assistant)
