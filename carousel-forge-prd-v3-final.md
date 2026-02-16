# CarouselForge PRD
## AI-Powered Instagram Carousel Generator Built with Claude Code

**Version:** 3.0 (Final)  
**Created for:** Andrew Naegele  
**Build Platform:** Claude Code via Vibe Code (vibecode.dev)

---

## Executive Summary

Build a personalized Instagram carousel creation studio that leverages the best AI image models—eliminating expensive SaaS wrapper fees. Based on the proven architecture from Riley Brown's Thumbnail Studio (which cloned Crea's $1B interface in 34 minutes), adapted for multi-slide Instagram content.

**Target Outcome:** Generate unlimited professional Instagram carousels using AI with a simple subscription model.

---

## Problem Statement

Existing carousel tools have three fatal flaws:

1. **Credit Systems & Usage Caps** — Crea charges compute units that drain mid-project. Canva limits AI features. Creators constantly worry about running out.

2. **Generic Interfaces** — Built for everyone, optimized for no one. You're forced to navigate features you'll never use.

3. **No Brand Consistency** — Creating cohesive multi-slide carousels requires manually maintaining visual consistency across 5-10 images.

**The Solution:** A custom-built carousel studio using Claude Code that:
- Offers unlimited carousel generation within subscription
- Saves brand elements (logos, faces, style references) for instant @mention access
- Generates entire carousel sequences with visual coherence
- Deploys privately for team use

---

## Pricing Model

**Weekly Plan:** $19/week  
- Unlimited carousel generation
- Full access to all features
- Ideal for testing or seasonal campaigns

**Monthly Plan:** $49/month (Starter) | $99/month (Pro)  
- Unlimited carousel generation
- Starter: Single user, 50 saved elements
- Pro: Team access (up to 5 users), unlimited elements, priority generation

**No credits. No usage caps. No surprise charges.**

---

## Core Features (Prioritized)

### Phase 1: MVP (Day 1 Build)

#### 1.1 Carousel Canvas
- **Slide Grid View** — Display 1-10 carousel slides in order (Instagram max = 10)
- **Aspect Ratio Options** — 4:5 portrait (default, recommended) or 1:1 square
- **Drag-to-Reorder** — Reposition slides within the carousel
- **Add/Remove Slides** — + button to add, X to remove individual slides

**Aspect Ratio Logic:**
| Ratio | Dimensions | Use Case |
|-------|------------|----------|
| **4:5 Portrait** | 1080 × 1350px | Default. Maximum screen coverage, highest engagement |
| 1:1 Square | 1080 × 1080px | Secondary. For brands requiring square format |

*Note: Landscape intentionally excluded — wastes 45% of mobile screen real estate.*

#### 1.2 Prompt Interface
- **Single Input Field** — Clean text input for image generation prompts
- **@Element Trigger** — Type @ to show popup of saved brand elements
- **Slide Targeting** — Generate for "all slides" or specific slide numbers
- **Aspect Ratio Selector** — Left-aligned dropdown, 4:5 selected by default

#### 1.3 Elements System (The Killer Feature)
This is what makes the tool 10x more useful than generic generators.

**Element Types:**
| Type | Example | Triggered By |
|------|---------|--------------|
| Face/Person | Your headshot, client photos | @Andrew, @ClientName |
| Logo | Brand logos, icons | @CallVaultLogo, @VibeyLogo |
| Style Reference | Competitor carousel, aesthetic | @HormosiStyle, @LinearStyle |
| Color Palette | Brand colors | @VibeyColors |
| Typography | Font styles captured from images | @BoldHeadlines |

**Element Management:**
- Upload image → Name it → Auto-assigned color tag
- Edit name/color anytime
- Elements stored in database, persist across sessions
- Show full aspect ratio (not cropped squares)

#### 1.4 Image Generation Engine

**Primary Model: Nano Banana Pro (Google's Imagen 3)**
- Best text rendering of any model
- Excellent style consistency
- Direct API access via Google AI Studio

**Fallback Models:**
- FLUX 1.1 Pro (via Replicate) — Best photorealism
- DALL-E 3 (via OpenAI) — Reliable, good text
- Ideogram 2.0 — Superior text-in-image

**Model Selection Logic:**
```
IF prompt contains text overlay → Ideogram 2.0 or Nano Banana
IF prompt is photorealistic person → FLUX 1.1 Pro  
IF prompt is illustration/graphic → Nano Banana Pro
DEFAULT → Nano Banana Pro
```

#### 1.5 Generation Queue
- **Parallel Generation** — Generate multiple slides simultaneously
- **Queue Status** — Show pending/generating/complete states
- **Non-Blocking UI** — Continue typing while images generate
- **Most Recent = Top Left** — New images appear in position 1

---

### Phase 2: Power Features (Week 1)

#### 2.1 Carousel Templates
Pre-built prompt sequences for common carousel types:

**Hook → Value → CTA Template:**
```
Slide 1: Bold statement with @BrandLogo, text: "[HOOK]"
Slides 2-8: Key points with consistent @StyleReference
Slide 9: Summary slide
Slide 10: CTA with @BrandLogo and "Save this post"
```

**Story Arc Template:**
```
Slide 1: Problem statement (dark/moody)
Slides 2-4: Agitation (tension builds)
Slides 5-7: Solution reveal (brighter)
Slides 8-10: Transformation (aspirational)
```

**Listicle Template:**
```
Slide 1: "X Things That [Promise]" with @BrandLogo
Slides 2-9: One point per slide, numbered
Slide 10: "Follow for more" CTA
```

#### 2.2 Instagram Import
Extract style references directly from Instagram content.

**Instagram Post Import:**
- Paste Instagram post URL → Extract all carousel images
- Save individual slides as style reference elements
- Auto-detect aspect ratio used
- Name elements by account handle + post date

**Instagram Profile Import:**
- Paste Instagram profile URL → Show recent posts grid
- Select specific posts to import as style references
- Bulk import top-performing posts (by engagement if available)

**Import Sources:**
| Source | What It Extracts | Use Case |
|--------|-----------------|----------|
| Instagram Post URL | All carousel slides | Clone competitor style |
| Instagram Profile | Recent post thumbnails | Build style library from creator |
| Direct Image Upload | Single image | Manual style reference |

**Technical Implementation:**
- Use Instagram's oEmbed API for public posts
- Fallback: Scrape via proxy service (RapidAPI Instagram scrapers)
- Store extracted images with source attribution

#### 2.3 Pinterest Import (Style Mining)
- Paste Pinterest pin URL → Extract image as style reference
- Paste Pinterest board URL → Show pins grid for selection
- Ideal for mood boards and aesthetic references

#### 2.4 Batch Variations
- Generate 3-4 variations of each slide
- Compare side-by-side
- Select winners into final carousel

---

### Phase 3: Team & Export (Week 2)

#### 3.1 Export Options
- **ZIP Download** — All slides numbered (01.png, 02.png...)
- **Individual Download** — Single slide export
- **Caption Generator** — AI-written captions matching carousel content
- **Alt Text Generator** — Accessibility descriptions for each slide

#### 3.2 Carousel History
- Save completed carousels with names
- View generation history
- Re-edit previous carousels
- Duplicate as starting point

#### 3.3 Team Sharing (Pro Plan)
- Invite team members via email
- Shared elements library across team
- Usage dashboard per user

---

## Technical Architecture

### Stack Decision

**Build Platform: Claude Code via Vibe Code (vibecode.dev)**

Why this stack:
- Same approach proven in Riley Brown's original build
- Built-in APIs for image models (no key management)
- Instant deployment with shareable URL
- Database included for elements/history
- Claude Opus 4.5 for intelligent code generation

### API Integrations

| Service | Purpose |
|---------|---------|
| Nano Banana Pro | Primary image generation |
| Replicate (FLUX) | Photorealistic fallback |
| OpenAI (DALL-E 3) | Text-heavy fallback |
| Ideogram API | Best text rendering |
| Instagram oEmbed | Public post extraction |
| RapidAPI Instagram | Profile/private scraping |
| Pinterest API | Pin extraction |
| Stripe | Subscription billing |

### Database Schema

```sql
-- Users table
users {
  id: uuid PRIMARY KEY
  email: string NOT NULL UNIQUE
  plan: enum('weekly', 'starter', 'pro') 
  subscription_status: enum('active', 'canceled', 'past_due')
  stripe_customer_id: string
  created_at: timestamp
}

-- Teams table (Pro plan)
teams {
  id: uuid PRIMARY KEY
  name: string
  owner_id: uuid REFERENCES users
  created_at: timestamp
}

-- Team members
team_members {
  team_id: uuid REFERENCES teams
  user_id: uuid REFERENCES users
  role: enum('owner', 'member')
  added_at: timestamp
}

-- Elements table
elements {
  id: uuid PRIMARY KEY
  name: string NOT NULL
  image_url: string NOT NULL
  element_type: enum('face', 'logo', 'style', 'palette', 'typography')
  color_tag: string (hex)
  source_platform: enum('upload', 'instagram', 'pinterest') DEFAULT 'upload'
  source_url: string (original post/pin URL)
  created_at: timestamp
  user_id: uuid REFERENCES users
  team_id: uuid REFERENCES teams (nullable, for shared elements)
}

-- Carousels table
carousels {
  id: uuid PRIMARY KEY
  name: string
  slide_count: int
  aspect_ratio: enum('4:5', '1:1') DEFAULT '4:5'
  user_id: uuid REFERENCES users
  created_at: timestamp
  updated_at: timestamp
}

-- Slides table
slides {
  id: uuid PRIMARY KEY
  carousel_id: uuid REFERENCES carousels
  position: int (1-10)
  prompt: text
  image_url: string
  elements_used: jsonb (array of element IDs)
  model_used: string
  generated_at: timestamp
}

-- Generation queue
generation_queue {
  id: uuid PRIMARY KEY
  slide_id: uuid REFERENCES slides
  status: enum('pending', 'generating', 'complete', 'failed')
  started_at: timestamp
  completed_at: timestamp
  error_message: text
}
```

### UI Component Structure

```
App
├── Header
│   ├── Logo (CarouselForge)
│   ├── Carousel Name (editable)
│   ├── Export Button
│   └── Account/Plan Badge
├── Sidebar (Left)
│   ├── Elements Tab
│   │   ├── Element Grid (full aspect ratio)
│   │   ├── Add Element Button
│   │   │   ├── Upload Image
│   │   │   ├── Instagram URL Input
│   │   │   └── Pinterest URL Input
│   │   └── Element Edit Modal
│   └── Templates Tab
│       └── Template Cards
├── Main Canvas (Center)
│   ├── Slide Grid (1-10 slides)
│   │   └── Slide Card
│   │       ├── Image Preview
│   │       ├── Slide Number Badge
│   │       ├── Download Icon (faint, bold on hover)
│   │       ├── Insert to Prompt Icon
│   │       └── Delete Icon
│   └── Add Slide Button (+)
├── Prompt Bar (Bottom)
│   ├── Reference Images (dragged in)
│   ├── Text Input with @mention support
│   ├── Aspect Ratio Dropdown (4:5 default)
│   ├── Slide Target Selector (All / Specific)
│   └── Generate Button (white bg, black icon)
└── Image Viewer Modal
    ├── Full Image
    ├── Left/Right Arrows
    ├── Keyboard Navigation (← →)
    └── Action Buttons (Download, Insert to Prompt)
```

---

## UI/UX Specifications

### Visual Design

**Background:** Dark charcoal gray (#1a1a1a) with subtle grid texture  
**Cards:** Slightly lighter (#2a2a2a) with soft shadows  
**Accent:** White text, colored element tags  
**Generate Button:** White background, black enter icon

### Interaction Patterns

**@Mention Behavior:**
1. User types @
2. Popup appears with element grid
3. Filter as user continues typing
4. Click or Enter to select
5. Element name appears in prompt with color highlight
6. Multiple elements supported in single prompt

**Drag & Drop:**
- Drag generated image from canvas → drops into prompt as reference
- Drag slide card → reorder within carousel
- Drag external image → opens Add Element modal

**Keyboard Shortcuts:**
| Key | Action |
|-----|--------|
| Enter | Generate (when in prompt field) |
| ← → | Navigate slides in viewer modal |
| Esc | Close modals |
| Cmd+S | Export carousel |
| Cmd+N | New carousel |

---

## Prompt Engineering for Consistency

### Carousel Coherence Prompt Wrapper

When generating slides 2-10, automatically prepend:

```
Maintain visual consistency with the carousel series:
- Same color palette and lighting
- Consistent typography style
- Matching compositional balance
- Unified illustration/photo style
- Aspect ratio: [4:5 or 1:1] — optimize composition for vertical/square format

Previous slides context: [auto-injected from slide 1 generation]
```

### Element Reference Injection

When user types @ElementName, inject:

```
Reference image [ElementName]: [image_url]
Important: Incorporate this element naturally into the composition.
For faces: maintain likeness while matching the scene.
For logos: preserve exact design, adjust scale appropriately.
For styles: match the visual aesthetic, color grading, and composition.
```

---

## Build Sequence (Claude Code Prompts)

### Prompt 1: Foundation
```
Build an Instagram carousel creation app called CarouselForge.

Core requirements:
- Look up Nano Banana Pro documentation for image generation
- Clean dark interface with charcoal gray background (#1a1a1a) and subtle grid texture
- Left sidebar for Elements management
- Center canvas showing carousel slides (1-10 max)
- Bottom prompt bar with @mention support
- Generate button: white bg, black enter icon

Aspect ratio options: 4:5 portrait (default) and 1:1 square only.
No landscape option.

Output dimensions:
- 4:5 = 1080 × 1350px
- 1:1 = 1080 × 1080px

When user types @, show popup of saved elements.
Elements are reference images saved with names and color tags.
Store elements and generated images in database.
```

### Prompt 2: Elements System
```
Implement the Elements system:

1. Add Element modal with three input methods:
   a) Upload image directly from device
   b) Paste Instagram post URL — extract images from the carousel/post
   c) Paste Pinterest pin URL — extract the pin image
   
2. For Instagram URLs:
   - Use oEmbed API to fetch post data
   - If carousel, show all slides and let user select which to save
   - Auto-name element as "@handle_date" (e.g., "hormozi_jan2025")
   - Store source URL for attribution

3. For Pinterest URLs:
   - Extract pin image
   - Auto-name from pin title or board name

4. Element display:
   - Show full aspect ratio (not cropped squares)
   - Color tag visible on each element card
   - Small source icon (Instagram/Pinterest/Upload) in corner
   - Edit button for name/color changes
   - Delete with confirmation

5. @mention in prompt:
   - Typing @ triggers element popup
   - Filter results as user types
   - Selected element appears in its assigned color in the prompt text
   - Multiple elements supported in single prompt
   - Don't bold the text, just change color
```

### Prompt 3: Generation Engine
```
Implement multi-slide generation:

1. Aspect ratio selector: 4:5 (default), 1:1
2. Slide targeting: generate for all slides or specific slide numbers (e.g., "slides 3-5")
3. Parallel generation queue — generate multiple at once
4. Non-blocking UI — user can keep typing while generating
5. New images appear top-left (position 1), pushing others right

When generating with @elements:
- Inject element images as reference inputs to Nano Banana
- Add consistency wrapper for slides 2+
- Store which elements were used per slide in database

Show generation status on each slide card: pending → generating → complete
```

### Prompt 4: Canvas Interactions
```
Add canvas features:

1. Drag slides to reorder positions within carousel
2. Drag generated image from canvas into prompt area as reference
3. Click slide to open full viewer modal

4. Viewer modal features:
   - Large image display
   - Left/right arrows for navigation
   - Keyboard navigation (← →) between slides
   - Download button (faint icon, full button on hover)
   - "Insert to Prompt" button (same hover behavior)
   
5. Slide card hover state:
   - Show faint action icons (download, insert, delete)
   - Icons become bold/visible on hover
   - Slight scale-up animation

6. Keep prompt text and reference images after pressing Enter
   - Don't clear the input field after generation
   - Allow rapid iteration on same prompt
```

### Prompt 5: Export & Polish
```
Final features:

1. Export:
   - ZIP download all slides (01.png, 02.png, 03.png...)
   - Individual slide download from hover menu
   
2. Carousel management:
   - Editable carousel name in header
   - Auto-save to history
   - Load previous carousels from sidebar
   - Duplicate existing carousel as starting point
   
3. UI Polish:
   - Smooth animations on all interactions
   - Loading skeletons during generation
   - Error states with retry option
   - Empty state: paintbrush icon + "Create your first carousel"
   
4. Templates section in sidebar:
   - Hook → Value → CTA
   - Story Arc
   - Listicle
   - Clicking template pre-populates prompt sequence for all 10 slides
```

### Prompt 6: Subscription & Auth
```
Add Stripe subscription billing:

1. Plans:
   - Weekly: $19/week
   - Starter: $49/month (single user, 50 elements max)
   - Pro: $99/month (5 users, unlimited elements)

2. Auth flow:
   - Sign up with email
   - Stripe Checkout for plan selection
   - Manage subscription in account settings

3. Plan enforcement:
   - Check subscription status before generation
   - Show upgrade prompt if on Starter and hitting element limit
   - Team invite only available on Pro plan

4. Account UI:
   - Plan badge in header
   - Account settings page with billing management
   - Usage stats (carousels created, elements saved)
```

---

## Success Metrics

### MVP Launch (Day 1)
- [ ] Generate single image with @element reference
- [ ] Save and retrieve elements from database
- [ ] Display carousel grid (up to 10 slides)
- [ ] Export carousel as ZIP
- [ ] 4:5 aspect ratio working correctly

### Week 1
- [ ] Instagram post import working
- [ ] Pinterest pin import working
- [ ] 3+ elements used in single prompt successfully
- [ ] Carousel history saved and loadable
- [ ] Templates generating multi-slide sequences

### Week 2
- [ ] Stripe subscription integration live
- [ ] Team invite working on Pro plan
- [ ] Batch variations (3-4 per slide)
- [ ] Caption generation for carousels
- [ ] 50+ carousels created without issues

---

## Risk Mitigation

| Risk | Mitigation |
|------|------------|
| Nano Banana API changes | FLUX and DALL-E fallbacks implemented |
| Instagram API restrictions | Multiple scraping fallbacks (RapidAPI, Apify) |
| Pinterest API limits | Direct image URL extraction as backup |
| Rate limiting | Queue system with exponential backoff |
| Image inconsistency across slides | Seed locking, style reference injection |

---

## Future Roadmap (Post-MVP)

1. **Brand Kits** — Save complete brand packages (colors, fonts, logos, styles)
2. **A/B Testing** — Generate multiple carousel versions, track performance
3. **Direct Scheduling** — Buffer/Later integration for posting
4. **Video Slides** — Support for Reels-style mixed media carousels
5. **Voice Prompting** — Whisper integration for speaking prompts
6. **Analytics Dashboard** — Track generation patterns, popular elements
7. **Caption AI** — Generate carousel captions with hooks and CTAs
8. **Hashtag Suggestions** — AI-powered hashtag recommendations
9. **Competitor Monitoring** — Auto-import new posts from tracked accounts

---

## Appendix: Key Learnings from Original Build

From Riley Brown's 34-minute Thumbnail Studio build:

1. **Start with core feature** — Elements system was the differentiator, not fancy UI
2. **Iterate fast** — 6-7 prompts total, rapid testing between each
3. **UI details matter** — Spent time on hover states, colors, subtle textures
4. **Don't over-scope** — No auth in MVP, internal tool first
5. **Use built-in APIs** — Vibe Code's API tab eliminates key management headaches
6. **Clear context periodically** — After many prompts, clear Claude Code context to avoid confusion
7. **Voice your prompts** — He used Whisper Flow to speak prompts faster than typing

---

## Quick Reference: Aspect Ratios

**Use 4:5 Portrait (1080 × 1350px)** — Default for everything
- Maximum mobile screen coverage
- Highest engagement potential
- Industry standard for carousel content

**Use 1:1 Square (1080 × 1080px)** — Only when required
- Brand guidelines mandate squares
- Cross-posting to platforms that don't support 4:5
- Grid aesthetic consistency on profile

**Never use Landscape** — Wastes 45% of screen real estate

---

## Quick Reference: Import Sources

| Want to copy... | Import from... | How |
|-----------------|----------------|-----|
| Competitor carousel style | Instagram post URL | Paste URL → Select slides → Save as @elements |
| Creator's overall aesthetic | Instagram profile | Browse posts → Select multiple → Bulk import |
| Mood board / visual direction | Pinterest pin or board | Paste URL → Extract images |
| Your own brand assets | Direct upload | Drag & drop or file picker |

---

## Quick Reference: Pricing

| Plan | Price | Users | Elements | Best For |
|------|-------|-------|----------|----------|
| Weekly | $19/week | 1 | 50 | Testing, short campaigns |
| Starter | $49/month | 1 | 50 | Solo creators, coaches |
| Pro | $99/month | 5 | Unlimited | Agencies, teams |

All plans include unlimited carousel generation.

---

*Document Version: 3.0 Final*  
*Last Updated: January 2025*  
*Build Platform: Claude Code via vibecode.dev*
