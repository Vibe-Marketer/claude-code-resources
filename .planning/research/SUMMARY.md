# Research Summary: CarouselForge

**Project:** CarouselForge - iOS AI-Powered Carousel Generation App
**Domain:** iOS Mobile AI Content Creation
**Researched:** 2026-01-19
**Overall Confidence:** HIGH

## Executive Summary

CarouselForge should be built as a **native Swift/SwiftUI iOS app** targeting iOS 17+, using SwiftData for persistence, RevenueCat for subscriptions, and OpenAI APIs (proxied through a backend) for AI generation. The iOS-native approach is non-negotiable given the requirements for share extensions, native polish expected in content creation tools, and the iOS-first strategy that eliminates cross-platform's main advantage. The recommended architecture is MVVM + Clean Architecture with feature modules, centering on a content pipeline that processes inputs through extraction, generation, and export stages.

The project's **unique moat is the "Offer Doc" concept** - persistent business context that informs all carousel generation. No competitors offer this. Combined with a text-first workflow (opposite of template-first competitors) and true iOS-native mobile editing, CarouselForge has genuine differentiation opportunities. However, most competitors are web-first with poor mobile UX, creating a significant gap CarouselForge can exploit.

**Three risks could kill this project:** (1) App Store rejection under Guideline 5.1.2(i) - Apple's November 2025 rule requiring explicit consent before sharing data with third-party AI services; (2) AI API cost explosion that makes unit economics unsustainable ($0.50-1.80 per carousel in API costs); (3) Content extraction legal liability from YouTube/Instagram ToS violations. These must be addressed in Phase 1 architecture decisions, not bolted on later.

## Recommended Stack

Native Swift 6.0+ with SwiftUI for iOS 17+. SwiftData for persistence with CloudKit sync. OpenAI GPT-4o for text generation with structured JSON outputs. OpenAI GPT Image 1.5 and FLUX via Replicate for image generation. RevenueCat for subscription management. URLSession with async/await for networking. All AI API calls proxied through a backend (Supabase Edge Functions recommended) to protect API keys and enable cost control.

**Core technologies:**

| Technology | Purpose | Rationale |
|------------|---------|-----------|
| Swift 6.0 / SwiftUI (iOS 17+) | UI Framework | Apple's future direction, native feel critical for content creation, share extension support |
| SwiftData | Persistence | Modern Swift syntax, automatic SwiftUI binding, iOS 17+ acceptable for new app |
| OpenAI GPT-4o | Text generation | Structured outputs guarantee parseable JSON, best prompt adherence |
| OpenAI GPT Image 1.5 | Image generation | Superior text rendering for carousel headlines (critical) |
| RevenueCat | Subscriptions | 1.5 hours to first purchase vs 2 weeks with raw StoreKit, handles complexity |
| Supabase | Backend/Auth | PostgreSQL with RLS, Edge Functions for API proxy, good Swift SDK |

**What NOT to use:** React Native/Flutter (share extension pain, non-native feel), Core Data (SwiftData simpler for greenfield), raw StoreKit 2 (2 weeks dev time), Firebase (NoSQL less suited for relational offer doc data), DALL-E 3 (deprecated May 2026), hardcoded API keys (extractable from binary).

## Feature Priorities

### Must Have (Table Stakes)

Users will leave without these:

- AI content generation from prompt (core value prop)
- Brand kit (colors, fonts, logo) - 77% cite brand consistency as critical
- Template library (non-designers need scaffolding)
- PDF export (LinkedIn requires PDF for carousels)
- PNG/image export (Instagram requires images)
- Multiple aspect ratios (LinkedIn 4:5, Instagram 4:5, etc.)
- Text editing on slides (WYSIWYG expected)
- Undo/redo (basic editing expectation)
- Mobile-optimized editing (touch-friendly, pinch-zoom, drag-reposition)

### Should Have (Differentiators)

Features that create competitive advantage:

- **Offer Document (persistent business context)** - UNIQUE, biggest moat opportunity
- **Text-first, image-second workflow** - UNIQUE approach, matches how pros work
- YouTube URL to carousel (time saver, many competitors have this)
- URL/article to carousel (content repurposing is 65% of marketer workflows)
- Caption + hashtag generation (full post package)
- First comment text (LinkedIn engagement hack)
- Native iOS share sheets (mobile-native advantage over web tools)

### Defer to v2+

Anti-features to deliberately NOT build:

- Built-in image generation (DALL-E/Midjourney style) - use stock photos/uploads instead
- Full social media management suite (Buffer/Hootsuite territory)
- Auto-posting directly to platforms (OAuth complexity, constant API changes)
- Desktop web app (diffuses iOS focus)
- Collaborative editing (solo creators are primary target)
- Template marketplace (two-sided marketplace is different business)
- Generic graphic design features (Canva territory)

## Architecture Highlights

**Pattern:** MVVM + Clean Architecture with feature modules. Layered structure: Presentation (SwiftUI views) -> ViewModel (@Observable classes) -> Domain (use cases, entities) -> Data (repositories, services).

**Critical architectural insight:** The "text-first, image-second" moat means the text generation pipeline is the critical path. Image generation is secondary/optional and should be architecturally isolated.

**Major components:**

1. **Content Pipeline** - Ingestion -> Context Assembly -> Text Generation -> Carousel Assembly -> Export
2. **Offer Doc System** - Persistent business context that injects into every generation prompt
3. **Backend Proxy** - All AI calls through proxy for key security, cost control, rate limiting, caching
4. **Export Service** - ImageRenderer for SwiftUI-to-image, share sheet integration

**Data Flow:**
```
[Input Source] -> [Extraction] -> [Text Generation] -> [Carousel Assembly] -> [Export]
     |                |                 |                     |                  |
  YouTube URL    Transcript API    OpenAI API (proxy)    SwiftData         Share Sheet
  Web URL        SwiftSoup                               CloudKit Sync     Instagram/LinkedIn
  Offer Doc      Local Storage
```

**Key decisions:**
- SwiftData as source of truth, queue generation requests when offline
- @Observable for state management (iOS 17+)
- Protocol-based dependency injection for testability
- Feature modules: CarouselEditor, ContentSource, BrandManager, Export, Settings

## Critical Risks

**Top 5 pitfalls that could kill the project:**

### 1. Apple Guideline 5.1.2(i) Non-Compliance
**Risk:** App Store rejection (15% of apps rejected for privacy violations in 2025).
**Prevention:** Build explicit consent modal FIRST - before any data goes to OpenAI/Claude. Modal must specify provider name, data types shared, purpose. Test against App Review checklist before submission.

### 2. AI API Cost Explosion
**Risk:** Per-user costs exceed subscription revenue. Single carousel costs $0.50-1.80 in API calls.
**Prevention:** Tiered model strategy (GPT-4o-mini for drafts, GPT-4o for final). Cache offer doc analysis (90% savings via prompt caching). Batch image generation. Per-user generation limits. Cost dashboard from day 1.

### 3. Content Extraction Legal Liability
**Risk:** Cease and desist from YouTube/Instagram for ToS violations.
**Prevention:** Use official YouTube Data API for metadata only. Accept user-pasted transcripts rather than extraction. Plan for "save to camera roll + open app" flow, not direct posting. Get legal review on "remix" feature before building.

### 4. StoreKit 2 Implementation Failures
**Risk:** Subscription purchases fail silently, App Store rejection.
**Prevention:** Use RevenueCat to abstract complexity. If custom: use Transaction validation, NOT receipts (receipts = rejection). Test on physical devices with sandbox accounts. Handle Transaction.updates app-wide.

### 5. AI Generation Latency Destroying UX
**Risk:** Users abandon app (80% abandon after 3 bad uses). Full carousel takes 30-90 seconds serial.
**Prevention:** Design for latency, not around it. Parallelize image generation. Stream text generation. Progressive reveal (slide-by-slide). Set expectations upfront ("~60 seconds").

## Roadmap Implications

Based on research dependencies and risk mitigation priorities:

### Phase 1: Foundation
**Rationale:** Everything depends on data models, persistence, and the consent/privacy framework. Consent modal must be built FIRST to avoid App Store rejection.
**Delivers:** Core entities, SwiftData persistence, brand kit, basic carousel editor without AI.
**Addresses:** Template system, text editor, brand kit, undo/redo.
**Avoids:** Guideline 5.1.2(i) rejection by building consent flow upfront.

### Phase 2: Manual Carousel Creation
**Rationale:** Validate core UX before adding AI complexity. Users can manually create carousels.
**Delivers:** Carousel editor (create/delete/reorder slides), text editing, brand application, PDF/PNG export, share sheet.
**Addresses:** All table stakes editing features, export capabilities.
**Avoids:** Building AI without validated core product.

### Phase 3: Content Extraction Pipeline
**Rationale:** Input pipeline must work before AI generation makes sense.
**Delivers:** URL extraction (SwiftSoup), YouTube integration (with legal safeguards), Offer Doc system.
**Addresses:** URL to carousel, Offer Doc persistence.
**Avoids:** Legal risk by using official APIs and user-provided content.

### Phase 4: AI Text Generation (The Moat)
**Rationale:** This is the core value proposition. Text generation quality determines product success.
**Delivers:** Backend proxy setup, OpenAI integration with structured outputs, Offer Doc context injection, generation UI with progress.
**Addresses:** AI content generation from prompt, AI writing assistant.
**Avoids:** Cost explosion via tiered models and caching.

### Phase 5: Polish and Subscriptions
**Rationale:** Monetization after core value proven. Image generation is enhancement, not core.
**Delivers:** RevenueCat integration, paywall UI, CloudKit sync, optional image generation.
**Addresses:** Subscription tiers, cross-device sync.
**Avoids:** StoreKit failures by using RevenueCat.

### Phase 6: Full Post Package
**Rationale:** Complete the content creation workflow with caption, hashtags, first comment.
**Delivers:** Caption generation, hashtag generation, first comment text, unified export.
**Addresses:** Full post package output.

### Phase Ordering Rationale

1. **Consent and data models first** - App Store rejection risk is highest; get this right in Phase 1.
2. **Manual editing before AI** - Validates core UX, reduces dependency on AI working perfectly.
3. **Extraction before generation** - Can't generate without content to process.
4. **Text generation before monetization** - Need to prove value before asking for payment.
5. **Image generation is optional** - Text-first approach means carousels work without AI images.

### Research Flags

**Phases needing deeper research during planning:**
- **Phase 3 (Content Extraction):** Legal review needed for YouTube/Instagram extraction. API availability uncertain.
- **Phase 4 (AI Generation):** Prompt engineering for carousel format. Structured output schema design.
- **Phase 5 (Subscriptions):** Pricing strategy validation. RevenueCat paywall configuration.

**Phases with standard patterns (skip additional research):**
- **Phase 1 (Foundation):** SwiftData and SwiftUI patterns well-documented.
- **Phase 2 (Manual Editor):** Standard iOS editing patterns.
- **Phase 6 (Full Package):** Extension of Phase 4 generation patterns.

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | HIGH | Apple documentation, community consensus on SwiftUI/SwiftData for iOS 17+ apps |
| Features | MEDIUM-HIGH | Competitor analysis verified, user expectations clear, moat features are hypothesis |
| Architecture | HIGH | Clean Architecture well-documented, mobile patterns established |
| Pitfalls | HIGH | Official Apple guidelines, API documentation, legal precedents cited |

**Overall confidence:** HIGH

### Gaps to Address

1. **YouTube transcript reliability:** Swift package uses unofficial APIs, may break. Need fallback UX for manual paste. Test extensively before committing.

2. **Pricing validation:** Proposed $19/week tier has worst retention in industry. Need to validate pricing with user research. Consider dropping weekly tier entirely.

3. **Offer Doc effectiveness:** The moat hypothesis (persistent context improves quality) needs validation. Build feedback loops to measure if users see value.

4. **Instagram sharing specifics:** Instagram requires specific implementation (.ig/.igo file extensions). Test on physical devices early.

5. **iOS 26 SDK timeline:** If launching Q2 2026+, must use iOS 26 SDK (April 2026 requirement). May need to start development targeting that.

## Open Questions

1. Should weekly subscription tier be dropped? Industry data shows worst retention (3-6%).
2. Can on-device ML (Core ML) reduce API costs for text generation in v2?
3. How much offline functionality is expected? Full offline editing vs always-online generation.
4. Legal review outcome on competitor carousel "remix" feature - build or defer?
5. Partnership path for LinkedIn API access - pursue now or defer to post-launch?

## Sources

### Primary (HIGH confidence)
- Apple Developer Guidelines (5.1.2(i) requirements, StoreKit 2)
- OpenAI API Documentation (structured outputs, image generation, pricing)
- RevenueCat Documentation (SDK integration, subscription benchmarks)
- Supabase Documentation (Swift SDK, Edge Functions)

### Secondary (MEDIUM confidence)
- Competitor analysis (aiCarousels, PostNitro, Contentdrips, Draft AI)
- RevenueCat State of Subscription Apps 2025 (conversion/churn benchmarks)
- Community articles on SwiftUI architecture patterns

### Tertiary (LOW confidence - validate during implementation)
- YouTube transcript extraction methods (unofficial APIs)
- Instagram Graph API limits (change frequently)
- AI API cost projections (usage patterns will vary)

---
*Research completed: 2026-01-19*
*Ready for roadmap: yes*
