# Ansikt Brand Identity System — Design Spec

## Overview

A single-page HTML brand identity document for **Ansikt**, a beauty studio specialising in brow and facial treatments. The document codifies the brand's visual language as a modular design token system with CSS custom properties, ready to be consumed by a future web product.

**Format:** Single HTML file with embedded CSS, fixed sidebar navigation, mobile-responsive (hamburger menu on small screens).

**Reference structure:** [Copia Design System](https://copiadigital.github.io/copia-brand/) sidebar navigation pattern (not the visual style).

## Brand Context

- **Business:** Brow and facial treatment studio based in the UK
- **Instagram:** @ansikt.uk
- **Aesthetic:** Earth tones, bare plaster interiors, exposed wood, warm neutrals. Beauty brand meets raw interior design.
- **Existing materials:** Two Heyzine flipbooks (brows, facials), printed typewriter-style price list menu, 3D backlit signage, gift cards
- **Logo:** Bold display serif with decorative swash on "a" and angular cuts. SVG to be sourced later — used as image asset.

## Deliverable Structure

The HTML document contains these sections, each navigable via the sidebar:

### 1. Introduction
- Brand name, tagline, brief philosophy
- Logo display (PNG for now, SVG placeholder)
- Logo usage rules (clear space, minimum size, what not to do)

### 2. Colour — Brand Palette
Five core brand colours derived from the salon interior and existing materials:

| Token Name | Hex | Role |
|---|---|---|
| Plaster | `#D4C4B0` | Primary warm neutral, borders, rules |
| Linen | `#F5F0E8` | Page background |
| Blush | `#DBBFB3` | Accent surfaces, callout cards |
| Charcoal | `#2C2420` | Primary text, dark surfaces |
| Terracotta | `#B5704F` | Active accent, links, CTAs, focus states |

### 3. Colour — Semantic Tokens
CSS custom properties mapping brand colours to functional roles:

```css
--color-bg: #F5F0E8;          /* Linen */
--color-surface: #FFFFFF;      /* cards, panels */
--color-surface-warm: #F5F0E8; /* tinted panels */
--color-surface-accent: #DBBFB3; /* Blush callout cards */
--color-border: #D4C4B0;      /* Plaster borders */
--color-border-subtle: #E8E0D6;
--color-ink-1: #2C2420;        /* Charcoal — headings */
--color-ink-2: #5C524A;        /* body copy */
--color-ink-3: #8C8078;        /* muted, labels */
--color-accent: #B5704F;       /* Terracotta — links, buttons */
--color-accent-hover: #9A5D3F;
```

### 4. Colour — Semantic States
Warm, muted functional colours:

| State | Text | Tint | Usage |
|---|---|---|---|
| Success | `#5C8A52` | `#E8F0E4` | Confirmations, positive feedback |
| Warning | `#C4903A` | `#FDF3E0` | Alerts, caution states |
| Error | `#B84C4C` | `#FAEAEA` | Errors, destructive actions |
| Info | `#5A7FA0` | `#E6EEF5` | Informational, neutral prompts |

### 5. Colour — Accessibility Matrix
A contrast ratio table showing every text-on-background combination with AA/AAA pass/fail badges. All pairings used in the system must meet WCAG 2.1 AA (4.5:1 for normal text, 3:1 for large text).

### 6. Typography — Font Stack
Three fonts with distinct roles:

| Font | Role | Weights | Source |
|---|---|---|---|
| **Recoleta** | Display/editorial: headings, hero text, pull quotes, service names | 400, 500, 600, 700 | Commercial (Latinotype) |
| **Plus Jakarta Sans** | Body/UI: paragraphs, buttons, navigation, forms, captions | 300, 400, 500, 600, 700 | Google Fonts (free) |
| **Courier Prime** | Data/typewriter: prices, durations, tables, treatment menus, code | 400, 700, 400 italic | Google Fonts (free) |

### 7. Typography — Type Scale
Responsive type scale with defined sizes, weights, line-heights, and letter-spacing:

| Level | Font | Weight | Size | Line-height | Letter-spacing |
|---|---|---|---|---|---|
| Hero display | Recoleta | 700 | 48-56px | 1.1 | -0.02em |
| Page heading H1 | Recoleta | 600 | 36-40px | 1.15 | -0.02em |
| Section heading H2 | Recoleta | 600 | 28-32px | 1.2 | -0.01em |
| Subheading H3 | Plus Jakarta Sans | 600 | 20-24px | 1.3 | 0 |
| Lead / deck | Plus Jakarta Sans | 400 | 18px | 1.5 | 0 |
| Body copy | Plus Jakarta Sans | 400 | 16px | 1.6 | 0 |
| Caption / label | Plus Jakarta Sans | 500 | 14px | 1.4 | 0.02em |
| Data / price | Courier Prime | 400 | 14-16px | 1.4 | 0 |

**System minimum:** 14px. No text in the system may be set below this size.

### 8. Typography — Usage Rules
Do/don't guidance for each font. Key rules:
- Recoleta is for display only — never for body paragraphs
- Plus Jakarta Sans is for everything functional — never for hero headings
- Courier Prime is for data and typewriter-style content only
- Maximum 2 fonts on one surface (card, section, panel)
- Uppercase labels must use letter-spacing ≥0.02em

### 9. Combinations — Font + Colour Pairings
Approved combinations shown as live examples:
- Charcoal text on Linen background (primary reading)
- Linen text on Charcoal background (inverted hero/header)
- Terracotta accent text on Linen (links, CTAs)
- Charcoal text on Blush background (callout cards)
- Courier Prime on warm surfaces (treatment menus)
- Each pairing shown with its contrast ratio

### 10. Components — Treatment Card
A reference card component showing all three fonts working together:
- Recoleta heading, price in Courier Prime, body in Plus Jakarta Sans
- Pre/post treatment notes in Courier Prime on warm surface
- CTA buttons in Plus Jakarta Sans

### 11. Components — Treatment Menu
The price list layout echoing the printed typewriter menu:
- Treatment names in Plus Jakarta Sans
- Prices/durations in Courier Prime
- Section headings in Recoleta

### 12. Components — Buttons
Primary, secondary, outline, and disabled states:
- Font: Plus Jakarta Sans 600
- Border-radius: 8px
- Sizes: small (32px), medium (40px), large (48px)
- States: default, hover, active, focus, disabled

### 13. Components — Callout / Quote Card
Testimonial and info card on Blush background:
- Quote in Recoleta
- Attribution in Courier Prime italic

### 14. Components — Navigation
Header nav pattern with Recoleta logo, Plus Jakarta Sans links, accent CTA button.

### 15. Table Styles
Data table styling for treatment comparisons, pricing tables, etc:
- Header: Plus Jakarta Sans 600, uppercase, letter-spaced
- Body: Plus Jakarta Sans 400
- Data cells: Courier Prime for numbers/prices
- Alternating row tint using --color-surface-warm
- Border using --color-border-subtle
- Responsive: horizontal scroll on mobile

### 16. Imagery — Photography Guidelines
Guidance on photography style derived from existing flipbook imagery:
- Warm, natural lighting
- Earthy/neutral colour grading
- Close-up beauty portraits with natural skin texture (dewy, not airbrushed)
- Salon interior shots: bare plaster, exposed wood, dried flowers
- Muted, warm colour temperature
- Example images generated via Gemini for illustration

### 17. Imagery — Treatment Examples
AI-generated example imagery showing approved photographic style for each treatment category (brows, facials, lashes).

### 18. Accessibility — AA Compliance Guide
Practical guidance for maintaining WCAG 2.1 AA compliance:
- Contrast ratio requirements (4.5:1 normal text, 3:1 large text, 3:1 UI components)
- Minimum font size (14px)
- Focus states (Terracotta outline, 2px offset)
- Touch target sizes (minimum 44x44px)
- Colour not used as sole indicator
- Alt text requirements for imagery
- Full audit table of all colour pairings with pass/fail

## Technical Implementation

### Architecture
- Single `index.html` file with embedded `<style>` block
- All CSS custom properties defined in `:root`
- Google Fonts loaded via `<link>` (Plus Jakarta Sans, Courier Prime)
- Recoleta loaded via `@font-face` from local files (or fallback to Georgia)
- Logo as inline SVG or `<img>` referencing PNG
- No JavaScript dependencies except for sidebar toggle on mobile
- Minimal JS: sidebar hamburger toggle, smooth scroll, active section highlighting

### Sidebar Navigation
- Fixed left sidebar (240px width) on desktop
- Collapsible hamburger menu on mobile (breakpoint: 768px)
- Sections grouped under category headings (Colour, Typography, Combinations, Components, Imagery, Accessibility)
- Active section highlighted on scroll via IntersectionObserver
- Smooth scroll to section on click

### Mobile Responsiveness
- Sidebar collapses to top hamburger menu below 768px
- Content goes full-width on mobile
- Type scale reduces proportionally (hero 36px, H1 28px, etc.)
- Tables get horizontal scroll wrapper
- Treatment cards stack vertically
- Touch targets minimum 44x44px

### Image Generation
- Example imagery generated using the `gemini-image` tool (work API key)
- Images stored in `./gemini_outputs/` then moved to project assets
- Prompts focused on: warm natural beauty photography, bare plaster interiors, earthy tones
- 2-3 images per category (salon interior, brow treatments, facial treatments, lash treatments)
- Images used for photography guidelines section and treatment examples

### Font Sourcing
- Recoleta is a commercial font (Latinotype). If font files are not available, use Georgia as the fallback for initial implementation. The system should be built so swapping in Recoleta via `@font-face` later is trivial.
- Plus Jakarta Sans and Courier Prime are loaded from Google Fonts.

### File Structure
```
ansikt/
├── index.html              # The brand identity system document
├── assets/
│   ├── logo.png            # Current logo
│   ├── logo.svg            # Future SVG (placeholder)
│   └── imagery/            # Generated example images
├── treatments.md           # Treatment details (already created)
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-03-23-ansikt-brand-identity-system-design.md
```

## Out of Scope
- Dark mode tokens (can be added later as a second theme)
- Component JavaScript behaviour (interactive states, animations)
- Actual booking functionality
- CMS or backend integration
- Print stylesheet
