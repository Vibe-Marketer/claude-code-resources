# Stack Research: CarouselForge

**Project:** iOS-first AI-powered carousel generation app
**Researched:** 2026-01-19
**Overall Confidence:** HIGH

## Summary

For CarouselForge, a **native Swift/SwiftUI** approach is the clear winner over cross-platform alternatives. The app requires deep iOS integration (share extensions, photo library, native UI polish) that cross-platform frameworks struggle with. The recommended stack centers on SwiftUI with SwiftData for persistence, RevenueCat for subscriptions, OpenAI GPT-4o for text/image generation, and Supabase for lightweight backend needs.

The stack prioritizes:
1. **Developer velocity** - SwiftUI + SwiftData enables rapid iteration
2. **AI integration flexibility** - Direct API calls to OpenAI/Replicate
3. **Native polish** - Critical for a content creation tool
4. **Subscription simplicity** - RevenueCat handles the complexity

---

## Recommended Stack

### iOS Framework

| Technology | Version | Purpose | Rationale |
|------------|---------|---------|-----------|
| **Swift** | 6.0+ | Language | Modern concurrency (async/await), type safety, performance. Swift 6 brings 40% faster development and 60% fewer runtime errors vs legacy approaches. |
| **SwiftUI** | iOS 17+ | UI Framework | Declarative, reactive updates, native feel. SwiftUI is now production-ready and Apple's clear future direction. |
| **UIKit** | iOS 17+ | Selective use | Share extensions, complex image manipulation, areas where SwiftUI falls short. |

**Why Native over Cross-Platform:**
- Instagram/LinkedIn share extensions require native iOS integration
- Image canvas manipulation benefits from Core Graphics/Metal access
- User expectation for premium feel in content creation apps
- Performance: native achieves 100% vs 80-90% for cross-platform
- Single platform (iOS-first) eliminates cross-platform's main advantage (code sharing)

**Alternatives Rejected:**
- **React Native**: 80-90% native performance, share extension complexity, JavaScript debugging pain
- **Flutter**: Better performance than RN but still non-native share extensions, Dart ecosystem smaller
- **Kotlin Multiplatform**: Emerging but not mature for iOS-first apps

**Confidence:** HIGH - Native Swift/SwiftUI is the clear choice for iOS-first apps requiring deep platform integration.

---

### AI/LLM APIs

#### Text Generation

| Technology | Model | Purpose | Rationale |
|------------|-------|---------|-----------|
| **OpenAI API** | GPT-4o | Primary text generation | Best prompt adherence, structured outputs, fastest iteration. |
| **OpenAI API** | GPT-4o-mini | High-volume/draft generation | 10x cheaper, good enough for first drafts |

**Why OpenAI over Anthropic Claude:**
- **Structured Outputs**: OpenAI's JSON Schema enforcement guarantees parseable carousel slide content
- **Image generation integration**: Single vendor for text + image (see below)
- **Swift ecosystem**: More community examples and libraries

**Implementation Notes:**
- Use `response_format: { "type": "json_schema" }` for guaranteed JSON responses
- Define schemas for carousel slides (headline, body, CTA, visual direction)
- No official Swift SDK - use URLSession with async/await directly

**Confidence:** HIGH - OpenAI's structured outputs solve the carousel content generation problem elegantly.

#### Image Generation

| Technology | Model | Purpose | Rationale |
|------------|-------|---------|-----------|
| **OpenAI API** | GPT Image 1.5 (gpt-image-1) | Primary image generation | Superior text rendering (critical for carousel slides), deep prompt understanding |
| **Replicate** | FLUX.1 Schnell | Fast previews | 1-2 second generation for rapid iteration |
| **Replicate** | FLUX.1 Pro | Final renders | Best photorealism when needed |

**Why This Combination:**
- GPT-4o native image generation excels at text-in-image (carousel headlines)
- FLUX via Replicate provides speed options and photorealism
- Both are API-based, no on-device ML complexity

**DALL-E 3 Deprecation Warning:** DALL-E 3 will stop being supported on 05/12/2026. Plan migration to GPT Image models.

**Confidence:** HIGH - GPT-4o for text-heavy carousel images is well-documented; FLUX for photorealism is proven.

#### Content Extraction

| Technology | Purpose | Rationale |
|------------|---------|-----------|
| **YouTubeTranscript (Swift Package)** | YouTube transcript extraction | Native Swift async/await, no API key required |
| **SwiftSoup** | URL/webpage scraping | Pure Swift HTML parsing, CSS selectors, mature library |
| **OpenAI GPT-4o** | Content summarization | Extract key points from transcripts/scraped content |

**YouTubeTranscript Package:** Uses unofficial YouTube API via HTML scraper and Innertube API. Supports language selection, async/await.

**Confidence:** MEDIUM - YouTube transcript extraction is unofficial API, may break. Have fallback plan (manual paste).

---

### Local Persistence

| Technology | Version | Purpose | Rationale |
|------------|---------|---------|-----------|
| **SwiftData** | iOS 17+ | Primary persistence | Modern Swift syntax, SwiftUI integration, async/await support |
| **UserDefaults** | - | Settings/preferences | Simple key-value for non-sensitive config |
| **Keychain (via Valet)** | - | API keys, tokens | Secure storage with biometric protection |

**Why SwiftData over Core Data:**
- Declarative model definition with `@Model` macro
- Automatic SwiftUI binding updates
- Modern async/await concurrency
- No NSManagedObject boilerplate

**SwiftData Limitations to Note:**
- iOS 17+ only (acceptable for new app)
- Lightweight migrations only (no heavyweight custom migrations)
- Cloud sync more limited than Core Data + CloudKit

**Confidence:** HIGH - SwiftData is production-ready as of iOS 18, perfect for greenfield iOS 17+ apps.

---

### Backend/Database

| Technology | Purpose | Rationale |
|------------|---------|-----------|
| **Supabase** | User data, offer docs, templates | PostgreSQL with real-time, Row-Level Security, Edge Functions |
| **Supabase Edge Functions** | API proxying, webhooks | Serverless Deno/TypeScript, low latency |
| **Supabase Auth** | User authentication | Sign in with Apple, email/password |

**Why Supabase over Firebase:**
- **Relational data model**: Offer docs have structured relationships (user -> brand -> templates)
- **SQL queries**: Complex queries for template search, analytics
- **Open source**: No vendor lock-in, can self-host if needed
- **pgvector**: Future AI features (semantic search over user content)

**Why Not Local-Only:**
- Offer docs need backup/sync across devices
- Subscription status verification needs server-side truth
- Future: sharing templates, collaboration

**Confidence:** HIGH - Supabase is well-suited for structured data with modern iOS integration.

---

### Subscription/Payments

| Technology | Purpose | Rationale |
|------------|---------|-----------|
| **RevenueCat** | Subscription management | Cross-platform entitlements, analytics, paywalls |
| **StoreKit 2** | Underlying iOS API | RevenueCat wraps this, handles complexity |

**Why RevenueCat over Raw StoreKit 2:**
- **Development time**: 1.5 hours to first purchase vs 2 weeks for raw StoreKit
- **Annual API changes**: RevenueCat handles StoreKit evolution
- **Analytics**: Subscriber lifecycle, churn, conversion - beyond App Store Connect
- **Paywall A/B testing**: No-code paywall editor
- **Cross-platform ready**: If Android version needed later

**Pricing Context:**
- Free tier: Up to $2,500 MTR (monthly tracked revenue)
- Starter: $99/mo up to $10k MTR
- For MVP/early stage: Free tier is sufficient

**StoreKit 1 Deprecation:** Apple deprecated StoreKit 1 at WWDC 2024. RevenueCat SDK 5.0 uses StoreKit 2 by default for iOS 16+.

**Confidence:** HIGH - RevenueCat is industry standard, used by 75,000+ apps including OpenAI, Notion, Buffer.

---

### Networking

| Technology | Purpose | Rationale |
|------------|---------|-----------|
| **URLSession** | HTTP requests | Native async/await, no external dependency |
| **Codable** | JSON serialization | Native Swift, type-safe |

**Why URLSession over Alamofire:**
- Modern async/await APIs eliminate callback complexity
- No external dependency for straightforward API calls
- URLSession is sufficient for REST API consumption

**When to Add Alamofire:**
- Complex retry logic with token refresh
- Certificate pinning requirements
- Request queuing and prioritization

**Confidence:** HIGH - URLSession with async/await is the modern standard for Swift networking.

---

### Image Processing & Export

| Technology | Purpose | Rationale |
|------------|---------|-----------|
| **SwiftUI Canvas** | Carousel rendering | Declarative drawing, hardware-accelerated |
| **ImageRenderer** | PNG/JPEG export | Native SwiftUI-to-image conversion |
| **Core Graphics** | Advanced manipulation | When Canvas isn't enough |

**Canvas Capabilities:**
- Procedural drawing with GraphicsContext
- Metal-backed rendering performance
- Native SwiftUI integration

**Export Flow:**
1. Render carousel slide as SwiftUI View
2. Use `ImageRenderer` to convert to UIImage
3. Call `pngData()` for file export
4. Save to Photos or share via UIActivityViewController

**Confidence:** HIGH - Apple's documented approach for SwiftUI-to-image export.

---

### Share Extensions

| Technology | Purpose | Rationale |
|------------|---------|-----------|
| **Share Extension target** | System share sheet integration | Native iOS capability |
| **App Groups** | Data sharing between app and extension | Required for extension communication |
| **UIDocumentInteractionController** | Instagram-specific sharing | Instagram requires .ig/.igo file extensions |

**Instagram Integration:**
- Add `instagram-stories` and `instagram://` to LSApplicationQueriesSchemes
- Use UIDocumentInteractionController with `.ig` extension for photos
- Stories sharing requires specific URL scheme

**LinkedIn Integration:**
- Standard UIActivityViewController works
- No special SDK required for share sheet

**Confidence:** MEDIUM - Instagram sharing requires specific implementation; LinkedIn is straightforward.

---

### Key Libraries (Swift Package Manager)

| Library | Version | Purpose | Source |
|---------|---------|---------|--------|
| **RevenueCat/purchases-ios** | 5.x | Subscriptions | Official |
| **supabase-swift** | 2.x | Backend SDK | Official |
| **scinfu/SwiftSoup** | 2.x | HTML parsing | Community |
| **YoutubeTranscript** | Latest | YouTube transcripts | Community |
| **Square/Valet** | 4.x | Keychain wrapper | Square (Official) |

**Installation (Package.swift):**
```swift
dependencies: [
    .package(url: "https://github.com/RevenueCat/purchases-ios.git", from: "5.0.0"),
    .package(url: "https://github.com/supabase-community/supabase-swift.git", from: "2.0.0"),
    .package(url: "https://github.com/scinfu/SwiftSoup.git", from: "2.6.0"),
    .package(url: "https://github.com/nicktrienenern/YoutubeTranscript.git", from: "1.0.0"),
    .package(url: "https://github.com/square/Valet.git", from: "4.0.0")
]
```

---

## What NOT to Use

| Technology | Why Avoid |
|------------|-----------|
| **React Native / Flutter** | Overkill complexity for iOS-only; share extension pain; non-native feel for premium content app |
| **Core Data** | SwiftData is simpler for new iOS 17+ apps; Core Data's boilerplate slows iteration |
| **Raw StoreKit 2** | 2 weeks dev time vs 1.5 hours with RevenueCat; ongoing maintenance burden |
| **Firebase** | NoSQL less suited for relational offer doc data; vendor lock-in; more expensive at scale |
| **Alamofire** | Unnecessary dependency when URLSession + async/await suffices |
| **DALL-E 3** | Deprecated May 2026; migrate to GPT Image models now |
| **UserDefaults for secrets** | Plaintext storage; use Keychain via Valet instead |
| **Hardcoded API keys** | Extractable from binary; fetch from server, store in Keychain |
| **WKWebView for YouTube** | Overcomplex; use YouTubeTranscript package for transcripts |

---

## Security Considerations

### API Key Management

1. **Never hardcode** OpenAI/Replicate keys in source
2. **Remote fetch** keys from Supabase Edge Function on first launch
3. **Store in Keychain** using Valet with `kSecAttrAccessibleWhenPasscodeSetThisDeviceOnly`
4. **Rotate keys** via server-side config without app update

### Network Security

1. **HTTPS only** for all API calls (URLSession default)
2. **Certificate pinning** for Supabase connection (consider for v2)
3. **No logging** of API keys or user content in production

---

## Confidence Levels Summary

| Component | Confidence | Rationale |
|-----------|------------|-----------|
| Swift/SwiftUI | HIGH | Apple's clear direction, production-ready, deep iOS integration required |
| OpenAI GPT-4o (text) | HIGH | Structured outputs solve content generation; well-documented |
| OpenAI GPT Image (images) | HIGH | Superior text rendering for carousel slides |
| SwiftData | HIGH | Modern, SwiftUI-native, iOS 17+ acceptable for new app |
| Supabase | HIGH | Relational model fits offer docs; good Swift SDK |
| RevenueCat | HIGH | Industry standard, massive time savings, proven at scale |
| YouTubeTranscript | MEDIUM | Unofficial API may break; have fallback plan |
| Share Extensions | MEDIUM | Instagram requires specific implementation; needs testing |
| FLUX via Replicate | MEDIUM | Good for photorealism but secondary to OpenAI for text-heavy slides |

---

## Open Questions

1. **YouTube transcript reliability**: The Swift package uses unofficial APIs. Need fallback UX for manual transcript paste.

2. **Instagram API changes**: Instagram frequently updates sharing requirements. Monitor for changes during development.

3. **SwiftData migration path**: If complex migrations needed later, may need to add Core Data layer.

4. **On-device ML**: Could on-device models (Core ML) reduce API costs for text generation? Investigate for v2.

5. **Offline mode**: How much functionality should work offline? SwiftData + local image cache vs always-online?

---

## Sources

### iOS Development
- [2025 iOS Developer Roadmap: Swift 6 SwiftUI](https://ravi6997.medium.com/2025-ios-developer-roadmap-swift-6-swiftui-combine-and-modern-tooling-ed477320a814)
- [Native vs Cross-Platform Development 2025](https://eluminoustechnologies.com/blog/native-vs-cross-platform/)
- [SwiftUI Canvas Revolution 2025](https://ravi6997.medium.com/swiftuis-canvas-revolution-how-apple-s-new-drawing-api-is-transforming-ios-development-in-2025-ac0c1eb838df)

### AI/LLM
- [OpenAI Image Generation Guide](https://platform.openai.com/docs/guides/image-generation)
- [OpenAI Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)
- [FLUX vs DALL-E vs Midjourney Comparison](https://ulazai.com/flux-vs-dalle-midjourney/)
- [Replicate FLUX Models](https://replicate.com/collections/flux)

### Persistence & Backend
- [SwiftData vs Core Data 2025](https://distantjob.com/blog/core-data-vs-swiftdata/)
- [Supabase vs Firebase 2025](https://ravi6997.medium.com/supabase-vs-firebase-best-baas-for-ios-in-2025-04eff1136745)

### Subscriptions
- [RevenueCat vs StoreKit 2](https://www.revenuecat.com/blog/engineering/implementing-storekit/)
- [StoreKit 2 Overview](https://www.revenuecat.com/blog/engineering/storekit-2-overview/)

### Content Extraction
- [Swift Web Scraping with SwiftSoup](https://www.zenrows.com/blog/swift-web-scraping)
- [YouTubeTranscript Swift Package](https://github.com/topics/youtube-transcript)

### Security
- [iOS Keychain with Valet](https://www.blog.brightcoding.dev/2025/09/07/storing-secrets-in-ios-keychain-with-swift-a-complete-guide-using-squares-valet/)
- [Securing API Keys in SwiftUI](https://dev.to/msiatrak/securing-api-keys-in-swiftui-a-practical-guide-intro-3f91)

### Share Extensions
- [iOS Share Extension with SwiftUI](https://www.merrell.dev/ios-share-extension-with-swiftui-and-swiftdata/)
- [Sharing to Instagram with Swift](https://dogusyigitozcelik.medium.com/sharing-feeds-and-stories-to-instagram-with-swift-6162a679d9ce)
