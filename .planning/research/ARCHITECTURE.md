# Architecture Research: CarouselForge

**Domain:** iOS Mobile AI Content Creation
**Researched:** 2026-01-19
**Confidence:** HIGH (based on official Apple documentation and verified patterns)

## Summary

CarouselForge requires a **layered, modular architecture** optimized for iOS-first development with SwiftUI. The recommended architecture combines MVVM with Clean Architecture principles, organizing code into feature modules with clear dependency injection. The system centers on a **content pipeline** that processes inputs through extraction, generation, and export stages, with persistent local storage via SwiftData and CloudKit sync.

Key architectural insight: The "text-first, image-second" moat means the **text generation pipeline is the critical path**. Image generation is secondary/optional and should be architecturally isolated to avoid blocking the core carousel creation flow.

---

## System Components

### Layer 1: Presentation (SwiftUI Views)

**Responsibility:** Display UI, capture user input, observe state changes
**Technology:** SwiftUI with @Observable pattern (iOS 17+)

| Component | Responsibility |
|-----------|----------------|
| `CarouselEditorView` | Main editing canvas for carousel slides |
| `ContentSourceView` | Input selection (URL, YouTube, text, offer doc) |
| `BrandManagerView` | Brand element configuration |
| `ExportView` | Preview and sharing interface |
| `SettingsView` | App configuration, subscription status |

**Pattern:** Views are thin, declarative, and stateless. All business logic lives in ViewModels.

### Layer 2: ViewModel / Presentation Logic

**Responsibility:** Transform domain data for display, handle user actions, coordinate services
**Technology:** @Observable classes with Swift Concurrency (async/await)

| Component | Responsibility | Dependencies |
|-----------|----------------|--------------|
| `CarouselViewModel` | Manages carousel editing state | ContentService, BrandService |
| `ContentSourceViewModel` | Handles input source selection and extraction | ExtractionService |
| `GenerationViewModel` | Orchestrates text/image generation | TextGenerationService, ImageGenerationService |
| `BrandViewModel` | Manages brand assets | BrandRepository |
| `ExportViewModel` | Handles export and sharing | ExportService, ShareService |

### Layer 3: Domain / Business Logic

**Responsibility:** Core business rules, use cases, entity definitions
**Technology:** Pure Swift, protocol-based

| Component | Responsibility |
|-----------|----------------|
| `Carousel` | Core entity - slides, layout, brand applied |
| `Slide` | Individual carousel slide with text, image, styling |
| `OfferDoc` | Persistent context document with offer details |
| `Brand` | Colors, fonts, logo, styling rules |
| `ContentSource` | Abstraction over input types (URL, YouTube, text) |

**Use Cases:**
- `CreateCarouselUseCase` - Orchestrates carousel creation from source
- `ApplyBrandUseCase` - Applies brand styling to carousel
- `GenerateTextUseCase` - Coordinates AI text generation
- `ExportCarouselUseCase` - Produces export artifacts

### Layer 4: Data / Services

**Responsibility:** External integrations, persistence, API communication
**Technology:** SwiftData, URLSession, third-party SDKs

| Component | Responsibility | External Dependency |
|-----------|----------------|---------------------|
| `TextGenerationService` | AI text generation | OpenAI API (via backend proxy) |
| `ImageGenerationService` | AI image generation | DALL-E or Stable Diffusion API |
| `ContentExtractionService` | URL/YouTube content extraction | Transcript APIs, SwiftSoup |
| `BrandRepository` | Brand asset persistence | SwiftData |
| `CarouselRepository` | Carousel persistence | SwiftData + CloudKit |
| `OfferDocRepository` | Offer document persistence | SwiftData + CloudKit |
| `SubscriptionService` | Payment handling | RevenueCat / StoreKit 2 |
| `ShareService` | Social sharing | UIActivityViewController, Instagram API |

---

## Data Flow

### Primary Flow: Content to Carousel

```
[Input Source] --> [Extraction] --> [Text Generation] --> [Carousel Assembly] --> [Export]
     |                  |                  |                      |                 |
     v                  v                  v                      v                 v
  YouTube URL      Transcript API     OpenAI API            SwiftData         Share Sheet
  Web URL          SwiftSoup          (via proxy)           Local Store       Instagram
  Raw Text         ReadabilityKit                           CloudKit Sync     LinkedIn
  Offer Doc        Local Storage
```

### Detailed Pipeline Stages

**Stage 1: Content Ingestion**
```
User selects source type
    --> ContentSourceViewModel validates input
    --> ExtractionService dispatches to appropriate extractor
    --> Raw content returned with metadata
```

**Stage 2: Context Assembly**
```
Raw content + Offer Doc (if available)
    --> ContextBuilder assembles prompt context
    --> Brand voice guidelines injected
    --> Structured context package ready for AI
```

**Stage 3: Text Generation**
```
Context package --> TextGenerationService
    --> Backend proxy --> OpenAI API
    --> Structured slide content returned (JSON)
    --> Parse into Slide entities
```

**Stage 4: Carousel Assembly**
```
Slide entities + Brand settings
    --> ApplyBrandUseCase applies styling
    --> Carousel entity with complete slides
    --> Persisted to SwiftData
```

**Stage 5: Image Generation (Optional)**
```
Slide text --> ImageGenerationService (user-initiated)
    --> Backend proxy --> DALL-E API
    --> Image URLs returned
    --> Downloaded and attached to slides
```

**Stage 6: Export**
```
Carousel --> ExportService
    --> Renders slides as images
    --> Applies final brand watermark (if applicable)
    --> Returns exportable image array
    --> ShareService presents share sheet
```

### Offer Doc as Persistent Context

The Offer Doc is a **first-class citizen** that persists across sessions:

```
OfferDoc
    |-- Business description
    |-- Target audience
    |-- Key benefits
    |-- Tone/voice guidelines
    |-- Example phrases
    |-- Pain points addressed

Every generation request includes:
    [Immediate content] + [Offer Doc context] --> AI prompt
```

---

## External Integrations

### AI Services (via Backend Proxy)

**CRITICAL:** Never expose API keys in the iOS app. All AI calls go through a backend proxy.

| Service | Purpose | Integration Pattern |
|---------|---------|---------------------|
| OpenAI GPT-4 | Text generation | REST API via proxy server |
| DALL-E 3 | Image generation | REST API via proxy server |

**Backend Proxy Architecture:**
```
iOS App --> Your Backend --> OpenAI
              |
              +-- Rate limiting
              +-- Usage tracking
              +-- Response caching
              +-- Content filtering
              +-- Cost management
```

**Proxy Benefits:**
- API key security (never on device)
- Request logging and analytics
- Response caching for common patterns
- Cost controls and usage quotas
- Content moderation before responses reach device

### Content Extraction APIs

| Source | API/Library | Notes |
|--------|-------------|-------|
| YouTube | youtube-transcript.io or Supadata | Rate limited, may need backend proxy |
| Web URLs | SwiftSoup (on-device) | Direct HTML parsing |
| Web URLs | ReadabilityKit (on-device) | Extract readable content |

### Social Sharing

| Platform | Integration | Limitations |
|----------|-------------|-------------|
| Instagram Stories | URL scheme + share extension | Requires app installed |
| Instagram Feed | UIActivityViewController | Limited customization |
| LinkedIn | UIActivityViewController | Standard share sheet |
| General | UIActivityViewController | All platforms via share sheet |

### Payments

| Provider | Purpose | Why |
|----------|---------|-----|
| RevenueCat | Subscription management | Cross-platform, handles StoreKit complexity |
| StoreKit 2 | Native fallback | Direct Apple integration if needed |

---

## Suggested Build Order

### Phase 1: Foundation (Weeks 1-2)
**Goal:** Core infrastructure that everything else builds on

1. **Project Setup**
   - Xcode project with SwiftUI App lifecycle
   - SwiftData schema for core entities
   - Basic navigation structure (TabView or NavigationStack)

2. **Core Entities**
   - `Carousel`, `Slide`, `Brand`, `OfferDoc` models
   - SwiftData persistence layer
   - Basic CRUD operations

3. **Brand Management (MVP)**
   - Color palette storage
   - Font selection (system fonts initially)
   - Brand preview

**Rationale:** Everything depends on data models and persistence. Get this right first.

### Phase 2: Manual Carousel Creation (Weeks 3-4)
**Goal:** Users can create carousels without AI (validates core UX)

1. **Carousel Editor**
   - Slide creation/deletion/reordering
   - Text editing per slide
   - Brand application to slides

2. **Export System**
   - Render slides as images
   - Basic share sheet integration
   - Save to photo library

**Rationale:** Validates core product value before AI complexity. Users can manually create carousels.

### Phase 3: Content Extraction Pipeline (Weeks 5-6)
**Goal:** Ingest content from various sources

1. **URL Extraction**
   - SwiftSoup integration for web content
   - ReadabilityKit for clean article extraction

2. **YouTube Integration**
   - Transcript API integration (via backend)
   - Video metadata extraction

3. **Offer Doc System**
   - Offer doc creation UI
   - Persistence and retrieval
   - Context injection preparation

**Rationale:** Input pipeline must work before AI generation makes sense.

### Phase 4: AI Text Generation (Weeks 7-8)
**Goal:** Core value proposition - AI-generated carousel text

1. **Backend Proxy Setup**
   - Simple serverless function (Vercel, AWS Lambda, or CloudFlare Workers)
   - OpenAI API integration
   - Request/response handling

2. **Text Generation Service**
   - Prompt engineering for carousel content
   - Offer doc context injection
   - Structured output parsing (JSON mode)

3. **Generation UI**
   - Generation progress indicator
   - Error handling and retry
   - Edit/regenerate individual slides

**Rationale:** This is the moat. Text generation quality determines product success.

### Phase 5: Polish & Subscriptions (Weeks 9-10)
**Goal:** Production-ready with monetization

1. **Subscription Integration**
   - RevenueCat SDK setup
   - Paywall UI
   - Entitlement checking

2. **CloudKit Sync**
   - Enable NSPersistentCloudKitContainer
   - Sync testing across devices

3. **Image Generation (Optional)**
   - DALL-E integration via backend
   - Image attachment to slides
   - Generation queue management

**Rationale:** Monetization after core value proven. Image generation is enhancement, not core.

### Phase 6: Launch Prep (Weeks 11-12)
**Goal:** App Store ready

1. **Onboarding**
   - First-run experience
   - Offer doc setup flow

2. **Analytics & Crash Reporting**
   - Usage analytics
   - Error tracking

3. **App Store Assets**
   - Screenshots
   - App Store description
   - Review preparation

---

## Mobile-Specific Considerations

### Offline Capability

**Strategy:** Offline-first with sync-when-available

| Feature | Offline Behavior |
|---------|------------------|
| Carousel editing | Fully offline (SwiftData) |
| Brand management | Fully offline |
| Offer doc editing | Fully offline |
| Content extraction (URLs) | Requires network |
| AI generation | Requires network |
| Export to photos | Fully offline |
| Share to social | Requires network |

**Implementation:**
- SwiftData as source of truth
- Queue generation requests when offline
- Process queue when connectivity returns
- Clear UI indication of offline state

### Performance

**Memory Management:**
- Load slides lazily in editor
- Release image memory for off-screen slides
- Use @Attribute(.externalStorage) for images in SwiftData

**Image Handling:**
- Generate carousel images at export time, not edit time
- Cache rendered slides for preview
- Use thumbnail previews in editor, full resolution at export

**Background Processing:**
- Use BGProcessingTask for batch image generation
- Queue AI requests, don't block UI
- Save incremental progress for long operations

### Battery Considerations

| Operation | Battery Impact | Mitigation |
|-----------|----------------|------------|
| AI API calls | Low (network only) | Batch requests where possible |
| Image rendering | Medium | Render on-demand, not continuously |
| CloudKit sync | Low | System-managed scheduling |
| Content extraction | Low | Cache results aggressively |

### State Management

**Recommended:** @Observable with SwiftData

```swift
@Observable
class CarouselViewModel {
    var carousel: Carousel?
    var isGenerating = false
    var error: Error?

    private let repository: CarouselRepository
    private let generationService: TextGenerationService

    // State changes automatically update SwiftUI views
}
```

**State Persistence:**
- Use SwiftData for document state (carousels, brands, offer docs)
- Use @AppStorage for preferences (theme, default settings)
- Use @SceneStorage for transient UI state (selected tab, scroll position)

---

## Architecture Diagram

```
+------------------------------------------------------------------+
|                        CarouselForge iOS App                      |
+------------------------------------------------------------------+
|                                                                   |
|  +--------------------+  +--------------------+  +-------------+  |
|  |  Presentation      |  |  Presentation      |  | Settings    |  |
|  |  (Carousel Editor) |  |  (Content Source)  |  | (Profile)   |  |
|  +--------+-----------+  +--------+-----------+  +------+------+  |
|           |                       |                     |         |
|  +--------v-----------+  +--------v-----------+  +------v------+  |
|  | CarouselViewModel  |  | SourceViewModel    |  | SettingsVM  |  |
|  +--------+-----------+  +--------+-----------+  +------+------+  |
|           |                       |                     |         |
+-----------|------------------------|-----------------------|-------+
|           |        DOMAIN LAYER    |                     |         |
|  +--------v-----------------------v---------------------v------+  |
|  |                      Use Cases                              |  |
|  |  CreateCarousel | ApplyBrand | GenerateText | ExportCarousel|  |
|  +------------------------+------------------------------------+  |
|                           |                                       |
|  +------------------------v------------------------------------+  |
|  |                      Entities                               |  |
|  |     Carousel | Slide | Brand | OfferDoc | ContentSource     |  |
|  +-------------------------------------------------------------+  |
+-------------------------------------------------------------------+
|                        DATA LAYER                                 |
|  +-------------+  +---------------+  +-------------------------+  |
|  | SwiftData   |  | CloudKit Sync |  | API Services            |  |
|  | Repository  |  | Manager       |  | (via Backend Proxy)     |  |
|  +------+------+  +-------+-------+  +------------+------------+  |
|         |                 |                       |               |
+---------|-----------------|-----------------------|---------------+
          |                 |                       |
          v                 v                       v
    +----------+     +-----------+          +-------------+
    | SQLite   |     | iCloud    |          | Your        |
    | (Local)  |     | (Apple)   |          | Backend     |
    +----------+     +-----------+          +------+------+
                                                   |
                                            +------v------+
                                            | OpenAI API  |
                                            | DALL-E API  |
                                            | Transcript  |
                                            +-------------+
```

---

## Dependency Injection Strategy

**Recommended:** Protocol-based DI with Environment injection for SwiftUI

```swift
// 1. Define protocols
protocol TextGenerationServiceProtocol {
    func generate(content: String, context: OfferDoc?) async throws -> [SlideContent]
}

// 2. Create concrete implementations
class TextGenerationService: TextGenerationServiceProtocol {
    private let apiClient: APIClient

    func generate(content: String, context: OfferDoc?) async throws -> [SlideContent] {
        // Implementation
    }
}

// 3. Create mock for testing
class MockTextGenerationService: TextGenerationServiceProtocol {
    var mockResult: [SlideContent] = []

    func generate(content: String, context: OfferDoc?) async throws -> [SlideContent] {
        return mockResult
    }
}

// 4. Inject via Environment
@main
struct CarouselForgeApp: App {
    @State private var dependencies = AppDependencies()

    var body: some Scene {
        WindowGroup {
            ContentView()
                .environment(dependencies)
        }
    }
}
```

**Module Structure:**
```
CarouselForge/
├── App/
│   ├── CarouselForgeApp.swift
│   └── AppDependencies.swift
├── Features/
│   ├── CarouselEditor/
│   │   ├── Views/
│   │   ├── ViewModels/
│   │   └── Components/
│   ├── ContentSource/
│   ├── BrandManager/
│   ├── Export/
│   └── Settings/
├── Domain/
│   ├── Entities/
│   ├── UseCases/
│   └── Protocols/
├── Data/
│   ├── Repositories/
│   ├── Services/
│   └── Networking/
└── Shared/
    ├── Extensions/
    ├── Utilities/
    └── DesignSystem/
```

---

## Technology Decisions Summary

| Decision | Choice | Rationale |
|----------|--------|-----------|
| UI Framework | SwiftUI | Modern, declarative, Apple's future direction |
| Architecture | MVVM + Clean | Balance of simplicity and separation |
| Persistence | SwiftData | Native, modern, CloudKit integration |
| Sync | CloudKit via SwiftData | Free, Apple-native, automatic |
| State Management | @Observable | iOS 17+, cleaner than ObservableObject |
| Networking | URLSession + async/await | Native, no dependencies |
| AI Integration | Backend proxy | Security, cost control, flexibility |
| Subscriptions | RevenueCat | Handles complexity, analytics included |
| HTML Parsing | SwiftSoup | Pure Swift, well-maintained |

---

## Sources

**iOS Architecture:**
- [Clean Architecture for SwiftUI](https://nalexn.github.io/clean-architecture-swiftui)
- [2025's Best SwiftUI Architecture: MVVM + Clean + Feature Modules](https://medium.com/@minalkewat/2025s-best-swiftui-architecture-mvvm-clean-feature-modules-3a369a22858c)
- [Dependency Injection in Swift 2025](https://medium.com/@varunbhola1991/dependency-injection-in-swift-2025-clean-architecture-better-testing-7228f971446c)
- [Modularizing iOS Applications with SwiftUI and SPM](https://nimblehq.co/blog/modern-approach-modularize-ios-swiftui-spm)

**Persistence & Sync:**
- [Apple Developer: Syncing a Core Data Store with CloudKit](https://developer.apple.com/documentation/coredata/syncing-a-core-data-store-with-cloudkit)
- [Offline Sync Strategies: Core Data + CloudKit + SwiftData](https://ravi6997.medium.com/offline-sync-strategies-core-data-cloudkit-swiftdata-in-ios-apps-3760684567fd)
- [SwiftData Architecture Patterns and Practices](https://azamsharp.com/2025/03/28/swiftdata-architecture-patterns-and-practices.html)

**AI Integration:**
- [OpenAI API Integration Best Practices](https://www.openassistantgpt.io/blogs/openai-api-integration-best-practices)
- [MacPaw/OpenAI Swift Package](https://github.com/MacPaw/OpenAI)
- [AI in Mobile App Development 2025 Guide](https://www.thedroidsonroids.com/blog/ai-mobile-app-development-guide)

**Content Extraction:**
- [SwiftSoup GitHub](https://github.com/scinfu/SwiftSoup)
- [Best YouTube Transcript APIs 2025](https://www.socialkit.dev/blog/best-youtube-transcript-apis-2025)

**Payments:**
- [iOS In-App Subscription Tutorial with StoreKit 2](https://www.revenuecat.com/blog/engineering/ios-in-app-subscription-tutorial-with-storekit-2-and-swift/)
- [RevenueCat SDK 5.0 - StoreKit 2 Update](https://www.revenuecat.com/blog/engineering/revenuecat-sdk-5-0-the-storekit-2-update/)

**Background Tasks:**
- [Apple Developer: Background Tasks](https://developer.apple.com/documentation/backgroundtasks)
- [Mastering Background Tasks in iOS](https://medium.com/@dhruvmanavadaria/mastering-background-tasks-in-ios-bgtaskscheduler-silent-push-and-background-fetch-with-6b5c502d7448)
