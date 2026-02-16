# Carousel Virality Research Prompt
## Understanding What Makes Carousels Genuinely Addictive

---

<session_initialization>
Before beginning research, verify today's date:
!`date +%Y-%m-%d`

Use this date when searching for "current" or "latest" information.
</session_initialization>

<research_objective>
Research what makes Instagram carousels genuinely viral, high-converting, and addictive—beyond basic hooks and engagement tactics.

**The core question:** If we could crack the code on carousels that people genuinely can't stop watching, that convert viewers into buyers, that spread organically—what would that look like? And how do we build a tool that produces them?

Purpose: Inform CarouselForge's core generation logic to create output that's genuinely better than competitors
Scope: Psychological patterns, structural formulas, visual design principles, text-image interplay
Output: carousel-virality-research.md with actionable insights for product architecture
</research_objective>

<context>
**Product background:**
- CarouselForge = AI-powered Instagram carousel generator
- Target: coaches, creators, agencies, solopreneurs
- Key differentiator potential: Generate carousels that actually work, not just "look nice"

**Market validation (already completed):**
- Carousels get 2.14x more engagement than single-image posts
- 10.15% average engagement rate
- 2x more likely to be saved than Reels
- Instagram expanded max to 20 slides
- Time pain is #1 signal (users spend 10+ hours on single carousels)

**Guiding philosophy (One-Click Promise):**
1. Gather Silently, Confirm Minimally
2. Radical Simplicity
3. Smart Defaults (every option has intelligent default)
4. Invisible Complexity (users see simple, systems handle complex)
5. Respect Cognitive Budget
6. One Click is the Ceiling (zero is better)

**The "how" question we're solving:**
"How do we deliver on this promise in a way that creates a moat? How can we generate one-click carousels that are genuinely high quality—virtually addictive—that convert buyers?"

**Hypothesis to explore:**
Separate text generation and image generation, render them separately, combine at end. This decoupling might enable:
- Better text optimization (persuasive, structured)
- Better image consistency (style-matched across slides)
- Smarter combination (text placement, visual hierarchy)
</context>

<research_scope>
<include>
**1. Carousel Psychology - What makes people swipe?**
- The "open loop" effect (curiosity gaps between slides)
- Pattern interrupt mechanics
- The dopamine loop of progressive revelation
- Why some carousels are saved but others aren't
- The "scroll stopper" first slide formula

**2. High-Converting Carousel Structures**
- Story arc templates that sell (not just engage)
- The difference between viral and converting
- How top coaches/creators structure money-making carousels
- Slide count optimization (when 5 beats 10, when 10 beats 5)
- The role of the final CTA slide

**3. Visual Design Principles**
- Color psychology in carousel context
- Typography choices that increase read-through
- Image vs. text-heavy slides—when each works
- Visual consistency patterns that don't bore
- The "thumb-stopping" visual formula

**4. Text-Image Interplay**
- Where text should live on each slide
- When to use pure image vs. text overlay vs. text-only
- How much text per slide for optimal engagement
- Font sizing hierarchy across carousel
- The role of whitespace

**5. The Creator Workflow Insight**
- What do top creators actually do when making carousels?
- Where do they spend most time?
- What decisions do they make that AI could replicate or improve?
- What parts are "creative" vs. "formula"?

**6. Offer Doc Integration**
- How does knowing buyer persona change carousel approach?
- How does competitive positioning appear in carousels?
- How do top coaches weave their offer into educational content?
</include>

<exclude>
- Basic Instagram algorithm mechanics (already known)
- Hashtag strategy (separate concern)
- Posting timing optimization (separate concern)
- Account growth tactics (outside scope)
- Technical implementation details (for planning phase)
</exclude>

<sources>
**Official/authoritative sources (use WebFetch):**
- Instagram @creators account recent carousel posts and analysis
- Later.com blog - carousel guides
- Buffer.com blog - carousel research
- Socialinsider.io - carousel benchmarks
- Sprout Social - carousel best practices

**Creator economy sources (use WebSearch):**
- "viral instagram carousel structure 2025"
- "carousel psychology swipe rate"
- "high converting carousel examples coaches"
- "carousel copywriting formulas"
- "instagram carousel visual hierarchy"
- "alex hormozi carousel strategy"
- "dickie bush carousel framework"
- "jasmine star carousel templates"
- "carousel first slide formula"
- "carousel CTA slide conversion"

**Academic/psychological sources:**
- Persuasion psychology applied to social media
- Visual hierarchy research
- Reading patterns on mobile
- Progressive disclosure UX patterns

**Reverse engineering sources:**
- Top-performing carousels from: @hormozi, @thejasminstar, @garyvee, @lewishowes, @brendonburchard
- Analyze: What structural patterns repeat? What visual patterns repeat?
</sources>
</research_scope>

<verification_checklist>
**Carousel Structure Patterns:**
- [ ] Document at least 5 distinct high-performing carousel structures
- [ ] Verify with engagement data where available
- [ ] Distinguish "viral" vs "converting" structures

**Visual Design Rules:**
- [ ] Confirm color/contrast recommendations with multiple sources
- [ ] Verify typography best practices for mobile reading
- [ ] Document text density guidelines with evidence

**Psychology Patterns:**
- [ ] Verify open loop / curiosity gap effectiveness
- [ ] Confirm first slide "hook" mechanics
- [ ] Document what triggers saves vs. shares vs. follows

**Creator Insights:**
- [ ] Find actual creator workflow descriptions
- [ ] Identify repeatable patterns (formula) vs. creative decisions
- [ ] Document time/effort distribution in carousel creation

**Offer Integration:**
- [ ] Find examples of carousels that successfully weave offers
- [ ] Identify anti-patterns (what makes carousels feel salesy/fail)
</verification_checklist>

<research_quality_assurance>
Before completing research, perform these checks:

<completeness_check>
- [ ] All five research areas covered with substantive findings
- [ ] At least 3 concrete carousel "formulas" documented
- [ ] Visual design rules specific enough to implement
- [ ] Psychology patterns connected to product implications
</completeness_check>

<source_verification>
- [ ] Primary claims backed by multiple sources
- [ ] Distinguish expert opinion from data-backed findings
- [ ] Include actual carousel examples where possible
- [ ] URLs provided for verification
</source_verification>

<blind_spots_review>
Ask yourself: "What might I have missed?"
- [ ] Did I look at failing carousels to understand what NOT to do?
- [ ] Did I consider different niches (coaches vs. agencies vs. creators)?
- [ ] Did I verify claims about "what works" with actual data?
</blind_spots_review>

<actionability_check>
- [ ] Can each finding translate into a product feature or decision?
- [ ] Are recommendations specific enough to implement?
- [ ] Is the text/image separation hypothesis addressed?
</actionability_check>
</research_quality_assurance>

<output_structure>
Save to: `.prompts/002-carousel-virality-research/carousel-virality-research.md`

**CRITICAL: Write findings incrementally as you discover them.**

1. Create the file with initial skeleton
2. Append each finding as discovered (don't wait until end)
3. This ensures no lost work if token limits hit

Structure findings using this XML format:

```xml
<research>
  <summary>
    {2-3 paragraph executive summary: What makes carousels genuinely addictive and high-converting? What's the formula that no one has cracked in a tool yet?}
  </summary>

  <findings>
    <finding category="structure">
      <title>{Finding title}</title>
      <detail>{Detailed explanation with examples}</detail>
      <source>{Where this came from}</source>
      <product_implication>{How this affects what CarouselForge should do}</product_implication>
    </finding>

    <finding category="visual">
      <!-- Visual design findings -->
    </finding>

    <finding category="psychology">
      <!-- Psychology/engagement findings -->
    </finding>

    <finding category="text-image">
      <!-- Text-image interplay findings -->
    </finding>

    <finding category="workflow">
      <!-- Creator workflow findings -->
    </finding>
  </findings>

  <carousel_formulas>
    <formula name="{formula-name}">
      <description>{What it is}</description>
      <slide_by_slide>
        <slide number="1">{Purpose and content}</slide>
        <slide number="2">{Purpose and content}</slide>
        <!-- Continue for all slides -->
      </slide_by_slide>
      <when_to_use>{Situations this works best}</when_to_use>
      <evidence>{Where this was validated}</evidence>
    </formula>
    <!-- Document 3-5 formulas -->
  </carousel_formulas>

  <visual_rules>
    <rule name="{rule-name}">
      <guideline>{Specific, implementable guidance}</guideline>
      <rationale>{Why this works}</rationale>
      <examples>{Concrete examples}</examples>
    </rule>
    <!-- Document key visual rules -->
  </visual_rules>

  <text_image_separation_analysis>
    <viability>{Analysis of the hypothesis: separate text and image generation}</viability>
    <benefits>{What this approach enables}</benefits>
    <risks>{What could go wrong}</risks>
    <implementation_approach>{If viable, how to do it}</implementation_approach>
  </text_image_separation_analysis>

  <recommendations>
    <recommendation priority="critical">
      <action>{What CarouselForge MUST do}</action>
      <rationale>{Why}</rationale>
    </recommendation>

    <recommendation priority="high">
      <action>{What would significantly improve output quality}</action>
      <rationale>{Why}</rationale>
    </recommendation>

    <recommendation priority="medium">
      <action>{Nice to have}</action>
      <rationale>{Why}</rationale>
    </recommendation>
  </recommendations>

  <metadata>
    <confidence level="{high|medium|low}">
      {Why this confidence level}
    </confidence>
    <dependencies>
      {What's needed to act on this research}
    </dependencies>
    <open_questions>
      {What couldn't be determined}
    </open_questions>
    <assumptions>
      {What was assumed}
    </assumptions>

    <quality_report>
      <sources_consulted>
        {List URLs consulted}
      </sources_consulted>
      <claims_verified>
        {Key findings backed by data or multiple sources}
      </claims_verified>
      <claims_assumed>
        {Findings based on inference or single sources}
      </claims_assumed>
      <confidence_by_finding>
        - Carousel structures: {level} - {reason}
        - Visual rules: {level} - {reason}
        - Psychology patterns: {level} - {reason}
        - Text-image separation: {level} - {reason}
      </confidence_by_finding>
    </quality_report>
  </metadata>
</research>
```
</output_structure>

<summary_requirements>
Create `.prompts/002-carousel-virality-research/SUMMARY.md`

Format:
```markdown
# Carousel Virality Research Summary

**{Substantive one-liner: e.g., "5 structural formulas + visual rules that make carousels convert, not just engage"}**

## Key Findings
- {Most actionable insight for product}
- {Second key insight}
- {Third key insight}

## Carousel Formulas Discovered
- {Formula 1 name}: {one-line description}
- {Formula 2 name}: {one-line description}
- {etc.}

## Text-Image Separation Verdict
{Is the hypothesis viable? Brief answer with key consideration}

## Decisions Needed
{What needs user input before planning}

## Blockers
{None or specific issues}

## Next Step
Create carousel-implementation-plan.md

---
*Confidence: {level}*
*Full output: carousel-virality-research.md*
```
</summary_requirements>

<success_criteria>
- [ ] At least 5 distinct carousel structure formulas documented with slide-by-slide breakdown
- [ ] Visual design rules specific enough to become AI generation instructions
- [ ] Psychology insights connected to specific product features
- [ ] Text-image separation hypothesis analyzed with clear verdict
- [ ] Recommendations prioritized by impact on output quality
- [ ] All findings connected to "what CarouselForge should do differently"
- [ ] SUMMARY.md created with substantive one-liner
- [ ] Ready for planning prompt to consume
</success_criteria>

<extended_thinking>
This research requires deep analysis of:
- Why existing carousel tools produce "meh" output
- What the gap is between AI-generated and human-crafted carousels
- How to encode human creative judgment into replicable patterns

Thoroughly explore multiple sources before synthesizing. Consider that the most valuable insight may be something no one else has articulated—the non-obvious pattern that makes certain carousels genuinely addictive.

The goal isn't just documentation—it's finding the insight that gives CarouselForge an actual moat.
</extended_thinking>
