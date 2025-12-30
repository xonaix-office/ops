# XCORE CI BRAND STYLE GUIDE
## Version 1.0 | December 2025

---

## 1. BRAND OVERVIEW

### 1.1 Brand Architecture

```
COMPANY:     Xonaix, Inc.
MARK:        Xcore CI
MEANING:     Cognitive Intelligence
TAGLINE:     "Intelligence, evolved." (teaser)
             "Cognitive Intelligence." (hero)
```

### 1.2 Brand Hierarchy

| Level | Name | Pronunciation | Usage |
|-------|------|---------------|-------|
| Company | Xonaix | "ZON-ayks" | Corporate, legal, investor |
| Mark | Xcore CI | "X-core C-I" | Product, visual identity |
| Prefix | Xon | "ZON" | Product naming (Xon Core, etc.) |

### 1.3 Locked Taglines

| Tagline | Use Case |
|---------|----------|
| "Intelligence, evolved." | Teaser, pre-launch |
| "Cognitive Intelligence." | **Hero** — category definition |
| "AI that's governed, verified, and accountable." | Sub — explains hero |
| "Integrity at the core." | Values-focused, enterprise |
| "Intelligence, accountable." | Trust/compliance |
| "Core. Intelligence." | Minimal, punchy |
| "Where AI gets CI." | Playful, memorable |
| "CI for AI." | Short, memorable |

---

## 2. THE MARK

### 2.1 Primary Mark (v92 - LOCKED)

The Xcore CI mark consists of three elements:

```
┌─────────────────────────────────────────┐
│                                         │
│      X          CORE (rotated -45°)     │
│       \        /                        │
│        \      /                         │
│         \    /                          │
│          \  /                           │
│           \/                            │
│           /\                            │
│          /  \                           │
│         /    \  CI                      │
│        /      \                         │
│                                         │
└─────────────────────────────────────────┘
```

### 2.2 Mark Specifications

| Element | Property | Value |
|---------|----------|-------|
| **X** | Font size | 52px |
| | Font weight | 500 |
| | Font style | Italic |
| | Position | x=6, y=48 |
| **CORE** | Font size | 6px |
| | Font weight | 600 |
| | Letter spacing | 2px |
| | Transform | translate(34.5, 31.5) rotate(-45) |
| **CI** | Font size | 21px |
| | Font weight | 600 |
| | Letter spacing | 0.5px |
| | Position | x=40, y=48.00 |
| **ViewBox** | Dimensions | 0 0 95 60 |

### 2.3 Typography

Primary font stack (system fonts):
```css
font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', sans-serif;
```

Future consideration: Custom typeface for brand differentiation.

---

## 3. COLOR PALETTE

### 3.1 Primary Colors

| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| **Deep Void** | #050810 | 5, 8, 16 | Primary background |
| **Pure White** | #FFFFFF | 255, 255, 255 | Primary text on dark |
| **Electric Cyan** | #00FFF0 | 0, 255, 240 | Accent, highlight |
| **Electric Purple** | #BD00FF | 189, 0, 255 | Accent, secondary |

### 3.2 Secondary Colors

| Name | Hex | Usage |
|------|-----|-------|
| **Electric Blue** | #3B82F6 | Alternative accent |
| **Indigo** | #6366F1 | Alternative accent |
| **Soft Teal** | #4FD1C5 | Softer accent |
| **Cool Silver** | #A8B4C4 | Muted, secondary text |
| **Dark Cyan** | #00CFC5 | Cyan for light backgrounds |

### 3.3 Gradient

Primary gradient (diagonal, top-left to bottom-right):
```css
linear-gradient(135deg, #00FFF0 0%, #BD00FF 100%)
```

### 3.4 Color Usage Rules

| Context | Background | Mark Color |
|---------|------------|------------|
| Dark mode (primary) | #050810 | #FFFFFF or gradient |
| Light mode | #FFFFFF | #050810 or #00CFC5 |
| Hero/feature | #050810 | Gradient |
| Print/legal | White | #000000 |
| Favicon | #050810 | #FFFFFF, #00FFF0, or gradient |

---

## 4. MARK VARIANTS

### 4.1 Full Mark

| Variant | File | Usage |
|---------|------|-------|
| Primary (white on void) | xcore-ci-mark-v92.svg | Default, hero |
| Cyan | xcore-ci-mark-v92-cyan.svg | Accent contexts |
| Purple | xcore-ci-mark-v92-purple.svg | Alternative accent |
| Gradient | xcore-ci-mark-v92-gradient.svg | Hero, feature |
| Blue | xcore-ci-mark-v92-blue.svg | Alternative |
| Indigo | xcore-ci-mark-v92-indigo.svg | Alternative |
| Teal | xcore-ci-mark-v92-teal.svg | Softer contexts |
| Silver | xcore-ci-mark-v92-silver.svg | Muted contexts |
| Light (dark on white) | xcore-ci-mark-v92-light.svg | Light backgrounds |
| Light Cyan | xcore-ci-mark-v92-light-cyan.svg | Light + color |

### 4.2 Symbol Only (X)

| Variant | File | Usage |
|---------|------|-------|
| Dark background | xcore-ci-symbol-only-dark.svg | Small spaces |
| Transparent | xcore-ci-symbol-only-transparent.svg | Overlays |

### 4.3 Favicon

| Variant | File | Usage |
|---------|------|-------|
| Dark (white X) | xcore-ci-favicon-dark.svg | Default favicon |
| Cyan | xcore-ci-favicon-cyan.svg | Brand emphasis |
| Gradient | xcore-ci-favicon-gradient.svg | Premium contexts |

Favicon specifications:
- Container: 64x64 with 12px border radius
- X size: 44px, centered

### 4.4 Transparent Background

| Variant | File | Usage |
|---------|------|-------|
| White mark | xcore-ci-full-transparent-white.svg | Dark overlays |
| Dark mark | xcore-ci-full-transparent-dark.svg | Light overlays |
| Cyan mark | xcore-ci-full-transparent-cyan.svg | Flexible |

### 4.5 Lockup (Mark + Xonaix)

| Variant | File | Usage |
|---------|------|-------|
| Dark | xcore-ci-lockup-dark.svg | Corporate, investor |
| Gradient | xcore-ci-lockup-gradient.svg | Hero corporate |

Lockup specifications:
- ViewBox: 200x60
- Divider: 1px white line at 30% opacity
- Xonaix wordmark: 24px, weight 500, letter-spacing 1px

### 4.6 Monochrome

| Variant | File | Usage |
|---------|------|-------|
| Black | xcore-ci-mono-black.svg | Print, legal, fax |
| White | xcore-ci-mono-white.svg | Dark print contexts |

---

## 5. CLEAR SPACE & SIZING

### 5.1 Clear Space

Minimum clear space around the mark equals the height of "CI" (approximately 21px at standard size).

```
        ┌───────────────────────────────┐
        │         CLEAR SPACE           │
        │   ┌───────────────────────┐   │
        │   │                       │   │
        │   │      XCORE CI         │   │
        │   │        MARK           │   │
        │   │                       │   │
        │   └───────────────────────┘   │
        │         CLEAR SPACE           │
        └───────────────────────────────┘
```

### 5.2 Minimum Size

| Context | Minimum Width |
|---------|---------------|
| Full mark | 95px |
| Symbol only | 24px |
| Favicon | 16px |

Below these sizes, legibility is compromised.

---

## 6. INCORRECT USAGE

**Never:**

- ❌ Stretch or distort the mark
- ❌ Rotate the mark (CORE rotation is intentional and fixed)
- ❌ Change the typography or weights
- ❌ Rearrange elements
- ❌ Add effects (drop shadows, glows, bevels)
- ❌ Place on busy backgrounds without sufficient contrast
- ❌ Use unapproved colors
- ❌ Outline the mark
- ❌ Recreate the mark in different fonts
- ❌ Animate in ways that distort the mark

---

## 7. PRONUNCIATION GUIDE

| Term | Pronunciation | Phonetic | Notes |
|------|---------------|----------|-------|
| Xonaix | "ZON-ayks" | /ˈzɒn.eɪks/ | Company name |
| Xcore CI | "X-core C-I" | /ˈeks.kɔːr siː.aɪ/ | Say the letters |
| Xon | "ZON" | /zɒn/ | Product prefix |
| CI | "C-I" | /siː.aɪ/ | Always letters, never "see" or "ki" |

---

## 8. FILE FORMATS

### 8.1 Available Formats

| Format | Purpose | Scalable |
|--------|---------|----------|
| SVG | Digital, web, scalable | Yes |
| PNG | Raster, fixed sizes | No |
| PDF | Print, documents | Yes |
| ICO | Windows favicon | No |

### 8.2 Recommended PNG Sizes

For raster exports, generate at these sizes:
- 16px (favicon)
- 32px (favicon 2x)
- 64px (small UI)
- 128px (medium UI)
- 256px (large UI)
- 512px (app icons)
- 1024px (high-res)

---

## 9. ANIMATION GUIDELINES

### 9.1 Approved Animations

| Animation | Description | Duration |
|-----------|-------------|----------|
| **Color cycle** | Cyan ↔ Purple transition | 4-8 seconds |
| **Fade in** | Opacity 0 → 1 with scale 0.95 → 1.0 | 0.3-0.5 seconds |
| **Idle pulse** | Subtle glow on X center | 2-3 seconds |
| **Hover** | Single pulse or slight scale | 0.2 seconds |

### 9.2 Animation Principles

- Subtle, not distracting
- Matches teaser site DNA (alive, breathing)
- Never distorts the mark geometry
- Easing: ease-out or cubic-bezier for smooth motion

---

## 10. CO-BRANDING

### 10.1 Partner Placement

When appearing alongside partner logos:
- Maintain minimum clear space
- Equal or greater visual weight to partner
- Xcore CI on left or top in horizontal/vertical layouts
- Use lockup variant when company attribution needed

### 10.2 Endorsement

The mark should never imply endorsement without explicit agreement.

---

## 11. DOCUMENT HISTORY

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | December 2025 | Initial style guide |

---

## 12. CONTACT

For brand questions or asset requests:
- **Brand Owner:** Xonaix, Inc.
- **Email:** [TBD]
- **Web:** xonaix.com

---

*Document Classification: Internal - Brand Reference*
*© 2025 Xonaix, Inc. All rights reserved.*
