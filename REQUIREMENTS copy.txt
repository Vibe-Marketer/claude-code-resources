# Requirements: CarouselForge

**Defined:** 2026-01-19
**Core Value:** Turn any content into a branded carousel in under 60 seconds

## v1 Requirements

Requirements for initial release. Each maps to roadmap phases.

### Foundation

- [ ] **FOUND-01**: User sees consent modal before any data goes to AI services (Apple 5.1.2(i) compliance)
- [ ] **FOUND-02**: User can set up brand kit (colors, fonts, logo)
- [ ] **FOUND-03**: User can create/edit offer doc (business context)
- [ ] **FOUND-04**: Offer doc auto-generates from website URL
- [ ] **FOUND-05**: Offer doc generates from "what do you sell / who to" questions
- [ ] **FOUND-06**: User data syncs across devices via CloudKit

### Carousel Editor

- [ ] **EDIT-01**: User can create new carousel
- [ ] **EDIT-02**: User can add/remove slides (1-10 max)
- [ ] **EDIT-03**: User can reorder slides via drag
- [ ] **EDIT-04**: User can edit text directly on slides (WYSIWYG)
- [ ] **EDIT-05**: User can undo/redo actions
- [ ] **EDIT-06**: User can select aspect ratio (4:5 portrait or 1:1 square)
- [ ] **EDIT-07**: User can apply templates to carousel

### Content Sources

- [ ] **SRC-01**: User can generate carousel from raw idea/topic
- [ ] **SRC-02**: User can paste YouTube URL to extract content
- [ ] **SRC-03**: User can paste web URL/article to extract content
- [ ] **SRC-04**: User can upload call transcripts (batch)
- [ ] **SRC-05**: User can paste competitor carousel URL to remix
- [ ] **SRC-06**: User can adjust remix intensity (inspired by -> direct adaptation)

### AI Generation

- [ ] **GEN-01**: System generates text using offer doc context
- [ ] **GEN-02**: System applies persuasion frameworks (AIDA, PAS, Hook-Value-CTA)
- [ ] **GEN-03**: System optimizes slides 1 AND 2 as standalone hooks
- [ ] **GEN-04**: System enforces text density limits (3-12 words hooks, 10-15 content)
- [ ] **GEN-05**: System generates images with brand consistency
- [ ] **GEN-06**: User sees generation progress (streaming/progressive reveal)

### Output & Publishing

- [ ] **OUT-01**: User can export carousel as PNG images
- [ ] **OUT-02**: User can export carousel as PDF
- [ ] **OUT-03**: User can save images to camera roll
- [ ] **OUT-04**: System generates caption with carousel
- [ ] **OUT-05**: System generates relevant hashtags
- [ ] **OUT-06**: System generates first comment text
- [ ] **OUT-07**: User can open Instagram directly to post
- [ ] **OUT-08**: User can open LinkedIn directly to post

### Monetization

- [ ] **PAY-01**: User can subscribe monthly ($49 starter / $99 pro)
- [ ] **PAY-02**: User can subscribe annually (discounted)
- [ ] **PAY-03**: Subscription managed via RevenueCat
- [ ] **PAY-04**: Free tier with limited generations

## v2 Requirements

Deferred to future release. Tracked but not in current roadmap.

### Scheduling

- **SCHED-01**: User can schedule carousel for future posting
- **SCHED-02**: User receives reminder when scheduled post is due
- **SCHED-03**: User can view scheduled post calendar

### Platform Expansion

- **PLAT-01**: Android app
- **PLAT-02**: Desktop web app
- **PLAT-03**: Direct API posting to Instagram/LinkedIn

### Collaboration

- **COLLAB-01**: User can invite team members
- **COLLAB-02**: Team shares brand kit and offer doc
- **COLLAB-03**: Usage tracking per team member

## Out of Scope

Explicitly excluded. Documented to prevent scope creep.

| Feature | Reason |
|---------|--------|
| Generic graphic design | Canva territory - not our market |
| Full social media management | Buffer/Hootsuite territory - different product |
| Video/Reels generation | Complexity explosion, carousels only for v1 |
| Real-time collaborative editing | Solo creators are primary target |
| Template marketplace | Two-sided marketplace is different business |
| Auto-posting via API | Instagram/LinkedIn APIs are brittle, constant changes |

## Traceability

Which phases cover which requirements. Updated during roadmap creation.

| Requirement | Phase | Phase Name | Status |
|-------------|-------|------------|--------|
| FOUND-01 | Phase 1 | Foundation | Pending |
| FOUND-02 | Phase 1 | Foundation | Pending |
| FOUND-03 | Phase 1 | Foundation | Pending |
| FOUND-04 | Phase 1 | Foundation | Pending |
| FOUND-05 | Phase 1 | Foundation | Pending |
| FOUND-06 | Phase 1 | Foundation | Pending |
| EDIT-01 | Phase 2 | Manual Carousel Editor | Pending |
| EDIT-02 | Phase 2 | Manual Carousel Editor | Pending |
| EDIT-03 | Phase 2 | Manual Carousel Editor | Pending |
| EDIT-04 | Phase 2 | Manual Carousel Editor | Pending |
| EDIT-05 | Phase 2 | Manual Carousel Editor | Pending |
| EDIT-06 | Phase 2 | Manual Carousel Editor | Pending |
| EDIT-07 | Phase 2 | Manual Carousel Editor | Pending |
| SRC-01 | Phase 3 | Content Extraction Pipeline | Pending |
| SRC-02 | Phase 3 | Content Extraction Pipeline | Pending |
| SRC-03 | Phase 3 | Content Extraction Pipeline | Pending |
| SRC-04 | Phase 3 | Content Extraction Pipeline | Pending |
| SRC-05 | Phase 3 | Content Extraction Pipeline | Pending |
| SRC-06 | Phase 3 | Content Extraction Pipeline | Pending |
| GEN-01 | Phase 4 | AI Text Generation | Pending |
| GEN-02 | Phase 4 | AI Text Generation | Pending |
| GEN-03 | Phase 4 | AI Text Generation | Pending |
| GEN-04 | Phase 4 | AI Text Generation | Pending |
| GEN-05 | Phase 4 | AI Text Generation | Pending |
| GEN-06 | Phase 4 | AI Text Generation | Pending |
| OUT-01 | Phase 5 | Output & Publishing | Pending |
| OUT-02 | Phase 5 | Output & Publishing | Pending |
| OUT-03 | Phase 5 | Output & Publishing | Pending |
| OUT-04 | Phase 5 | Output & Publishing | Pending |
| OUT-05 | Phase 5 | Output & Publishing | Pending |
| OUT-06 | Phase 5 | Output & Publishing | Pending |
| OUT-07 | Phase 5 | Output & Publishing | Pending |
| OUT-08 | Phase 5 | Output & Publishing | Pending |
| PAY-01 | Phase 6 | Monetization & Polish | Pending |
| PAY-02 | Phase 6 | Monetization & Polish | Pending |
| PAY-03 | Phase 6 | Monetization & Polish | Pending |
| PAY-04 | Phase 6 | Monetization & Polish | Pending |

**Coverage:**
- v1 requirements: 28 total
- Mapped to phases: 28
- Unmapped: 0

---
*Requirements defined: 2026-01-19*
*Last updated: 2026-01-20 after roadmap creation*
