# Ansikt Brand Identity System — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-page HTML brand identity system document for Ansikt with sidebar navigation, CSS design tokens, component examples, generated imagery, and AA accessibility compliance.

**Architecture:** Single `index.html` with embedded CSS custom properties in `:root`, Google Fonts loaded via `<link>`, minimal vanilla JS for sidebar toggle and scroll-spy. No build tools or dependencies. Mobile-responsive with hamburger nav below 768px.

**Tech Stack:** HTML5, CSS3 (custom properties), vanilla JS, Google Fonts (Plus Jakarta Sans, Courier Prime), Gemini image generation for example imagery.

**Spec:** `docs/superpowers/specs/2026-03-23-ansikt-brand-identity-system-design.md`

**Key reference files:**
- `treatments.md` — all treatment details, prices, descriptions
- `assets/logo.png` — current logo (user-provided)
- Brainstorm mockups in `.superpowers/brainstorm/` — approved colour palette, typography system, three-font examples

---

## Task 1: Scaffold — HTML shell, CSS tokens, sidebar, mobile nav

**Files:**
- Create: `index.html`
- Create: `assets/` directory

This task builds the entire page skeleton that all subsequent tasks fill with content. The sidebar navigation links to section IDs that will be created in later tasks.

- [ ] **Step 1: Create directory structure**

```bash
mkdir -p /Users/matt/projects/ansikt/assets/imagery
```

Copy the user-provided logo PNG into assets/:
```bash
cp /Users/matt/projects/ansikt/logo.png /Users/matt/projects/ansikt/assets/logo.png 2>/dev/null || echo "Logo not yet available — will use text fallback"
```

- [ ] **Step 2: Write `index.html` with full CSS tokens, sidebar, and responsive shell**

Create `index.html` with:

**`<head>`:**
- Meta charset, viewport (width=device-width, initial-scale=1.0)
- Title: "Ansikt — Brand Identity System"
- Google Fonts `<link>` for Plus Jakarta Sans (300-700) and Courier Prime (400, 700, 400i)
- Embedded `<style>` block containing ALL of the following

**CSS — Design Tokens (`:root`):**
```css
:root {
  /* Brand palette */
  --color-plaster: #D4C4B0;
  --color-linen: #F5F0E8;
  --color-blush: #DBBFB3;
  --color-charcoal: #2C2420;
  --color-terracotta: #B5704F;

  /* Semantic tokens */
  --color-bg: #F5F0E8;
  --color-surface: #FFFFFF;
  --color-surface-warm: #F5F0E8;
  --color-surface-accent: #DBBFB3;
  --color-border: #D4C4B0;
  --color-border-subtle: #E8E0D6;
  --color-ink-1: #2C2420;
  --color-ink-2: #5C524A;
  --color-ink-3: #8C8078;
  --color-accent: #B5704F;
  --color-accent-hover: #9A5D3F;

  /* Semantic states */
  --color-success: #5C8A52;
  --color-success-tint: #E8F0E4;
  --color-warning: #C4903A;
  --color-warning-tint: #FDF3E0;
  --color-error: #B84C4C;
  --color-error-tint: #FAEAEA;
  --color-info: #5A7FA0;
  --color-info-tint: #E6EEF5;

  /* Font stacks */
  /* Recoleta: commercial font — swap in via @font-face when files are available.
     Until then, Georgia serves as the fallback. */
  --font-display: 'Recoleta', Georgia, serif;
  --font-body: 'Plus Jakarta Sans', sans-serif;
  --font-mono: 'Courier Prime', 'Courier New', monospace;

  /* Spacing scale */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;
  --space-3xl: 64px;

  /* Sidebar */
  --sidebar-width: 260px;

  /* Radii */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
}
```

**CSS — Reset & base styles:**
- Box-sizing border-box on all elements
- `body`: background `var(--color-bg)`, font-family `var(--font-body)`, font-size 16px, line-height 1.6, color `var(--color-ink-2)`, margin 0
- All headings (`h1, h2, h3`): font-family `var(--font-display)`, color `var(--color-ink-1)`
- Links: color `var(--color-accent)`, hover color `var(--color-accent-hover)`
- `::selection`: background `var(--color-blush)`, color `var(--color-charcoal)`

**CSS — Sidebar (desktop):**
- `.sidebar`: fixed, left 0, top 0, width `var(--sidebar-width)`, height 100vh, background `var(--color-surface)`, border-right 1px solid `var(--color-border-subtle)`, overflow-y auto, padding 32px 24px, z-index 100
- `.sidebar-logo`: font-family `var(--font-display)`, font-size 24px, color `var(--color-ink-1)`, margin-bottom 8px
- `.sidebar-version`: font-family `var(--font-mono)`, font-size 12px, color `var(--color-ink-3)`, margin-bottom 32px
- `.sidebar-group`: margin-bottom 24px
- `.sidebar-group-title`: font-family `var(--font-body)`, font-size 11px, font-weight 600, text-transform uppercase, letter-spacing 0.08em, color `var(--color-ink-3)`, margin-bottom 12px
- `.sidebar-link`: display block, font-family `var(--font-body)`, font-size 14px, color `var(--color-ink-2)`, text-decoration none, padding 6px 0, transition color 0.15s
- `.sidebar-link:hover`: color `var(--color-accent)`
- `.sidebar-link.active`: color `var(--color-accent)`, font-weight 500

**CSS — Hamburger (mobile):**
- `.hamburger`: display none (hidden on desktop)
- Below 768px: `.sidebar` transforms off-screen (translateX -100%), `.sidebar.open` transforms to 0, `.hamburger` displays as fixed button top-left (44x44px min touch target), overlay behind sidebar when open
- `.hamburger-btn`: 44x44px, background `var(--color-surface)`, border 1px solid `var(--color-border-subtle)`, border-radius `var(--radius-md)`, cursor pointer, z-index 101, position fixed, top 16px, left 16px

**CSS — Main content:**
- `.main`: margin-left `var(--sidebar-width)`, padding 48px 64px, max-width 860px (content area)
- Below 768px: `.main` margin-left 0, padding 24px 20px, padding-top 72px (below hamburger)
- `.section`: margin-bottom 64px
- `.section-label`: font-family `var(--font-mono)`, font-size 12px, color `var(--color-ink-3)`, letter-spacing 0.06em, text-transform uppercase, margin-bottom 8px
- `.section-title`: font-size 32px, font-weight 600, margin-bottom 8px (uses `var(--font-display)` via heading inheritance)
- `.section-desc`: font-size 16px, color `var(--color-ink-2)`, margin-bottom 32px, max-width 600px
- `hr.divider`: border none, border-top 1px solid `var(--color-border)`, margin 64px 0

**HTML — Sidebar structure:**
```html
<nav class="sidebar" id="sidebar">
  <div class="sidebar-logo">ansikt</div>
  <div class="sidebar-version">Brand Identity v1.0</div>

  <div class="sidebar-group">
    <div class="sidebar-group-title">Introduction</div>
    <a href="#brand" class="sidebar-link">Brand</a>
    <a href="#logo" class="sidebar-link">Logo</a>
  </div>
  <div class="sidebar-group">
    <div class="sidebar-group-title">Colour</div>
    <a href="#brand-palette" class="sidebar-link">Brand palette</a>
    <a href="#semantic-tokens" class="sidebar-link">Semantic tokens</a>
    <a href="#semantic-states" class="sidebar-link">Semantic states</a>
    <a href="#accessibility-matrix" class="sidebar-link">Accessibility matrix</a>
  </div>
  <div class="sidebar-group">
    <div class="sidebar-group-title">Typography</div>
    <a href="#font-stack" class="sidebar-link">Font stack</a>
    <a href="#type-scale" class="sidebar-link">Type scale</a>
    <a href="#usage-rules" class="sidebar-link">Usage rules</a>
  </div>
  <div class="sidebar-group">
    <div class="sidebar-group-title">Combinations</div>
    <a href="#colour-font-pairings" class="sidebar-link">Colour + font pairings</a>
  </div>
  <div class="sidebar-group">
    <div class="sidebar-group-title">Components</div>
    <a href="#treatment-card" class="sidebar-link">Treatment card</a>
    <a href="#treatment-menu" class="sidebar-link">Treatment menu</a>
    <a href="#buttons" class="sidebar-link">Buttons</a>
    <a href="#callout" class="sidebar-link">Callout / quote</a>
    <a href="#navigation" class="sidebar-link">Navigation</a>
    <a href="#tables" class="sidebar-link">Tables</a>
  </div>
  <div class="sidebar-group">
    <div class="sidebar-group-title">Imagery</div>
    <a href="#photography" class="sidebar-link">Photography guidelines</a>
    <a href="#treatment-imagery" class="sidebar-link">Treatment examples</a>
  </div>
  <div class="sidebar-group">
    <div class="sidebar-group-title">Accessibility</div>
    <a href="#aa-guide" class="sidebar-link">AA compliance guide</a>
  </div>
</nav>
```

**HTML — Hamburger button:**
```html
<button class="hamburger-btn" id="hamburger" aria-label="Toggle navigation">
  <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
    <path d="M3 5h14M3 10h14M3 15h14" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
  </svg>
</button>
```

**HTML — Main content area:**
```html
<main class="main" id="main-content">
  <!-- Sections will be added in subsequent tasks -->
  <!-- Each section uses: -->
  <!-- <section class="section" id="section-id"> -->
  <!--   <div class="section-label">CATEGORY · 01</div> -->
  <!--   <h2 class="section-title">Section Title</h2> -->
  <!--   <p class="section-desc">Description</p> -->
  <!--   ... content ... -->
  <!-- </section> -->
</main>
```

**JavaScript (at end of `<body>`):**
```javascript
// Hamburger toggle
const hamburger = document.getElementById('hamburger');
const sidebar = document.getElementById('sidebar');
hamburger.addEventListener('click', () => {
  sidebar.classList.toggle('open');
});
// Close sidebar on link click (mobile)
sidebar.querySelectorAll('.sidebar-link').forEach(link => {
  link.addEventListener('click', () => {
    if (window.innerWidth < 768) sidebar.classList.remove('open');
  });
});

// Scroll spy — highlight active sidebar link
const sections = document.querySelectorAll('.section');
const navLinks = document.querySelectorAll('.sidebar-link');
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      navLinks.forEach(link => link.classList.remove('active'));
      const active = document.querySelector(`.sidebar-link[href="#${entry.target.id}"]`);
      if (active) active.classList.add('active');
    }
  });
}, { rootMargin: '-20% 0px -70% 0px' });
sections.forEach(section => observer.observe(section));

// Smooth scroll
document.querySelectorAll('.sidebar-link').forEach(link => {
  link.addEventListener('click', (e) => {
    e.preventDefault();
    const target = document.querySelector(link.getAttribute('href'));
    if (target) target.scrollIntoView({ behavior: 'smooth', block: 'start' });
  });
});
```

- [ ] **Step 3: Verify scaffold renders correctly**

Open `index.html` in browser. Verify:
- Sidebar is visible on the left with all navigation groups
- Main content area is offset by sidebar width
- Resize to <768px — sidebar should hide, hamburger button should appear
- Click hamburger — sidebar should slide in
- Click a nav link on mobile — sidebar should close
- All CSS custom properties are defined (inspect `:root` in dev tools)

- [ ] **Step 4: Commit scaffold**

```bash
cd /Users/matt/projects/ansikt
git init
git add index.html assets/ treatments.md docs/
git commit -m "feat: scaffold brand identity system with CSS tokens, sidebar nav, and mobile responsive shell"
```

---

## Task 2: Introduction & Logo section

**Files:**
- Modify: `index.html` (add content inside `<main>`)

- [ ] **Step 1: Add Introduction section**

Inside `<main>`, add the Brand section with:
- `id="brand"`
- Brand name "ansikt" in display font, large
- Tagline — something like "beauty" in spaced lowercase (matching flipbook covers)
- Brief philosophy paragraph: a few sentences about the brand's approach to brow and facial treatments, warm/considered space
- The word "ansikt" means "face" in Norwegian — note this

- [ ] **Step 2: Add Logo section**

Add section with `id="logo"`:
- Display the logo PNG (with fallback text if not available)
- Logo usage rules: minimum clear space (1x height of the "a" character on all sides), minimum display size (120px width for digital), always on light or dark backgrounds (never on busy imagery without overlay)
- "Don't" examples described textually: don't stretch, don't rotate, don't change colours, don't add effects, don't place on low-contrast backgrounds

- [ ] **Step 3: Verify in browser**

Check both sections render correctly on desktop and mobile.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add introduction and logo usage sections"
```

---

## Task 3: Colour sections — palette, tokens, states

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Brand Palette section**

Section `id="brand-palette"`:
- 5 colour swatches in a responsive grid (auto-fit, minmax 180px)
- Each swatch: colour block (100px height), name, hex code, role description, contrast ratio vs its primary pairing
- Colours: Plaster `#D4C4B0`, Linen `#F5F0E8`, Blush `#DBBFB3`, Charcoal `#2C2420`, Terracotta `#B5704F`

- [ ] **Step 2: Add Semantic Tokens section**

Section `id="semantic-tokens"`:
- Show the full CSS custom property map in a styled code block
- Use `var(--font-mono)` for the code, warm background surface
- Group tokens: backgrounds, borders, ink (text), accent

- [ ] **Step 3: Add Semantic States section**

Section `id="semantic-states"`:
- Four state cards in a grid: success, warning, error, info
- Each card uses its tint as background, text colour as left border and heading
- Show hex values for text and tint

- [ ] **Step 4: Verify in browser**

Check all three colour sections. Confirm swatches render, code block is readable, state cards show correct colours.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add colour palette, semantic tokens, and semantic states sections"
```

---

## Task 4: Colour — Accessibility Matrix

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Accessibility Matrix section**

Section `id="accessibility-matrix"`:
- A table showing every text-on-background combination used in the system
- Columns: Text colour, Background, Contrast Ratio, AA Normal (pass/fail badge), AA Large (pass/fail badge), AAA (pass/fail badge)
- Rows for all approved pairings:
  - ink-1 (#2C2420) on bg (#F5F0E8) — 11.5:1
  - ink-1 (#2C2420) on surface (#FFFFFF) — 14.7:1
  - ink-1 (#2C2420) on surface-accent (#DBBFB3) — 5.8:1
  - ink-2 (#5C524A) on bg (#F5F0E8) — 5.9:1
  - ink-2 (#5C524A) on surface (#FFFFFF) — 7.5:1
  - ink-3 (#8C8078) on bg (#F5F0E8) — 3.3:1 (large text only)
  - ink-3 (#8C8078) on surface (#FFFFFF) — 4.2:1 (large text only)
  - accent (#B5704F) on bg (#F5F0E8) — 4.5:1
  - accent (#B5704F) on surface (#FFFFFF) — 5.7:1
  - linen (#F5F0E8) on charcoal (#2C2420) — 11.5:1
  - linen (#F5F0E8) on accent (#B5704F) — 4.5:1
- Pass badges: green background. Fail: red. Large-only: amber.
- Note: calculate actual contrast ratios using the formula (L1 + 0.05) / (L2 + 0.05) to verify. If any pre-calculated ratio is wrong, correct it.
- Table should be horizontally scrollable on mobile (wrap in `overflow-x: auto` div)

- [ ] **Step 2: Verify matrix in browser**

Check table renders correctly, badges are visible, scroll works on mobile.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add colour accessibility contrast matrix with AA/AAA badges"
```

---

## Task 5: Typography sections — font stack, type scale, usage rules

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Font Stack section**

Section `id="font-stack"`:
- Three font cards in a responsive grid showing: font name rendered in its own face, CSS variable name, available weights, role description, do/don't one-liner
- Recoleta (fallback Georgia), Plus Jakarta Sans, Courier Prime

- [ ] **Step 2: Add Type Scale section**

Section `id="type-scale"`:
- A visual type scale showing each level rendered at its actual size
- Each row: left column with level name, font, weight, size, line-height specs (in `var(--font-mono)` small text), right column with the rendered example text using real Ansikt content
- Levels: Hero display, H1, H2, H3, Lead, Body, Caption, Data/Price
- Use treatment-related example text (from treatments.md) so it feels real

- [ ] **Step 3: Add Usage Rules section**

Section `id="usage-rules"`:
- Two-column grid: DO (green-tinted) and DON'T (red-tinted)
- Each rule as a bullet point
- Key rules from spec: Recoleta display only, Plus Jakarta Sans functional only, Courier Prime data only, max 2 fonts per surface, 14px minimum, uppercase needs letter-spacing

- [ ] **Step 4: Verify typography sections in browser**

Check fonts load from Google Fonts. Verify type scale renders at correct sizes. Check mobile layout stacks properly.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add font stack, type scale, and usage rules sections"
```

---

## Task 6: Combinations — Font + Colour Pairings

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Colour + Font Pairings section**

Section `id="colour-font-pairings"`:
- Live rendered examples of each approved combination:

**Pairing 1:** Charcoal on Linen — primary reading. Show a heading (Recoleta) and body paragraph (Plus Jakarta Sans) on linen background. Display contrast ratio.

**Pairing 2:** Linen on Charcoal — inverted/dark. Show a heading and subtitle on charcoal background (like the treatment card header from the three-font mockup). Display contrast ratio.

**Pairing 3:** Terracotta on Linen — accent text. Show a link, a button label, and a CTA on linen background. Display contrast ratio.

**Pairing 4:** Charcoal on Blush — callout. Show a testimonial quote (Recoleta) with attribution (Courier Prime) on blush background. Display contrast ratio.

**Pairing 5:** Courier Prime on warm surface. Show a treatment price list snippet on the warm surface colour. Display contrast ratio.

Each pairing: rendered example in a card, with the colour hexes and contrast ratio shown below in mono font.

- [ ] **Step 2: Verify in browser**

Check all 5 pairings render correctly with real fonts and colours.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add font and colour combination pairings with contrast ratios"
```

---

## Task 7: Components — Treatment Card, Menu, Buttons

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Treatment Card component**

Section `id="treatment-card"`:
- A fully rendered treatment card using the "Ansikt Luxury Facial" data from treatments.md
- Dark header: Recoleta title, Plus Jakarta Sans subtitle, Courier Prime price (top right)
- Body: Plus Jakarta Sans description paragraph
- Pre-treatment notes in Courier Prime on warm surface
- Two CTA buttons: primary "Book This Treatment", outline "View All Facials"
- Add CSS for `.treatment-card`, `.treatment-card-header`, `.treatment-card-body`, `.treatment-card-note` classes

- [ ] **Step 2: Add Treatment Menu component**

Section `id="treatment-menu"`:
- A price list styled like the flipbook treatment menu, using data from treatments.md
- Recoleta section heading "Facials"
- Each treatment: Plus Jakarta Sans name and subtitle on left, Courier Prime price/duration right-aligned
- Dividers between items using `var(--color-border-subtle)`
- Add CSS for `.menu`, `.menu-item`, `.menu-item-name`, `.menu-item-sub`, `.menu-item-price`
- Include all 5 facial treatments from treatments.md

- [ ] **Step 3: Add Buttons component**

Section `id="buttons"`:
- Show button variants: primary (filled terracotta), secondary (filled charcoal), outline (border only), disabled (muted)
- Three sizes: small (32px height, 13px text), medium (40px height, 14px text), large (48px height, 16px text)
- Show hover, active, focus states described (focus uses 2px terracotta outline with 2px offset)
- Add CSS for `.btn`, `.btn-primary`, `.btn-secondary`, `.btn-outline`, `.btn-sm`, `.btn-lg`, `.btn:disabled`
- All buttons: font-family `var(--font-body)`, font-weight 600, border-radius `var(--radius-md)`, min touch target 44x44px on mobile

- [ ] **Step 4: Verify components in browser**

Check treatment card, menu, and buttons all render correctly. Check mobile layout.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add treatment card, treatment menu, and button components"
```

---

## Task 8: Components — Callout, Navigation, Tables

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Callout / Quote component**

Section `id="callout"`:
- A testimonial card on blush background
- Quote text in Recoleta
- Attribution in Courier Prime italic
- Use a real testimonial from the flipbooks (e.g. Hollie, Putney)
- Also show an informational callout variant (e.g. a pre-treatment notice)
- Add CSS for `.callout`, `.callout-quote`, `.callout-attribution`, `.callout-info`

- [ ] **Step 2: Add Navigation component**

Section `id="navigation"`:
- A rendered example of the header navigation bar
- Recoleta logo text on left, Plus Jakarta Sans nav links in centre, terracotta CTA button on right
- Show active state on one link
- Add CSS for `.nav-bar`, `.nav-logo`, `.nav-links`, `.nav-cta`
- Note: this is a reference component, not the actual sidebar nav of this document

- [ ] **Step 3: Add Tables section**

Section `id="tables"`:
- A styled data table using a treatment comparison as example content
- Columns: Treatment, Duration, Price, Suitable for Pregnancy
- Header row: Plus Jakarta Sans 600, uppercase, letter-spaced, charcoal background with linen text
- Body rows: Plus Jakarta Sans 400, alternating white and warm-surface tint
- Price/duration cells: Courier Prime
- Border: `var(--color-border-subtle)`
- Wrap in `overflow-x: auto` div for mobile horizontal scroll
- Add CSS for `.data-table`, `.data-table th`, `.data-table td`, `.data-table tr:nth-child(even)`

- [ ] **Step 4: Verify in browser**

Check callout, navigation bar, and table render correctly. Check table scrolls horizontally on mobile.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add callout, navigation, and table style components"
```

---

## Task 9: Generate example imagery via Gemini

**Files:**
- Create: images in `assets/imagery/`

Generate 8-10 images using the gemini-image tool to illustrate the photography guidelines. Run each generation command from the project root directory.

- [ ] **Step 1: Generate salon interior images (2-3)**

```bash
cd /Users/matt/projects/ansikt
echo '{"prompt": "Professional photography of a beauty salon interior with bare plaster walls in warm pink-beige tone, exposed wooden beam ceiling, massage treatment bed with cream linen, dried flowers in ceramic vase, warm natural lighting, no people, editorial interior photography style, muted earth tones", "model_type": "pro", "resolution": "2K", "aspect_ratio": "16:9", "key": "work"}' | /Users/matt/scripts/.venv/bin/python /Users/matt/scripts/gemini_tool.py
```

Move output to assets:
```bash
mv gemini_outputs/*.png assets/imagery/salon-interior-1.png
```

Repeat with a variation prompt for 1-2 more interior shots (different angle, detail of decor/products).

- [ ] **Step 2: Generate beauty portrait images (2-3)**

Prompts focused on:
- Close-up beauty portrait, warm natural lighting, dewy skin, natural makeup, earthy warm tones, editorial beauty photography
- Variation: different angles (side profile, eye detail, full face)

```bash
echo '{"prompt": "Editorial beauty portrait close-up of a woman with natural dewy skin, warm natural lighting from the side, soft focus background in warm beige tones, no heavy makeup, natural skin texture visible, freckles, warm earth-toned colour grading, professional beauty photography", "model_type": "pro", "resolution": "2K", "aspect_ratio": "3:4", "key": "work"}' | /Users/matt/scripts/.venv/bin/python /Users/matt/scripts/gemini_tool.py
```

Move and rename outputs to `assets/imagery/`.

- [ ] **Step 3: Generate treatment-specific images (2-3)**

Prompts for:
- Facial treatment in progress: warm lighting, therapist's hands, calm setting
- Brow treatment close-up: natural brows, beauty detail
- Skincare products/textures: serums, creams, natural ingredients on warm surface

Move and rename outputs to `assets/imagery/`.

- [ ] **Step 4: Verify images**

Open each generated image and confirm they match the brand aesthetic (warm, earthy, natural, editorial). Regenerate any that feel off-brand.

- [ ] **Step 5: Commit**

```bash
git add assets/imagery/
git commit -m "feat: generate example brand imagery via Gemini for photography guidelines"
```

---

## Task 10: Imagery sections — Photography Guidelines & Treatment Examples

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Photography Guidelines section**

Section `id="photography"`:
- Introduction paragraph explaining the photographic style
- Grid of guideline cards covering:
  - **Lighting:** Warm, natural, side-lit. Avoid harsh flash or cool fluorescent.
  - **Colour grading:** Warm earth tones, slightly desaturated. Avoid high-saturation or cool/blue grading.
  - **Skin:** Natural texture, dewy, minimal retouching. No heavy airbrushing. Freckles and pores are welcome.
  - **Composition:** Close crops, eye-level or slightly above. Negative space in warm neutrals.
  - **Environment:** Bare plaster, natural materials, dried flowers, wood, ceramic. No clinical/sterile settings.
  - **Mood:** Calm, considered, intimate. Not high-energy or overly glossy.
- Include 2-3 of the generated salon/portrait images as reference examples
- Images displayed in a responsive grid with rounded corners and subtle border

- [ ] **Step 2: Add Treatment Examples section**

Section `id="treatment-imagery"`:
- Show 2-3 treatment-specific generated images
- Each with a caption describing the approved style for that treatment category
- Categories: Facials, Brows, Lashes, Environment/Product

- [ ] **Step 3: Verify in browser**

Check images load, grid is responsive, captions are readable.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add photography guidelines and treatment imagery sections"
```

---

## Task 11: Accessibility — AA Compliance Guide

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add AA Compliance Guide section**

Section `id="aa-guide"`:
- Introduction: "All design decisions in this system are made with WCAG 2.1 AA compliance. This section provides practical guidance for maintaining accessibility."
- Subsections as cards or styled blocks:

**Contrast Requirements:**
- Normal text (below 24px / 18.67px bold): minimum 4.5:1
- Large text (24px+ or 18.67px+ bold): minimum 3:1
- UI components and graphical objects: minimum 3:1
- Reference the accessibility matrix section above

**Typography:**
- System minimum: 14px — no text below this
- Body copy minimum: 16px recommended
- Line-height minimum: 1.4 for body text
- Paragraph max-width: ~70 characters for readability

**Interactive Elements:**
- Minimum touch target: 44x44px
- Focus states: 2px solid `var(--color-accent)` outline with 2px offset
- Focus must be visible on all interactive elements
- Never remove outline without providing alternative focus indicator

**Colour Usage:**
- Never use colour as the sole indicator of state or meaning
- Always pair colour with text, icon, or pattern
- Example: error states use red tint + red text + descriptive message

**Images:**
- All images must have descriptive alt text
- Decorative images use `alt=""`
- Complex images (charts, diagrams) need long descriptions

**Motion:**
- Respect `prefers-reduced-motion` media query
- No auto-playing animations
- Any motion should be subtle and purposeful

- [ ] **Step 2: Verify in browser**

Check all guidance sections render clearly with good hierarchy.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add WCAG AA accessibility compliance guide section"
```

---

## Task 12: Final polish — review, fix issues, verify mobile

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Full desktop review**

Open in browser at full width. Scroll through every section and verify:
- All sections are present and navigable via sidebar
- Scroll spy highlights correct sidebar link
- All fonts render correctly (Plus Jakarta Sans, Courier Prime, Georgia fallback for Recoleta)
- All colour tokens are applied correctly
- No layout breaks or overflow issues

- [ ] **Step 2: Mobile review**

Resize to 375px width. Verify:
- Sidebar is hidden, hamburger button is visible and 44x44px+
- Hamburger opens/closes sidebar
- All content is readable at mobile width
- Tables scroll horizontally
- Treatment cards stack vertically
- Touch targets are minimum 44x44px
- No horizontal overflow on the page body

- [ ] **Step 3: Fix any issues found**

Address any layout, typography, colour, or responsiveness issues.

- [ ] **Step 4: Final commit**

```bash
git add index.html
git commit -m "feat: final polish and mobile responsiveness fixes for brand identity system"
```

---

## Summary

| Task | Section | Est. Steps |
|---|---|---|
| 1 | Scaffold (HTML, CSS tokens, sidebar, mobile) | 4 |
| 2 | Introduction & Logo | 4 |
| 3 | Colour (palette, tokens, states) | 5 |
| 4 | Colour (accessibility matrix) | 3 |
| 5 | Typography (font stack, scale, rules) | 5 |
| 6 | Combinations (font + colour pairings) | 3 |
| 7 | Components (card, menu, buttons) | 5 |
| 8 | Components (callout, nav, tables) | 5 |
| 9 | Generate imagery via Gemini | 5 |
| 10 | Imagery sections | 4 |
| 11 | Accessibility guide | 3 |
| 12 | Final polish & mobile review | 4 |
