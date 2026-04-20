# The Peach System — Weekly Intelligence Report v2 Design Brief

**Surface:** Weekly intelligence report rendered in Softr via custom HTML/CSS/JS Custom Code block
**Source file:** `weekly-intelligence.html` (existing, to be redesigned in place)
**Status:** Design locked. Ready for Claude Code build.

---

## 1. The problem being solved

The Step 6 v2 and Step 7 v2 architecture now produces genuinely sophisticated intelligence — multi-window baselines, pattern observations across 90 days of creative history, forward preparation, sufficiency awareness, analyst-voice reasoning.

The current UI undersells this. Metric values are 26px. Cards are tinted pastel. Everything sits at similar visual weight. Pattern observations (the "wow" moments the engine now produces) have no dedicated visual treatment. The report reads as a friendly dashboard, not as premium intelligence worth paying for.

**The shift:** from flat-uniform-dashboard to editorial intelligence report. Scale, hierarchy, and compositional variety do the work. Nothing is hidden — everything is elevated.

---

## 2. Core design principles

### 2.1 Scale signals importance
The most important element on any screen is dramatically larger than everything else. Hero numbers at 96-120px. Section labels at 10px. Brief hooks at 48-64px. No middle-weight everything.

### 2.2 Compositional variety creates rhythm
Mix card types across the page: hero cards, stat clusters, dark accent cards, chart cards, editorial cards. Uniform grids flatten hierarchy. Mixed compositions create it naturally.

### 2.3 White is the canvas, not the wall
Generous negative space is compositional. Not "empty" — framed. Premium design shows confidence in what it doesn't show.

### 2.4 Coral means "pay attention here"
Reserve coral for genuine attention moments: hero numbers that beat baseline meaningfully, priority flags on observations, the "wow" accent on pattern observations, the brief hook as display type. Three or four moments per screen, not decoration.

### 2.5 Charts earn their place as evidence
Every chart substantiates a specific observation. No decorative donuts. No generic trend lines. A sparkline belongs next to a number; a retention curve belongs inside a video retention observation; a bar chart belongs inside a format pattern card.

### 2.6 Editorial atmosphere through abstract brand shapes
Subtle brand-navy or coral curves, gradients, or organic shapes behind hero moments. The gradients are **brand colour to transparent** (not brand colour to darker brand colour). Used sparingly — hero section, one or two pattern observations, forward preparation. Not decoration — atmosphere. Makes the report feel like a magazine spread rather than a data view.

### 2.7 Effects earn hierarchy
Glass, glow, subtle shadow — used 2-3 times per screen to signal tier, never as decoration. A frosted-glass pattern observation card signals "this is intelligence, not data." A glow under a hero number signals "this is the story." Elsewhere: flat, confident, considered.

### 2.8 One page, expansion in place
No tabs, no drill-down pages. Core scroll shows the weekly moment at a glance. Metric cards, pattern observations, and issues can expand in place to reveal depth (multi-window baselines, pattern reasoning, underlying data). Default state is scannable summary.

### 2.9 Dual-audience language — UI vs intelligence
Two different language registers at play:

**UI chrome** (section labels, button text, headers, empty states) stays warm and personal. "Your weekly report", "Your top performers", "Based on your tracked data." The subscriber owns the app experience; "your" is accurate and appropriate regardless of whether they're a founder running their own ads or an agency running a client's account.

**AI-generated intelligence** (headlines, observations, pattern framings, issue text) uses account-attributed language. Describes what the account's data shows, not what the subscriber did. Works for founders (it's about their business) and agencies (it's about their client's business) without sounding wrong to either.

Examples of account-attributed intelligence:
- "This account has consistently seen carousels outperform static" (not "your carousels")
- "Occasion-based hooks have been the strongest performers" (not "your occasion hooks")
- "Spend on this campaign has performed 40% above baseline — worth increasing" (not "you should increase spend")

This is a prompt-level discipline for Step 6 v2 and Step 7 v2. Worth auditing real output Tuesday and tweaking prompts if language leans too founder-specific.

---

## 3. Palette & typography

### 3.1 Palette — three colours only

The entire report uses:
- **Navy** `#37475D` — the brand navy. Used flat, no variants, no gradients to darker-or-lighter navies. Typography, dark accent cards, structural elements.
- **Coral** `#ff6b6b` — attention accent only (hero numbers when story, priority flags, pattern emphasis, brief hooks).
- **White** `#ffffff` — card surfaces, page canvas.

**That's it.** No navy deep, no navy mid, no pastels, no sage/peach/cream tints.

**All greys are transparent navy** at varying opacities:
- `rgba(55, 71, 93, 0.04)` — faintest surface tint (subtle section backgrounds)
- `rgba(55, 71, 93, 0.08)` — card borders
- `rgba(55, 71, 93, 0.12)` — dividers
- `rgba(55, 71, 93, 0.5)` — muted supporting text
- `rgba(55, 71, 93, 0.7)` — secondary text

**Banished from v2:**
- Pastel card tints (`#e3edf3` blue, `#e3ede6` sage, `#f7ebe7` peach, `#f2ebe0` warm)
- Secondary navies (`#2a3545` navy-deep, `#435569` navy-mid)
- Navy gradients (`linear-gradient(135deg, var(--navy), var(--navy-mid))` used in current story card, brief header, hook spot — all replaced with flat brand navy)
- Cream page background (`#eeeae4` — replaced by pure white or off-white)

**Atmosphere comes from scale, space, subtle shadow, and abstract shapes — not colour variation.**

### 3.2 Typography
- **Display** — DM Sans at 600-700 weight for hero numbers, headlines, brief hooks. Already loaded.
- **Body** — DM Sans at 400-500 weight for analysis prose, supporting text.
- **Monospace numbers** — use `font-variant-numeric: tabular-nums` on all number displays so columns align across rows.

Scale ladder:
- Hero number: 96-120px
- Weekly headline: 36-44px
- Pattern observation hero statement: 28-36px
- Metric card number: 48-64px (up from 26px)
- Brief hook: 48-64px (up from 17px)
- Body prose: 14-15px
- Section labels: 10-11px, uppercase, letter-spaced

---

## 4. Page structure — top to bottom

### 4.1 Header (preserve from current, minor refinement)
Keep the video header with light-leak overlay — it's genuinely cinematic and already in brand. Refinements only:
- Tighten the "Weekly Intelligence" eyebrow type (slightly smaller, more letter-spaced)
- Account name can go slightly larger (26px → 28-30px)
- Account selector and week selector styling stays
- Keep the "X weeks of your data" live-dot chip

### 4.2 Hero section — NEW
**Replaces:** the current navy story card with bullet points.

**What it is:** one hero moment per week, dynamically chosen based on what mattered most. The weekly_headline becomes the framing, one number becomes the anchor, one pattern observation becomes the supporting line.

**Visual treatment:**
- Full-width card, white background, generous vertical padding (80-100px)
- Abstract navy shape curving in from the right edge (subtle gradient, partially off-screen, like the Envato reference) — provides atmosphere without being data
- Eyebrow: "This week" at 10px uppercase, muted navy
- Weekly headline at 36-44px, navy, weighted (from `intel.weekly_headline`)
- Hero number at 96-120px — could be ROAS, Revenue, or change-percentage — picked by logic based on what drove the week's story. Coral if exceptional, navy if routine-positive, muted-navy if routine-neutral.
- Supporting stat line beneath the number (e.g., "vs 4-week baseline: +38%" at 16px)
- One pattern observation line underneath (from `intel.executive_summary[0]` or top `intel.issues` action), at 18-20px, italic-adjacent weight

**Fallback:** when `weekly_headline` is null and no strong story, render a quieter hero — account name and week as the headline, 4w ROAS as the number, no coral.

### 4.3 Metric row — REDESIGN
**Replaces:** the current 5 pastel-tinted cards in uniform grid.

**What it is:** mixed-composition row. Not 5 identical cards.

**Option A layout (recommended):**
- 1 "hero metric" card (the metric with the strongest story this week) — larger, spans 2 columns, white with subtle coral glow if value beats baseline meaningfully, sparkline background with coral current-point marker
- 4 smaller stat cards (the remaining metrics) — white, compact, number at 48px, sparkline beneath as background element

**Option B layout:**
- 5 cards, but two sizes alternating — odd-indexed cards slightly larger and taller than even-indexed, creating visual rhythm

**My recommendation: Option A.** Clearer hierarchy.

**Each card contains:**
- Metric name at 10-11px uppercase, muted
- The number at 48-64px (hero metric at 72-80px), tabular-nums, weighted
- One comparison line beneath ("38% above 4w baseline" — coral if positive & meaningful, muted navy if flat, navy if negative)
- Subtle sparkline rendered as card background element (gradient fade, opacity 0.4-0.6), with coral current-point marker if current is notable
- **Expansion on click:** the card grows in place to reveal multi-window data (4w/12w/lifetime/seasonal_yoy deltas as small stats), full trend chart, percentile marker, sufficiency note ("seasonal YoY unlocks in 8 weeks")

**No pastel backgrounds. All white cards. Hierarchy comes from scale, sparkline, and coral accent.**

### 4.4 Pattern observations — NEW SECTION
**Location:** directly beneath metric row. This is the "wow" section — the new-in-v2 intelligence.

**Data source:** `intel.pattern_observations` (from Step 6 v2 — new field).

**Visual treatment:**
- Section label at 10px, uppercase, letter-spaced: "Patterns we're tracking"
- 1-3 pattern observation cards, each given GENUINE space
- Each card is larger than a metric card — think 240-320px tall
- White card with navy-tinted subtle border, faint inner shadow, or a frosted-glass effect (`backdrop-filter: blur(20px)` on a semi-transparent white) — these cards should feel like a different LAYER of the page
- Abstract coral shape (gradient circle, partially off-screen) behind the most notable pattern observation for editorial atmosphere

**Each pattern observation card contains:**
- Eyebrow: pattern type ("Format performance" / "Hook style" / "Retention cliff") at 10px uppercase, muted navy
- Observation title as a hero statement at 28-36px — e.g., "Your carousels outperformed static 2.3x this quarter"
- Supporting detail at 14-15px, 2-4 sentences from the observation's `detail` field
- An integrated visualisation that substantiates the observation:
  - **Hook style pattern** → small bar chart showing ROAS by hook style category
  - **Format pattern** → two-bar comparison (carousel vs static, etc.)
  - **Video retention cliff** → line chart with the cliff marked in coral
  - **Visual theme pattern** → small grid of 3-4 thumbnails with coral border on winning theme
  - **Fatigue curve** → timeline graphic showing typical fatigue age
- Small "Because" disclosure at bottom: 2-3 data points supporting the observation ("Across 24 ads since Jan 15 · 12w baseline: 2.1x")
- **Expansion on click:** card grows to show full reasoning, complete supporting data, related observations

**When `pattern_observations` is empty** (early-account sufficiency): section renders a quieter placeholder — "Your pattern observations will appear as your account history builds. First patterns typically emerge at 10+ ads with 4+ weeks of spend."

### 4.5 Forward preparation — NEW SECTION
**Location:** after pattern observations.

**Data source:** `intel.forward_preparation` (new field from Step 6 v2).

**Visual treatment:**
- Small section, one card
- Eyebrow: "Coming into view" at 10px uppercase
- The forward preparation text at 20-24px, navy, weighted
- Subtle navy gradient background fading to white (atmosphere, not decoration)
- Small icon or abstract shape (horizon line graphic) to reinforce "looking ahead" metaphor
- Hidden entirely when `forward_preparation` is null

### 4.6 Performance analysis (issues) — REFINE
**Preserve from current:** the issues list structure. It works.

**Upgrades:**
- Issue cards slightly larger, more breathing room (padding: 24-28px vs current 18-20px)
- Severity pill stays, but Priority pill becomes more prominent — "Act now" in coral glow, "This week" in muted amber
- Issue type heading at 16-18px (up from 13px)
- Action detail at 15px (up from 13px), line-height 1.7
- Owner + metric footer stays compact
- **Expansion on click:** reveals full issue context (Step 6 v2's full reasoning, prior-weeks narrative, related baselines)

### 4.7 Creative analysis — REDESIGN
**Replaces:** the current thumbnails-with-overlays + plain-text analysis-wrap pattern.

**Visual treatment:**
- Section label: "Creative analysis"
- **Top row — hero creative treatment:** the #1 performer this week given editorial space
  - Thumbnail at 280-360px square, no overlay crowding
  - Beside it: hook text at 24-28px (if exists), ad name, ROAS at 48-56px coral, spend, key stat line
  - "Top performer" badge replaced with subtle coral accent bar
- **Second row — supporting creatives:** 3-4 smaller cards, uniform, thumbnails 160-200px, minimal overlay
- Beneath thumbnails: the Scale These / Consider Pausing / Watch Closely prose rendered in the analysis-wrap — but typography enhanced
  - Section headers (SCALE THESE etc.) at 11px uppercase coral (preserve current pattern)
  - Ad names at 16px navy weight (up from current) — preserve the ca-adname class but make bolder
  - Body prose at 15px, line-height 1.85

### 4.8 Creative pattern observations — NEW SECTION
**Location:** between creative analysis and briefs.

**Data source:** `intel.creative.creative_pattern_observations` (new field from Step 7 v2).

**Visual treatment:** mirrors the Step 6 pattern observations section (§4.4) but for creative patterns. Same card treatment, same expansion pattern, different observations.

Typically: hook style patterns, format performance, video retention cliff, visual theme patterns, fatigue curve awareness.

### 4.9 Creative briefs — REDESIGN
**Replaces:** the current navy brief card with 14px labels and 17px hook.

**The shift:** briefs become display-type artefacts. The hook is the hero. The interaction model stays — subscribers still click sidebar briefs to switch the active brief, and can "Generate Creative" or "Send to Designer" from the active brief.

**Active brief card (center — the hero brief):**
- Full-width card, navy background (this is one of the intentional dark moments)
- Coral accent bar along top edge
- Concept name at 14px uppercase, coral
- **Hook text at 48-64px display type**, white, weighted, generous line-height. This is the artefact.
- Beneath hook, two-column grid:
  - Left: ad copy (body), CTA (pill button style, coral)
  - Right: visual concept (muted card), why it works (analyst-voice framing, rendered in faint coral-tinted block)
- **Actions bar at bottom:**
  - **Generate Creative** — coral primary button, routes to `/creative-generator` (existing link, preserve href)
  - **Send to Designer** — ghost secondary button. Opens editable modal (see §4.9.1 below)

**Sidebar brief cards (briefs 2 and 3):**
- Navy cards (flat brand navy, not gradient), 220-280px wide
- Concept name at 12px uppercase coral
- Hook truncated to ~80 chars, 16-18px white
- "View brief" CTA pill at bottom
- **Click behaviour:** swaps the clicked brief into the active/hero position. Current active brief moves to the sidebar. Preserve the `switchBrief(idx)` function and `#briefData` JSON script pattern exactly — it works and keeps state client-side without a re-fetch.

**Switching animation:**
- Current v1 uses an instant swap. v2 should add a subtle transition — active card fades out (150ms), new content fades in (150ms), sidebar shuffles. Total under 400ms.

**When only 1 brief exists:** the sidebar renders the existing "1 brief this week — more briefs appear as more data builds up" placeholder. Preserve.

### 4.9.1 Send to Designer modal — NEW
**What it is:** the "Send to Designer" button opens a modal where the subscriber can edit the brief content before sending, add a personal note, and choose how to send (Copy text, WhatsApp, Email).

**Visual treatment:**
- Navy backdrop behind modal (60% opacity), subtle blur on page beneath
- White modal card, generous padding (40-60px), rounded corners (20-24px), max-width ~680px
- Modal title: "Send to Designer" at 24-28px navy
- Close × top-right

**Editable fields (all pre-filled with AI-generated brief content):**
- **Hook** — single-line editable input, monospace font, character counter "8/10 words" beneath (Meta best practice limit)
- **Ad copy** — multi-line textarea, character counter "118/125 characters" beneath (Meta limit awareness)
- **CTA** — single-line editable input
- **Visual concept** — multi-line textarea
- **Why it works** — multi-line textarea, hidden by default. Small toggle: "Include rationale for designer" (off by default). When on, this section appears in the output.

Each field:
- Label at 10-11px uppercase coral
- Editable value in white input, navy border (`rgba(55, 71, 93, 0.12)`), 15px navy text
- Character counter beneath — coral if over limit, muted navy otherwise (over-limit is shown but NOT blocked)

**Note field:**
- Label: "Add a note for your designer" (optional)
- Freeform textarea, ~4 rows
- Placeholder: `Anything else for your designer? E.g. "Need by Friday" · "Use our pink palette" · "Match our Eid campaign energy"`

**Send actions (bottom row of modal):**
- **Copy text** — copies formatted brief to clipboard, shows "Copied!" confirmation
- **WhatsApp** — opens `wa.me/?text=[encoded-brief]` in new tab
- **Email** — opens `mailto:?subject=Creative brief: [concept]&body=[encoded-brief]`

Each button has its relevant icon (clipboard, WhatsApp logo, envelope).

**Output format (what gets sent via any method):**

```
Creative brief: [Concept Name]

[Note from subscriber, if provided]

HOOK
[hook text — edited or original]

AD COPY
[ad copy — edited or original]

CTA
[CTA — edited or original]

VISUAL CONCEPT
[visual concept — edited or original]

WHY IT WORKS
[only included if "Include rationale" toggle is ON]

[Company Name] · via The Peach System
```

**localStorage draft persistence:**
- As user edits fields, save to `localStorage` under key `peach-brief-draft-[briefId]`
- If user closes modal without sending, edits persist
- If user reopens the modal, edits are restored
- On successful send, clear the localStorage entry

**Edit scope:**
- Edits are session-only for v1 — they don't save back to the Airtable brief record
- Reopening the modal after a full page refresh restores from localStorage (not from Airtable)
- This is intentional — subscribers can experiment with edits freely without worrying about overwriting the "official" AI-generated version

**What NOT in v1:**
- No branded shareable page
- No custom logo/colours (Peach-branded footer only)
- No shareable URL
- No persistence to Airtable
- No designer email memory / autocomplete
- No PDF export

These are reserved for the agency-tier project, planned as a focused build in 4-6 weeks once founder subscribers are validated.

### 4.10 Seasonal reminders — PRESERVE, minor refinement
Keep the current reminder grid structure. It works.

Refinements:
- Card treatment stays but shift from cream-white to pure white
- Navy typography slightly elevated in weight
- The "X weeks away" pill stays coral for urgency, navy for major seasons
- Preserve the seasonal banner rotation at top

---

## 5. Interaction patterns

### 5.1 Card expansion
Metric cards, pattern observation cards, and issue cards can expand in place. Click card → card grows vertically (animated, 300ms ease), revealing expanded content beneath the default summary. Click again or outside → collapses.

Expanded state is distinct:
- Background shifts slightly (pale coral tint for the expanded card)
- More content revealed — multi-window data, full reasoning, supporting stats
- Subtle close affordance (small × top-right)

### 5.2 Hero number count-up on load
When the page first renders, hero number counts up from 0 to target value over 800ms. Single polish moment on first view. Does not animate on re-render or navigation.

### 5.3 Sparkline draw-in
Sparklines animate left-to-right on first render (500ms). Static thereafter.

### 5.4 Pattern observation card reveal
Pattern observation cards animate in sequentially on first scroll-into-view (staggered 150ms apart). Not on every scroll — once per page load.

### 5.5 Coral glow on notable values
When a metric's change vs baseline is genuinely notable (>25% improvement or >15% decline), the value number has a subtle coral glow (text-shadow). Not every week. Not every metric.

### 5.6 Thumbnails — subtle performance glow
Creative thumbnails with ROAS above baseline have a faint coral border glow whose intensity maps to ROAS-over-baseline ratio. Scanning the creative row, you can feel which ads are winning.

---

## 6. Responsive behaviour

### 6.1 Breakpoints
Preserve current breakpoints (`760px`, `600px`). Mobile layout must remain usable.

### 6.2 Mobile adjustments
- Hero number scales down to 72-84px on mobile
- Metric row becomes 2-column on tablet, 1-column on mobile — hero metric spans full width on mobile
- Pattern observation cards stack vertically on mobile, full-width
- Brief hook scales to 32-40px on mobile
- Creative thumbnails: 3-col on desktop, 2-col on tablet, 1-col on mobile

### 6.3 Touch-friendly
All expandable cards have minimum 44px tap targets. Hover states fall back to active states on touch.

---

## 7. Data integration

### 7.1 New v2 fields expected in `intel` payload
- `intel.pattern_observations` (array from Step 6 v2) — `[{ title, detail, pattern_type }]`
- `intel.forward_preparation` (string or null, from Step 6 v2)
- `intel.creative.creative_pattern_observations` (array from Step 7 v2)
- `intel.creative.forward_preparation` (string or null, from Step 7 v2)

The existing `peach-intelligence-api` Worker returns these automatically once the Step 6 v2 and Step 7 v2 Workers have written them to Airtable. No frontend data-fetching changes needed.

### 7.2 Graceful degradation
- When `pattern_observations` is empty/undefined: section renders placeholder ("Patterns will appear as history builds")
- When `forward_preparation` is null: section not rendered at all
- When `creative_pattern_observations` is empty: section not rendered
- When `weekly_headline` is null: hero falls back to quieter state (account name + week, no coral)
- When any new field fails to load: existing v1 fields still render; new sections just skip

### 7.3 Multi-window baseline display
The current `mCard` function reads `weekly_spend_4w_median` etc. Extend to read 12w, lifetime, and seasonal_yoy medians when available (these come from D1 via `peach-dashboard-api` `/api/baselines` endpoint once D1 is queryable from there — may require API endpoint extension, flag in decisions log if so).

---

## 8. What to preserve from v1

- Overall file architecture (single HTML file, vanilla JS, fetches from existing Worker APIs)
- Auth flow (`window.logged_in_user.softr_user_email`)
- Admin platform access check
- Account selector + week selector dropdowns in header
- Account listing and access filtering logic
- Seasonal reminders grid + banner rotation
- Video header with light-leak overlay
- Brief switching interaction (active + sidebar pattern)
- `formatCreativeAnalysis` text parser
- Currency formatting (`fmtC`)
- ROAS percentile logic
- Fatigue alert banner
- History badge ("Benchmarked against X weeks")

## 9. What to remove from v1

- All pastel metric card tints (`--card-blue`, `--card-sage`, `--card-peach`, `--card-warm`)
- Current story card with glow gradients (replaced by new hero section)
- Current metric card layout (replaced)
- Current top video hook card (role absorbed into hero or pattern observations)
- Current fixed-structure creative analysis text dump (replaced by editorial creative section)
- Current brief card styling (replaced by display-type brief cards)

## 10. Acceptance criteria

### Visual
- Hero number displays at 96-120px on desktop
- No pastel card tints anywhere
- Coral used 3-5 times per screen maximum, each meaningful
- Generous white space between sections (minimum 48-64px margins)
- Abstract navy/coral shapes appear as atmosphere behind hero and 1-2 pattern observations
- Brief hooks display at 48-64px

### Functional
- All v1 data loading works
- New v2 fields render when present, degrade gracefully when absent
- Card expansion works smoothly for metrics, pattern observations, issues
- Mobile layout is usable down to 375px width
- Auth and account/week selection preserved

### Performance
- Initial paint under 1.5s on 4G
- Animations complete in under 1s
- No layout shift during data loading
- Spinner state shown during initial fetch

### Content integrity
- All existing v1 fields still render appropriately
- British English preserved
- No em dashes in framing text
- Currency formatting preserved (numbers only, no symbols for Gulf currencies)

---

## 11. Build sequencing (for Claude Code)

### Phase 1 — Foundation (chunks 1-3)
1. Update CSS variables and palette (remove pastel tints, add navy grey scale, confirm coral usage)
2. Refine header (minor typography updates)
3. Add typography utility classes (hero scale, display scale, tabular-nums)

### Phase 2 — Hero section (chunks 4-5)
4. Build new hero section with abstract shape, hero number, weekly headline integration
5. Add count-up animation and first-load polish

### Phase 3 — Metric row (chunks 6-7)
6. Redesign mCard function — new layout, scale, sparkline integration
7. Add click-to-expand multi-window reveal

### Phase 4 — Pattern observations (chunks 8-9)
8. Build new `patternObservationsSection` renderer from `intel.pattern_observations`
9. Add per-pattern-type visualisations (bar, line, thumbnail grid)

### Phase 5 — Forward preparation (chunk 10)
10. Build new `forwardPreparationSection` renderer from `intel.forward_preparation`

### Phase 6 — Creative redesign (chunks 11-13)
11. Redesign creative hero treatment (top performer editorial card)
12. Redesign supporting creatives row
13. Creative pattern observations section (mirror Step 6 patterns UI)

### Phase 7 — Briefs redesign (chunks 14-17)
14. Redesign active brief card (display-type hook, two-column layout)
15. Redesign sidebar brief cards
16. Build Send to Designer modal — editable fields, character counters, localStorage draft persistence
17. Wire Send to Designer actions — Copy text / WhatsApp / Email with formatted output

### Phase 8 — Issues and polish (chunks 18-20)
18. Refine issue cards (scale, padding, expansion)
19. Seasonal reminders minor refinement
20. Final polish pass — animations, coral glow intensity, mobile refinements

---

## 12. Key decisions locked (for reference)

1. Single HTML file, edited in place — no migration to Cloudflare Pages
2. **Three-colour palette: brand navy `#37475D`, brand coral `#ff6b6b`, white. Nothing else. All greys are transparent navy.**
3. One-page layout with in-place card expansion (no tabs, no drill-down)
4. Editorial direction with abstract atmospheric shapes (brand-colour-to-transparent gradients only)
5. Massive scale on hero numbers (96-120px) and brief hooks (48-64px)
6. Mixed card composition — hero cards, stats, dark accents, chart cards, editorial cards
7. Pattern observations get dedicated visual treatment as "wow" moments
8. Charts are evidence, not decoration — each chart substantiates a specific observation
9. Coral reserved for genuine attention moments (3-5 per screen)
10. Preserve data layer, auth, and core interactions from v1
11. Graceful degradation for v2 fields when data is absent
12. **Founder-first scope** — this build targets founders running their own Meta ads. No white-label, no branded shareable pages, no agency theming in this project.
13. **Dual-audience language discipline** — UI chrome stays warm and personal ("your"). AI-generated intelligence uses account-attributed language ("this account", "the data shows") so it works for founders AND agencies without sounding wrong to either.
14. **Send to Designer** is a focused modal — editable brief fields, optional note, three send methods (Copy/WhatsApp/Email), localStorage draft persistence, Peach-attributed footer. No branded pages, no custom colours, no logo overrides in v1.
15. **Agency tier reserved for a separate focused project** in 4-6 weeks once founder subscribers are validated and paying.

---

## 13. Inspiration references

Discussed during design session:
- **Envato dashboard template** (hero numbers at massive scale, abstract curves, editorial layout)
- **Apple Stocks widget** (row-based stat layout with inline sparklines)
- **Apple Screen Time widget** (chart-as-primary-content with supporting stats)
- **Stripe dashboard** (data density on clean canvas)
- **Linear app** (restrained colour, sharp typography)

These inform atmosphere and pattern — not literal copying. Direction is "Peach brand editorial intelligence report" not "mimic Envato" or "mimic Apple."

---

## 14. Open questions for Claude Code to flag

If any of these come up during build, flag in the decisions log rather than guess:

1. Whether API endpoint `/api/baselines` already returns 12w / lifetime / seasonal_yoy median fields, or if the endpoint needs extending (may require Worker-side change).
2. Whether `intel.pattern_observations` is pre-parsed JSON or needs `JSON.parse()` client-side.
3. Exact palette values for the gradient atmospheres (navy-to-transparent, coral-to-transparent) — propose and flag.
4. Whether to load a chart library (Recharts CDN? D3? inline SVG?) for pattern visualisations. Recommend inline SVG for minimal overhead.
5. Mobile hero number — if 72-84px breaks layout, flag and propose smaller.
