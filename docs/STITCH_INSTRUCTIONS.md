# Google Stitch UI Generation Constitution & System Constraints
### Operating Standard: Preventing AI Slop at Generation Time via the `unslop` Architecture

This document establishes the mandatory design rules, systemic constraints, and prompt blueprints for **Google Stitch** (and companion generative UI engines). Its purpose is to eliminate telltale AI "vibecoded slop" (e.g., purple gradients, ambient neon glows, emoji nav items, hyperbolic copy, floating shiny blobs, uneven arbitrary padding) directly at generation time.

---

## 1. Google Stitch Design Constitution

When generating UI through Google Stitch, the engine must never fall back on generic AI tropes. All output must strictly implement the 9 passes of the `unslop` methodology:

```
Pass 1: Spacing & Grid      → Strict 4px scale, Gestalt grouping, density tiers
Pass 2: Color & Surfaces    → Single neutral ramp, 3 text roles, 1 accent, hairline borders
Pass 3: Iconography         → Line icons only, locked stroke & dimensions, zero emojis
Pass 4: Copy & Realism      → Contextual deltas, no hype adjectives, domain-accurate data
Pass 5: Typography          → Character-driven pairings, tabular numbers, sentence case
Pass 6: Layout & Alignment  → Desktop app proportions, aligned vertical axes, calm hero
Pass 7: Component Details   → Concentric nested radii (R_in = R_out - p), kbd keycaps
Pass 8: Product Visuals     → Product-truth previews & real materials, zero shiny orbs
Pass 9: Purposeful Motion   → Opacity & transform only, single cubic-bezier, no loops
```

---

### Pass 1: Spacing & Grid System

* **Strict 4px Rhythm:** Every margin, padding, gap, and dimension must be an integer multiple of 4px: `4px, 8px, 12px, 16px, 20px, 24px, 32px, 40px, 48px, 64px, 80px, 96px, 128px`.
* **Zero Arbitrary Offsets:** Absolutely no arbitrary or prime-number pixel values (e.g., `mt-[13px]`, `py-[11px]`, `h-[31px]`, `w-[27px]`).
* **Density Tiers:**
  * **Navigation rows:** Height `32px–36px`, row-to-row gap `2px–4px`.
  * **Compact sidebars & tool panels:** Internal padding `16px`.
  * **Cards & metric blocks:** Internal padding `20px` to `24px`.
  * **Page containers & outer shells:** Page margin/padding `24px` to `32px`.
* **Gestalt Proximity Rule:** Internal element spacing within a cluster must be strictly tighter than the bounding gap separating groups:
  * Gap between group header and its items: `8px`.
  * Gap between previous group item and next group header: `24px` (3:1 ratio).
  * Card title to primary figure: `8px`.
  * Primary figure to comparative change subtext: `4px`.

---

### Pass 2: Color & Surfaces

* **Ban AI Gradient Slop:** 
  * Never render violet-to-blue, purple-to-pink, or neon radial gradients across cards, backgrounds, or buttons.
  * No gradient text (`bg-clip-text text-transparent bg-gradient-to-r`).
  * No diffuse colored neon drop-shadows (e.g., `shadow-[0_0_25px_rgba(168,85,247,0.4)]`).
* **Surface Architecture:**
  * Build on **one neutral ramp** tinted slightly toward the product's world (Graphite, Warm, or Ink).
  * Dashboard/App rule: 95%+ of all surfaces (background, sidebars, cards, tables, headers) must remain neutral. Color belongs exclusively to the content and data.
  * Elevation is achieved through discrete surface steps and crisp hairline borders (`1px solid rgba(255,255,255,0.08)` on dark, `1px solid rgba(0,0,0,0.08)` on light)—never through heavy glassmorphic blurs or glowing drop shadows.
* **Three Text Roles Only:**
  1. `Primary Text`: High contrast (#ededed on dark / #171717 on light).
  2. `Secondary Text`: Supporting context (#a1a1a6 on dark / #525252 on light).
  3. `Muted Text / Meta`: Captions, timestamps, keycaps (#85858b on dark / #737373 on light). Minimum contrast ratio must meet 4.5:1.
* **Accent Discipline:**
  * Exactly **one primary accent** hue per screen, used sparingly on at most 1–2 key interactions (e.g., the primary submit action or active metric badge).
  * On dark themes, primary actions can use high-contrast ramp off-white with dark ink text (`#ededed` background, `#111` text) rather than a loud neon saturated button.

---

### Pass 3: Iconography

* **Strict Emoji Ban:**
  * Zero emojis anywhere in UI controls, navigation items, status pills, or metric cards (no `🚀`, `✨`, `🔥`, `🏠`, `💰`, `👋`, `⚠️`).
  * Never use sparkle emojis (`✨`) as indicators for AI or automation features.
* **Unified Line-Icon Set:**
  * Use a single icon library (Lucide or Material Symbols Outlined).
  * Locked optical sizing: `16px` or `18px` with consistent `1.5px` or `2.0px` stroke weight.
  * Identical column bounding boxes: Every navigation or list icon must sit in an identical width container (e.g., `w-5 h-5` flex center) so all text labels align to an exact vertical pixel line.
  * Color inheritance: Icons inherit `currentColor` directly from the active text role (`secondary` or `muted`). Icons must never sport independent multi-color fills.

---

### Pass 4: Microcopy & Data Realism

* **Tone & Vocabulary:**
  * Ban greeting headlines: No `Welcome back, Sarah! 👋`. The page header must state the concrete working context: `Analytics Overview`, `Cluster Health`, `Billing — October 2026`.
  * Ban exclamation marks: Zero `!` or `!!` anywhere in UI text.
  * Ban AI marketing buzzwords: Remove `supercharge`, `seamless`, `unlock`, `magic`, `revolutionize`, `game-changing`, `AI-powered`.
  * Remove trailing punctuation on titles, button labels, tabs, and table headers. Only complete multi-sentence paragraphs take periods.
  * Concise input placeholders: Use `Search records...` or `Search`, never `Search anything here...`.
* **Data Realism & Explicit Deltas:**
  * Metric deltas must always name their comparative baseline: `+12.4% vs last month` (never `+12%!!` or `Growing fast`).
  * Numbers must reflect realistic domain scale and precision: e.g., `$42,850.00`, `99.98% uptime`, `1,420 ms avg latency` (never `$123,456` or `10,000+ teams`).

---

### Pass 5 & 6: Typography, Structural Alignment & Layout

* **Typographic Hierarchy:**
  * Pair one clean grotesque/neo-grotesque interface font (Inter, Geist, IBM Plex Sans) with an optional monospace partner for figures (Geist Mono, JetBrains Mono, IBM Plex Mono).
  * Use weights 400 (regular) and 500 (medium). 600 is reserved for rare emphasis. Never use 700–900 black weights.
  * Sentence case everywhere: Convert all `UPPERCASE TRACKED HEADERS` to normal sentence case (`Navigation`, `Total balance`).
* **Numeric Axis Rule (`tabular-nums`):**
  * Apply `font-variant-numeric: tabular-nums` (`font-mono` or `tabular-nums` in CSS) to all numeric values, timers, currency totals, and table columns.
  * Column alignment: All icons align on one vertical axis; all text labels align left; all financial metrics and tabular values align strictly to the right.
* **Layout Geometry:**
  * Dashboards fill real viewport proportions: fixed sidebar (`240px–280px`), responsive content canvas capped at `1440px–1600px`.
  * Never collapse a desktop dashboard into a narrow centered mobile-like column.

---

### Pass 7, 8 & 9: Component Details, Visuals & Motion

* **Concentric Nested Border Radii:**
  * Any nested child must calculate its border radius mathematically:
    $$\text{Radius}_{\text{inner}} = \text{Radius}_{\text{outer}} - \text{Padding}_{\text{container}}$$
  * Example: A card with `16px` border-radius and `8px` internal padding contains nested chips with `8px` radius (`16 - 8 = 8`). Minimum radius is `4px`. Not every element is a pill (`rounded-full`).
* **Tactile Micro-Details:**
  * Keyboard shortcuts use `<kbd>` keycap markup with subtle borders and inset shadow (`px-1.5 py-0.5 text-xs font-mono rounded border border-white/10 bg-white/5`).
  * Single-accent data visualizations: A line/bar chart uses neutral grey tones for baseline benchmarks and reserves the single accent color strictly for the active tracked series.
* **Visuals & Real Materials:**
  * Ban 3D orbs, floating glass shields, iridescent bubbles, and stock robot illustrations.
  * Render real product materials in code: a stylized credit card with a microchip, high-resolution SVG sparklines with muted grids, or authentic domain diagrams.
* **Motion Guardrails:**
  * No continuous looping animations: Ban `animate-pulse`, `animate-bounce`, and shimmering marquee loops on static content.
  * Strictly restrict CSS transitions to `transform` and `opacity`. Never transition layout dimensions (`width`, `height`, `margin`, `padding`).
  * Single easing curve across all interactions:
    ```css
    transition: transform 180ms cubic-bezier(0.16, 1, 0.3, 1), 
                opacity 180ms cubic-bezier(0.16, 1, 0.3, 1);
    ```

---

## 2. Google Stitch 5-Part Direction Template

Before invoking Google Stitch to design any page or widget, populate this 5-part directive. This ensures Stitch adheres to a bespoke product world instead of generic templates.

```markdown
### GOOGLE STITCH DIRECTION DIRECTIVE
1. PRODUCT:
   [What the application does and the exact operational user, e.g.: "High-throughput telemetry monitor for distributed database reliability engineers."]

2. CHARACTER:
   [3 concrete physical or atmospheric adjectives; BANNED WORDS: "clean", "modern", "sleek", "premium", "futuristic"]
   [e.g.: "Instrumental, rigorous, nocturnal"]

3. WORLD:
   [Physical workspace or material metaphor that dictates neutral tints and textures]
   [e.g.: "Air traffic control radar consoles, dark anodized aluminum, matte oscilloscopes"]

4. COLOR MOMENTS:
   [The 1 or 2 exact UI elements allowed to carry high-visibility accent color]
   [e.g.: "1) The active cluster latency sparkline; 2) The critical anomaly threshold status dot"]

5. SIGNATURE DETAIL:
   [1 repeatable, tactile micro-component unique to this product]
   [e.g.: "Monospace tabular keycap pills for query latency: [24ms] with a 1px vertical hairline separator"]
```

---

## 3. Ready-to-Paste Google Stitch Prompt Templates

### Template A: Global System Constraint Block
*(Paste this into Google Stitch's Project Instructions / Style Settings window)*

```text
=== MANDATORY SYSTEM CONSTRAINTS: ZERO-SLOP UI SPECIFICATION ===
You are generating production-grade, meticulously crafted UI code. You must adhere to the following strict architectural constraints:

1. SPACING & GRID:
   - Use strict 4px grid increments: 4, 8, 12, 16, 20, 24, 32, 48px. Zero arbitrary offsets (no 11px, 13px, 17px).
   - Sidebar padding: 16px. Card padding: 20px-24px. Page margin: 24px-32px.
   - Proximity rule: Internal element spacing (4px-8px) must be 1/3 of outer section spacing (24px).

2. COLOR & SURFACES:
   - NO purple-to-blue or violet-to-pink gradients. NO gradient text. NO glowing colored drop shadows.
   - Use ONE neutral ramp (Graphite or Slate). Surface depth comes from discrete color steps and 1px hairlines (border border-white/8 or border-black/8), never fuzzy glassmorphism.
   - Exactly THREE text roles: Primary (high contrast), Secondary (context), Muted (meta/timestamps).
   - Exactly ONE primary accent color. Confine it to at most 1-2 key elements per screen (primary CTA or active metric).

3. ICONOGRAPHY:
   - ZERO emojis anywhere (no 🚀, ✨, 🔥, 🏠, 👋).
   - Use a single line icon set (Lucide). Stroke width locked to 1.5px. Fixed container width (e.g., w-5 h-5 flex center).
   - Icons inherit text role color (text-zinc-400); never give icons custom multicolor fills.

4. MICROCOPY & REALISM:
   - NO greeting headlines ("Welcome back, User! 👋"). State context: "System Metrics — Q3 2026".
   - NO exclamation marks (never "!!"). NO marketing hype words ("supercharge", "seamless", "unlock", "AI-powered").
   - Comparative deltas must have a baseline: "+14.2% vs last week" (not "+14%!!").
   - Realistic domain numbers only (e.g., "$84,120.50", "99.95%").

5. TYPOGRAPHY & NUMERICS:
   - Sentence case everywhere. NO uppercase tracked headers ("NAVIGATION" -> "Navigation").
   - All numbers, timers, currency values, and table cells MUST use tabular numbers (font-mono or font-variant-numeric: tabular-nums).
   - Left-align text labels; right-align numeric and currency data.

6. DETAILS & MOTION:
   - Concentric nested radii: R_inner = R_outer - Padding (never make every card a full rounded-full pill).
   - Keyboard shortcuts use <kbd> keycaps with subtle hairline borders.
   - Transitions restricted to transform and opacity only with ease-out cubic-bezier(0.16, 1, 0.3, 1). NO transition-all. NO looping pulse/bounce effects.
================================================================
```

---

### Template B: Custom Dark Theme Preset
*(Deep Navy `#0A192F` Base + `#39FF14` High-Contrast Indicator Accent)*

> [!IMPORTANT]
> A high-voltage accent like Neon Green (`#39FF14`) easily deteriorates into "cyberpunk slop" if splashed across buttons, headers, borders, and gradients. Under `unslop` rules, **95% of the screen remains dark, quiet, and matte**. The `#39FF14` hue is reserved exclusively as a signal indicator.

```text
=== GOOGLE STITCH THEME PRESET: DEEP NAVY / HIGH-CONTRAST SIGNAL ===
PALETTE CONFIGURATION:
- Canvas Background:         #0A192F (Deep Obsidian Navy)
- Sidebar / Lowest Surface:   #060F1E (Sub-surface Navy)
- Card / Panel Surface:       #112240 (Elevated Navy Slate)
- Raised Surface / Active:    #1B3056 (Interactive Highlight)
- Hairline Border:           rgba(204, 214, 246, 0.08) (1px solid crisp boundary)
- Primary Text:              #E6F1FF (Crisp High-Contrast White)
- Secondary Text:            #8892B0 (Slate Neutral)
- Muted Text / Meta:         #495670 (Deep Muted Slate - 4.5:1 min contrast)
- Signal Accent:             #39FF14 (Pure Indicator Green - reserved exclusively for moments)

STRICT ACCENT APPLICATION RULES FOR #39FF14:
1. Surfaces and cards MUST NOT use #39FF14 gradients, glow filters, or border glows.
2. The primary button is NOT neon green. Render the primary button in #E6F1FF fill with #0A192F ink text.
3. The #39FF14 accent is permitted ONLY in two micro-moments:
   - An 8px live heartbeat status pip: `<span class="h-2 w-2 rounded-full bg-[#39FF14] inline-block mr-2"></span>`
   - The active primary metric curve on the main latency telemetry chart (1.5px stroke, no diffuse glow).
4. All badges, pills, and keycaps remain in muted slate (#1B3056 background with #8892B0 text).
====================================================================
```

---

### Template C: Export-to-Code Verification Checklist
*(Use this checklist to inspect HTML / Tailwind code generated or exported from Google Stitch)*

```markdown
### STITCH CODE VERIFICATION CHECKLIST

- [ ] **1. Spacing Validation**
  - [ ] Are all padding, margin, and gap values multiples of 4px (`p-2, p-3, p-4, p-6, p-8`)?
  - [ ] Are arbitrary bracket classes like `mt-[13px]` or `py-[11px]` absent?
  - [ ] Is sidebar padding 16px (`p-4`) and card padding 20px–24px (`p-5` or `p-6`)?

- [ ] **2. Surface & Color Validation**
  - [ ] Are all purple/pink gradients removed from buttons and card backgrounds?
  - [ ] Is gradient text (`bg-clip-text`) absent?
  - [ ] Are colored box-shadows (`shadow-[0_0_..._#8b5cf6]`) absent?
  - [ ] Do cards use solid discrete backgrounds with 1px hairline borders (`border border-white/8`)?
  - [ ] Does the entire screen use at most 1 primary accent color?

- [ ] **3. Icon & Emoji Validation**
  - [ ] Are all emojis (🚀, ✨, 🔥, 🏠, 👋) eliminated from navigation and labels?
  - [ ] Are all icons from a single uniform line set with matching stroke (1.5px or 2px)?
  - [ ] Do icons sit inside fixed-width containers to maintain vertical column alignment?

- [ ] **4. Copy & Data Realism**
  - [ ] Are generic greetings ("Welcome back...") replaced with operational context?
  - [ ] Are exclamation marks (`!`) completely absent?
  - [ ] Do metric changes specify comparison baselines (`+12.4% vs last month`)?
  - [ ] Are fake numbers like `$123,456` replaced with plausible domain data?

- [ ] **5. Typography & Numeric Alignment**
  - [ ] Are uppercase tracked headers replaced with clean sentence case?
  - [ ] Do all financial figures, table metrics, and timestamps carry `font-mono` or `tabular-nums`?
  - [ ] Are metric columns right-aligned and text labels left-aligned?

- [ ] **6. Details & Nested Radii**
  - [ ] Does child border radius satisfy `R_inner = R_outer - padding`?
  - [ ] Do shortcut indicators use semantic `<kbd>` keycaps instead of glowing rounded pills?
  - [ ] Do charts feature a single colored series with neutral baseline comparisons?

- [ ] **7. Motion & Transitions**
  - [ ] Is `transition-all` completely eliminated?
  - [ ] Are transitions restricted to `opacity` and `transform`?
  - [ ] Are infinite looping animations (`animate-pulse`, `animate-bounce`) removed?
```
