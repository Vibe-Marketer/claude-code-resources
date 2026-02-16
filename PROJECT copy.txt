# CarouselForge

## What This Is

An iOS-first mobile app that transforms any content source into branded Instagram/LinkedIn carousels. Not an image generator — a content intelligence system that applies persuasion frameworks to your business context, then generates visuals. Users paste a YouTube URL, drop call transcripts, or link competitor carousels, and get a complete post package (images + caption + hashtags) ready to publish.

## Core Value

**Turn any content into a branded carousel in under 60 seconds.**

Everything else can be imperfect — but the path from "I have this YouTube video / transcript / idea" to "carousel ready to post" must feel effortless.

## Requirements

### Validated

(None yet — ship to validate)

### Active

**Offer Doc Foundation**
- [ ] User provides website URL → auto-generate offer doc
- [ ] User answers "what do you sell / who to" → generate offer doc
- [ ] User can skip offer doc (not recommended, but allowed)
- [ ] Offer doc persists and informs all content generation

**Content Input Sources**
- [ ] YouTube video URL → extract content → generate carousel
- [ ] Instagram carousel URL → extract and remix with intensity slider
- [ ] LinkedIn carousel → extract and remix
- [ ] Call transcripts (batch upload) → extract hooks and ideas
- [ ] Raw idea/topic → generate carousel

**Text-First Generation**
- [ ] Generate hooks and copy before images
- [ ] Apply persuasion frameworks (AIDA, PAS, Hook-Value-CTA)
- [ ] Enforce text density limits (3-12 words on hooks, 10-15 on content slides)
- [ ] Dual-hook system (slides 1 AND 2 optimized as standalone hooks)

**Image Generation**
- [ ] Generate images after copy is finalized
- [ ] Visual consistency across all slides in a carousel
- [ ] Brand elements (logo, colors, style references) applied consistently

**Brand System**
- [ ] Skip brand setup initially (start creating immediately)
- [ ] Add logo, colors, style references later
- [ ] @mention system to reference brand elements in prompts

**Output & Publishing**
- [ ] Full post package: images + caption + hashtags
- [ ] Open Instagram directly on phone to post
- [ ] Open LinkedIn directly to post
- [ ] Schedule posts for later
- [ ] Save images to phone

**Remix Engine**
- [ ] Intensity slider: "inspired by" to "direct adaptation"
- [ ] Same structure, user's words
- [ ] Extract insight, create original take

**Monetization**
- [ ] Subscription tiers (weekly/starter/pro)
- [ ] No credits, no usage caps

### Out of Scope

- Android app — iOS first, Android in future milestone
- Web app — mobile-first, web later if needed
- Video/Reels generation — carousels only for v1
- Real-time chat/collaboration — single-user or async team workflows
- Direct Instagram API posting — too brittle, open native app instead

## Context

**The Insight:** The carousel research revealed that text-image separation is the architectural moat no competitor has built. Everyone generates text and images together, producing generic outputs. CarouselForge wins by optimizing copy through persuasion frameworks *before* touching image generation.

**Offer Doc:** Andrew has an existing offer doc concept/template — the "everything you need to know about a business to generate any content." This becomes the persistent intelligence layer that makes every carousel feel personalized, not generic.

**Content Extraction:** The real workflow problem isn't "make pretty images" — it's "I have this call/video/competitor post and I want to turn it into content for my brand." The extraction and remixing engine is the value, not the pixel-pushing.

**One-Click Promise:** Every interaction should reduce to minimal decisions. Website → offer doc. YouTube URL → carousel. No configuration screens, no onboarding friction. Get to value fast, add refinements later.

**Creator Workflow Pain:** Current carousel creation takes 1-3 hours. Some creators spend $1,500+/month on VAs just for this. Collapsing to under 60 seconds is the value prop.

## Constraints

- **Platform**: iOS native first — this is a mobile-first experience
- **Tech stack**: TBD after research phase (likely React Native or Swift, with AI APIs)
- **Existing asset**: Offer doc templates/thinking exist — productize, don't reinvent
- **Pricing model**: Subscription tiers ($19 weekly / $49 starter / $99 pro)
- **API dependency**: Image generation via external APIs (Imagen, FLUX, DALL-E, Ideogram)

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| iOS first, not cross-platform from day 1 | Focus on one platform, nail the UX, expand later | — Pending |
| Text-first, image-second architecture | Research shows this is the moat — optimize copy before pixels | — Pending |
| Skip brand setup on first use | One-Click Promise — get to value before asking for configuration | — Pending |
| Open native Instagram/LinkedIn apps vs. API posting | Instagram API is brittle and restricted; native share is reliable | — Pending |
| Offer doc as foundation layer | Persistent business context that compounds — can't be commoditized | — Pending |
| Remix intensity slider | User decides how close to source material — ethical flexibility | — Pending |

---
*Last updated: 2026-01-19 after initialization*
