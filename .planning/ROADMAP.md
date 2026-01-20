# Roadmap: CarouselForge

## Overview

CarouselForge delivers the "any content to carousel in 60 seconds" promise through six phases that build progressively from foundation to full product. Phase 1 establishes privacy compliance and brand/offer foundations. Phase 2 enables manual carousel creation without AI dependency. Phase 3 adds content extraction from external sources. Phase 4 introduces the text-first AI moat. Phase 5 completes the output pipeline. Phase 6 adds monetization and polish. Each phase delivers verifiable value and reduces risk incrementally.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: Foundation** - Privacy compliance, brand kit, offer doc, and data persistence
- [ ] **Phase 2: Manual Carousel Editor** - Create and edit carousels without AI
- [ ] **Phase 3: Content Extraction Pipeline** - YouTube, web, transcript, and remix inputs
- [ ] **Phase 4: AI Text Generation** - The moat: persuasion frameworks and text-first generation
- [ ] **Phase 5: Output & Publishing** - Export, caption, hashtags, and share to platforms
- [ ] **Phase 6: Monetization & Polish** - Subscriptions, free tier, and production readiness

## Phase Details

### Phase 1: Foundation
**Goal**: User can set up their business context and brand identity with App Store-compliant privacy
**Depends on**: Nothing (first phase)
**Requirements**: FOUND-01, FOUND-02, FOUND-03, FOUND-04, FOUND-05, FOUND-06
**Success Criteria** (what must be TRUE):
  1. User sees consent modal before any data leaves device to AI services
  2. User can create brand kit with colors, fonts, and logo
  3. User can create offer doc manually or auto-generate from website URL
  4. User can answer business questions to generate offer doc
  5. User data persists and syncs across their devices
**Plans**: TBD (estimated 5-7 plans)

Plans:
- [ ] 01-01: Project scaffolding and core data models
- [ ] 01-02: Privacy consent modal (Apple 5.1.2(i) compliance)
- [ ] 01-03: Brand kit creation and storage
- [ ] 01-04: Offer doc manual creation and editing
- [ ] 01-05: Offer doc auto-generation from URL
- [ ] 01-06: Offer doc generation from questions
- [ ] 01-07: CloudKit sync setup

### Phase 2: Manual Carousel Editor
**Goal**: User can create, edit, and manage carousels entirely without AI assistance
**Depends on**: Phase 1
**Requirements**: EDIT-01, EDIT-02, EDIT-03, EDIT-04, EDIT-05, EDIT-06, EDIT-07
**Success Criteria** (what must be TRUE):
  1. User can create a new carousel and add/remove slides (1-10)
  2. User can reorder slides via drag-and-drop
  3. User can edit text directly on slides (WYSIWYG)
  4. User can undo and redo editing actions
  5. User can select aspect ratio and apply templates
**Plans**: TBD (estimated 5-6 plans)

Plans:
- [ ] 02-01: Carousel data model and creation flow
- [ ] 02-02: Slide management (add/remove/reorder)
- [ ] 02-03: WYSIWYG text editing on slides
- [ ] 02-04: Undo/redo system
- [ ] 02-05: Aspect ratio selection
- [ ] 02-06: Template system and application

### Phase 3: Content Extraction Pipeline
**Goal**: User can generate carousels from external content sources (YouTube, web, transcripts, competitors)
**Depends on**: Phase 2
**Requirements**: SRC-01, SRC-02, SRC-03, SRC-04, SRC-05, SRC-06
**Success Criteria** (what must be TRUE):
  1. User can generate carousel from a raw idea or topic
  2. User can paste YouTube URL and extract content for carousel generation
  3. User can paste web URL/article and extract content for carousel generation
  4. User can upload call transcripts (batch) for idea extraction
  5. User can paste competitor carousel URL and remix with intensity slider
**Plans**: TBD (estimated 6-8 plans)

Plans:
- [ ] 03-01: Raw idea/topic input flow
- [ ] 03-02: YouTube URL extraction (transcript/metadata)
- [ ] 03-03: Web URL/article extraction (SwiftSoup)
- [ ] 03-04: Call transcript batch upload and parsing
- [ ] 03-05: Competitor carousel URL extraction
- [ ] 03-06: Remix intensity slider and transformation logic
- [ ] 03-07: Unified extraction pipeline architecture
- [ ] 03-08: Backend proxy for API key security

### Phase 4: AI Text Generation
**Goal**: System generates persuasion-optimized text using offer doc context before any images
**Depends on**: Phase 3
**Requirements**: GEN-01, GEN-02, GEN-03, GEN-04, GEN-05, GEN-06
**Success Criteria** (what must be TRUE):
  1. Generated text reflects offer doc business context
  2. Generated text follows persuasion frameworks (AIDA, PAS, Hook-Value-CTA)
  3. Slides 1 AND 2 work as standalone hooks (dual-hook system)
  4. Text density limits are enforced (3-12 words hooks, 10-15 content)
  5. User sees generation progress with streaming/progressive reveal
**Plans**: TBD (estimated 6-8 plans)

Plans:
- [ ] 04-01: OpenAI integration with structured outputs
- [ ] 04-02: Offer doc context injection into prompts
- [ ] 04-03: Persuasion framework prompt engineering (AIDA, PAS, Hook-Value-CTA)
- [ ] 04-04: Dual-hook system (slides 1 and 2)
- [ ] 04-05: Text density enforcement and validation
- [ ] 04-06: Generation progress UI with streaming
- [ ] 04-07: Image generation with brand consistency
- [ ] 04-08: Cost optimization (tiered models, caching)

### Phase 5: Output & Publishing
**Goal**: User can export complete post packages and share directly to Instagram/LinkedIn
**Depends on**: Phase 4
**Requirements**: OUT-01, OUT-02, OUT-03, OUT-04, OUT-05, OUT-06, OUT-07, OUT-08
**Success Criteria** (what must be TRUE):
  1. User can export carousel as PNG images or PDF
  2. User can save images directly to camera roll
  3. System generates caption, hashtags, and first comment text with carousel
  4. User can open Instagram directly to post (native share)
  5. User can open LinkedIn directly to post (native share)
**Plans**: TBD (estimated 5-7 plans)

Plans:
- [ ] 05-01: PNG image export (ImageRenderer)
- [ ] 05-02: PDF export for LinkedIn
- [ ] 05-03: Camera roll save integration
- [ ] 05-04: Caption generation
- [ ] 05-05: Hashtag generation
- [ ] 05-06: First comment text generation
- [ ] 05-07: Native share sheet (Instagram + LinkedIn)

### Phase 6: Monetization & Polish
**Goal**: App has sustainable business model with subscription tiers and production polish
**Depends on**: Phase 5
**Requirements**: PAY-01, PAY-02, PAY-03, PAY-04
**Success Criteria** (what must be TRUE):
  1. User can subscribe monthly ($49 starter / $99 pro)
  2. User can subscribe annually with discount
  3. Subscription status managed via RevenueCat
  4. Free tier exists with limited generations
**Plans**: TBD (estimated 4-5 plans)

Plans:
- [ ] 06-01: RevenueCat SDK integration
- [ ] 06-02: Subscription tiers and paywall UI
- [ ] 06-03: Annual subscription pricing
- [ ] 06-04: Free tier with generation limits
- [ ] 06-05: Production polish and App Store preparation

## Progress

**Execution Order:**
Phases execute in numeric order: 1 -> 2 -> 3 -> 4 -> 5 -> 6

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Foundation | 0/7 | Not started | - |
| 2. Manual Carousel Editor | 0/6 | Not started | - |
| 3. Content Extraction Pipeline | 0/8 | Not started | - |
| 4. AI Text Generation | 0/8 | Not started | - |
| 5. Output & Publishing | 0/7 | Not started | - |
| 6. Monetization & Polish | 0/5 | Not started | - |

---
*Roadmap created: 2026-01-20*
*Depth: comprehensive (6 phases, 41 estimated plans)*
