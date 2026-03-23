# Ansikt Homepage — Design Spec

## Overview

An editorial magazine-style homepage for Ansikt, a beauty studio specialising in brow and facial treatments. The page is the first of a multi-page site (home, about, treatments, bookings) and functions as the brand's flagship digital presence — drawing visitors in and funnelling them toward booking.

**Format:** Single `home.html` file with embedded CSS and vanilla JS. No build tools or dependencies.

**Style:** High-fashion editorial, not traditional beauty/wellness. Magazine spreads, bold colour blocking, full-bleed photography, scroll-triggered animation. Inspired by Lauren's existing website direction.

**Reference:** Brand identity system (`index.html`), Lauren's website screenshots (split-screen layouts, olive green sections, magazine numbering, editorial portraits).

## Brand Tokens (from identity system)

### Colours
```
--color-plaster: #D4C4B0
--color-linen: #F5F0E8
--color-blush: #DBBFB3
--color-charcoal: #2C2420
--color-terracotta: #B5704F
--color-olive: #B8D964
```

### Fonts
```
--font-display: 'Recoleta', Georgia, serif
--font-body: 'Plus Jakarta Sans', sans-serif
--font-mono: 'Courier Prime', 'Courier New', monospace
```

### Expanded for homepage
- Plus Jakarta Sans 300 (light) for large editorial intro text
- Courier Prime 400 italic for attributions, locations, details
- Opacity variants: ink-1 at 60% for secondary editorial text, olive at 15% for large background numbers

## Page Sections

### 1. Navigation (sticky)
- Fixed top, transparent on load, gains background on scroll (white with subtle border)
- Left: "ansikt" in display font
- Centre: nav links — Home, About, Treatments, Book (Plus Jakarta Sans 500, 14px, spaced)
- Right: "Book Now" CTA button in olive with charcoal text
- Mobile: collapses to hamburger
- Smooth transition between transparent and solid states on scroll
- Z-index above all content

### 2. Hero (100vh)
- **Layout:** Split-screen 50/50
- **Left panel:** Olive (#B8D964) background
  - Large editorial number "0.01" in Courier Prime 700, 120px+, at 12% opacity as background element
  - "ansikt" in display font, 48-56px
  - "beauty" in Plus Jakarta Sans 300, spaced lowercase, 16px, letter-spacing 0.2em
  - Tagline in Plus Jakarta Sans 300, 20px: "Bespoke brow and facial treatments in a calm, considered space"
  - "Explore treatments" CTA button — charcoal bg with olive text
  - Location line in Courier Prime italic: "Putney, London · by appointment"
- **Right panel:** Full-bleed editorial beauty portrait (generated)
  - Image covers entire right half
  - Subtle parallax on scroll (translateY at 0.3x scroll speed)
- **Animation:** Left content fades up with stagger (title first, then tagline, then CTA). Right image scales from 1.05 to 1.0 on load.
- **Mobile:** Stacks vertically — image on top (60vh), olive content panel below

### 3. Philosophy (short brand statement)
- **Layout:** Centred text, max-width 640px, generous vertical padding (120px+)
- **Background:** Linen (page default)
- **Content:**
  - Small label: "ABOUT ANSIKT" in Courier Prime, uppercase, letter-spaced
  - Main statement in Recoleta, 32-36px, colour charcoal: placeholder philosophy text about natural beauty, Norwegian heritage, considered space
  - Followed by a single body paragraph in Plus Jakarta Sans 300 light, 18px, ink-2
- **Animation:** Text fades up on scroll entry, line by line with slight stagger

### 4. Signature Treatments (curated 4)
- **Layout:** Alternating split-screen sections, each full-width
- Uses the editorial magazine pattern from the brand system
- 4 treatments selected as highlights:

**Treatment 1: Ansikt Luxury Facial**
- Left: Olive background with "0.01" watermark, treatment name in Recoleta, short description, price in Courier Prime, "Book" CTA
- Right: Full-bleed editorial portrait
- Content fades in from left on scroll

**Treatment 2: Brow Lamination**
- Left: Full-bleed image
- Right: Charcoal background with "0.02" watermark, light text
- Content fades in from right on scroll

**Treatment 3: Dermaplaning Reform**
- Left: Blush (#DBBFB3) background with "0.03" watermark, charcoal text
- Right: Full-bleed image
- Content fades in from left on scroll

**Treatment 4: Glass Skin (teen facial)**
- Left: Full-bleed image
- Right: Olive background with "0.04" watermark
- Content fades in from right on scroll

Treatment data (from treatments.md):
- Ansikt Luxury Facial: 50 mins | £50 (with Alpha H)
- Brow Lamination: 50 mins | £42
- Dermaplaning Reform: 50 mins | £50 (with LED light)
- Glass Skin: 25 mins | £30 (teen facial)

Each treatment block:
- Min-height: 500px (not full viewport — let them stack with rhythm)
- Image side: `object-fit: cover`, subtle scale on hover (1.0 → 1.03 over 0.6s)
- Content side: padding 48-64px, vertically centred
- "Book" button and "Learn more →" link
- Price/duration in Courier Prime
- Mobile: stacks vertically, image on top

### 5. Editorial Gallery
- **Layout:** Asymmetric grid (CSS grid with varying row/column spans)
- 4-5 images in a masonry-like layout
- **Hover state:** Image scales slightly (1.03), dark overlay fades in with treatment category name in Linen/Recoleta
- **Animation:** Staggered fade-up on scroll — each image enters 100ms after the previous
- One cell is a solid olive block with a pull quote in Recoleta instead of an image
- Mobile: 2-column grid, equal sizing

### 6. Testimonial
- **Layout:** Full-width, blush background
- Large quote in Recoleta, 28-36px, charcoal text, centred
- Attribution in Courier Prime italic
- Generous padding (100px+ vertical)
- **Animation:** Quote fades up, then attribution fades in 300ms later
- Optional: subtle parallax on the background (slight gradient shift)

### 7. Call to Action
- **Layout:** Full-bleed image background with dark gradient overlay
- Image: salon interior or beauty shot
- Content centred over image:
  - "Ready to book?" in Recoleta, 40px, linen text
  - Short line in Plus Jakarta Sans 300, plaster text
  - Large "Book Now" button — olive bg, charcoal text, hover scales up slightly
- **Animation:** Content fades up on scroll entry

### 8. Footer
- **Background:** Charcoal
- **Layout:** Three columns on desktop, stacked on mobile
  - Left: "ansikt" in display font (linen), "beauty" in Plus Jakarta Sans 300 spaced
  - Centre: nav links in Plus Jakarta Sans 400, plaster colour
  - Right: Instagram icon + @ansikt.uk in Courier Prime, contact details
- Bottom bar: copyright in Courier Prime 12px, ink-3 colour
- Olive accent line at the very top of footer (4px)

## Animation System

### Scroll Triggers
- Vanilla JS IntersectionObserver — no libraries
- Elements start with `opacity: 0` and `transform: translateY(24px)`
- On intersect: transition to `opacity: 1` and `translateY(0)` over 0.6s ease-out
- Stagger: child elements delay by 100-150ms each
- `threshold: 0.15` — trigger when 15% visible

### CSS Classes
```css
.reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease-out, transform 0.6s ease-out; }
.reveal.visible { opacity: 1; transform: translateY(0); }
.reveal-left { opacity: 0; transform: translateX(-24px); /* same transition */ }
.reveal-right { opacity: 0; transform: translateX(24px); }
.stagger-1 { transition-delay: 0.1s; }
.stagger-2 { transition-delay: 0.2s; }
.stagger-3 { transition-delay: 0.3s; }
.stagger-4 { transition-delay: 0.4s; }
```

### Interaction States
- **Buttons:** Scale 1.02 on hover, background colour transition 0.2s, shadow lift
- **Links:** Underline grows from left on hover (pseudo-element animation)
- **Gallery images:** Scale 1.03 in container with overflow hidden, overlay fades in
- **Treatment cards:** Image side scales subtly on hover
- **Nav links:** Colour transition + underline animation
- **All transitions:** `prefers-reduced-motion` query disables transforms, keeps opacity

### Parallax (hero image only)
- CSS `transform: translateY(calc(var(--scroll) * 0.3))` driven by scroll event
- Applied only to hero image
- Disabled for `prefers-reduced-motion`

## Responsive Breakpoints

| Breakpoint | Behaviour |
|---|---|
| > 1200px | Full editorial layouts, split-screens 50/50 |
| 768–1200px | Split-screens become 45/55, padding reduces |
| < 768px | All splits stack vertically, hamburger nav, image-first then content, gallery becomes 2-col |
| < 480px | Single column, further padding reduction, hero image 50vh |

## Image Generation

Generate via Gemini (work key), resize to max 1200px, convert to JPEG 80%:

1. **Hero portrait** — editorial beauty, 3:4 aspect, warm tones, side-lit, direct gaze
2. **Facial treatment** — close-up of treatment in progress, warm lighting (reuse existing if suitable)
3. **Brow close-up** — natural groomed brows, macro detail (reuse existing if suitable)
4. **Dermaplaning** — skin treatment detail, warm clinical-but-editorial
5. **Teen/glass skin** — young fresh skin, K-beauty feel, bright
6. **Gallery images** — 2-3 additional editorial shots for the asymmetric grid
7. **CTA background** — salon interior, wide angle, warm (reuse existing if suitable)

Reuse images from `assets/imagery/` where they fit. Generate only what's needed.

## File Structure
```
ansikt/
├── home.html              # The homepage
├── assets/
│   ├── imagery/           # Existing + new generated images
│   │   ├── home/          # Homepage-specific images
│   │   └── ...            # Existing brand images
├── index.html             # Brand identity system (unchanged)
└── ...
```

## Out of Scope
- Other pages (about, treatments, bookings)
- Actual booking functionality
- CMS integration
- Backend / server
- Real contact form
