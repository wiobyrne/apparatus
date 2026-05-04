# DESIGN.md — wiobyrne.com

This file is the canonical design reference for the Astro site at wiobyrne.com.
Any AI agent generating pages, components, or styles for this site must read this first.

Token source of truth: `src/styles/tokens.css`
Global styles: `src/styles/global.css`
Site identifier: `data-site="wiobyrne"` on `<html>`

For the site-wide reading system and page posture rules, see `APPARATUS.md`.

---

## Design Philosophy

Editorial precision. Sparse. Warm.
This is a **thinking environment**, not a publication or magazine.
The design should disappear — readers notice the ideas, not the interface.

Influences: Gwern, Audrey Watters, Doug Belshaw (thoughtshrapnel.com).
Not influences: Medium, Substack, card-grid tech blogs.

---

## Color Tokens

All tokens defined in `src/styles/tokens.css`. Do not hardcode hex values.

### Light mode (default)
```
--bg-page:      #f9f9f7    /* warm lived-in white — base surface */
--bg-subtle:    #f2f4f2    /* elevated surface — code blocks, wells, understory */
--text-main:    #2d3432    /* charcoal ink — warm, not cold black */
--text-muted:   #5a605e    /* metadata, captions, secondary text */
--text-soft:    #6b716f    /* timestamps, tertiary labels */
--border-light: rgba(45, 52, 50, 0.15)   /* ghost border */
--border:       var(--border-light)       /* alias used by components */
--link:         #2d3432    /* links match text — black, editorial */
```

### Dark mode
```
--bg-page:      #1a1e1c
--bg-subtle:    #222826
--text-main:    #e6e4e1
--text-muted:   #8a908e
--border-light: rgba(230, 228, 225, 0.12)
--link:         #e6e4e1
```

Dark mode triggers on `prefers-color-scheme: dark` OR `data-theme="dark"` on `<html>`.
Manual toggle stored in `localStorage('theme')`.

### Green — Digitally Literate / garden connective tissue
```
--green-accent: #006d48    /* forest green — growth, literacy, ecosystem links */
--green-hover:  #00522f
```
Green is not the general wiobyrne.com accent color, but it may appear where the page is explicitly pointing into Digitally Literate, the newsletter, or the digital garden. Use it as connective tissue, not generic decoration.

### Site-level variables
Components reference these; overridden per-site via `data-site`:
```
--site-bg:          var(--bg-page)
--site-link:        var(--link)
--site-accent:      transparent          /* no global accent on wiobyrne.com */
--site-prose-width: var(--width-prose)   /* 660px */
--site-shell-width: var(--width-home)    /* 720px */
```

---

## Typography

### Font stack
```
--font-serif: "Source Serif 4", Georgia, serif
--font-sans:  "Inter", system-ui, sans-serif
--font-mono:  "JetBrains Mono", "Courier New", monospace
```

Loaded from Google Fonts in `global.css`.

### Core rule
> If it helps you **read**, it's serif.
> If it helps you **navigate**, it's sans.

**Body default: `--font-serif`**
Everything is serif unless explicitly overridden.

**UI override — these always use sans:**
```css
h1, h2, h3, h4, h5, h6, nav, .ui, .meta, .button, .section-label, .eyebrow, small
```

**Exception:** The homepage intro `<h1>` overrides back to serif with a local rule + comment,
because it is editorial content, not navigation.

### Type scale
```
--text-h1:   40px
--text-h2:   24px
--text-body: 18px
--text-ui:   14px
```

### Line heights
```
--leading-prose: 1.75    /* reading */
--leading-ui:    1.6     /* interface */
--leading-tight: 1.15    /* headings */
```

---

## Layout

```
--width-home:  720px     /* shell / nav max-width */
--width-prose: 660px     /* reading column */
--pad-mobile:  24px
--pad-desktop: 40px
```

```
--space-1: 8px
--space-2: 16px
--space-3: 32px
--space-4: 64px
```

**Single column, centered.** No sidebar. Ever.

---

## Shape & Effects

**Border radius: 0 everywhere.** No exceptions. No `border-radius` on buttons, cards, tags, inputs, or code blocks.

**No-Line Rule:** `hr` and `.section-divider` are `display: none`. Tonal background shifts and spacing carry the structure.

Current homepage exception:
- Very light `border-top: 1px solid var(--border)` is allowed on selected section transitions in long single-column flows
- This is a compositional aid, not decorative chrome
- Use sparingly; if spacing alone can carry the rhythm, prefer spacing

**Glass nav:**
```css
background: var(--glass-surface);          /* rgba(249, 249, 247, 0.72) */
backdrop-filter: blur(12px);
-webkit-backdrop-filter: blur(12px);
```
No border-bottom on the header. The glass effect replaces the line.

**Ambient shadow (used sparingly):**
```
--ambient-shadow: 0 0 40px rgba(45, 52, 50, 0.04)
```
0px offset. Never a drop shadow. Never on cards.

---

## Components

### Header
- `position: sticky; top: 0; z-index: 100`
- Height: `3.5rem`
- Background: `var(--glass-surface)` with `backdrop-filter: blur(12px)`
- No bottom border
- Nav links: `--font-sans`, `var(--text-ui)`, `--text-muted` default, `--text-main` on hover/active
- Active page: `font-weight: 600`

#### Wordmark (left) — locked 2026-04-22
- Treatment: **boxed all-caps mono** ("AD" style)
- Font: `--font-mono`, `0.75rem`, weight `700`, `letter-spacing: 0.12em`, `text-transform: uppercase`
- Frame: `border: 1px solid var(--border)`, `height: 1.9rem`, `padding: 0 0.7em` — matches gear trigger height exactly
- Hover: border darkens to `--text-muted`
- Rationale: JetBrains Mono is used throughout the site for tags, dates, section labels, code, and the footer — the wordmark as a structural label is coherent with that system

#### Command palette trigger (right) — locked 2026-04-22
- Element: gear mark SVG with dashed outer ring, inline in button
- Size: `17px × 17px` SVG inside `1.9rem × 1.9rem` button
- Color: `currentColor` — inherits `--text-muted` at rest, `--text-main` on hover
- Rationale: gear was Ian's favicon from ~2018 onward; dashed ring is distinctive; gear = process/friction/making, which is the philosophical counterpart to the garden metaphor on DL
- SVG source: `04 META/🔗 Assets/mark-light.svg` (light) and `mark-dark.svg` (dark)
- Do NOT replace with `/` or any other glyph — this is a deliberate identity decision

### Footer
- Border top: `1px solid var(--border)`, `margin-top: var(--space-4)`
- Name: `--font-serif` bold
- Links: `--font-sans` `0.8125rem` `--text-muted`
- Copyright: `--font-mono` `0.75rem`

### Buttons
- `border-radius: 0` — always
- Min height: `2.4rem`, padding `0.55rem 0.9rem`
- Default (`.btn`): `--bg-subtle` bg, `1px solid var(--border)`, `--text-main`
- Primary (`.btn-primary`): `--text-main` bg, `--bg-page` text (inverted)
- Green primary buttons are allowed only inside explicit Digitally Literate / garden bridge sections

### Writing list (homepage / archive)
- Text-only: title + date on one row, description below; no images, no arrows
- No border separators inside the list — spacing only
- Hover: `background: var(--bg-subtle)` on the list item (tonal shift)
- Title: `--font-sans`, `0.9375rem`, weight 600
- Date: `--font-mono`, `0.72rem`, right-aligned, low visual weight
- Description: `--font-sans`, `0.8125rem`, `--text-muted`

### Homepage composition
The homepage is a **newsletter growth engine with intellectual credibility as the conversion mechanism**.

Its jobs, in order:
1. convert strangers into newsletter subscribers
2. convert subscribers into clients or paid readers

Current homepage order and emphasis:
- **Intro** — compact trust-builder, hands off quickly
- **Newsletter** — primary conversion zone; visually featured as a fuller green-tinted bridge into Digitally Literate with the most breathing room
- **Recent writing** — archive proof; dense list + archive-scale note
- **Work with me** — downstream conversion; tighter and more utilitarian
- **The Understory** — quiet tertiary invitation

Rules:
- There is no standalone "What I do" section anymore
- Homepage hierarchy comes from **spacing and density shifts**, not new colors, fonts, or motifs
- The newsletter block is the only homepage section that should feel fully "featured"
- On wiobyrne.com, that featured state may use a full green-tinted band when the section is explicitly about Digitally Literate or the garden ecosystem
- Archive scale should be signaled explicitly
- Light section-top borders may be used sparingly on lower-priority transitions if they improve scanability in the single-column flow

### Post card (if used)
- Border: `1px solid var(--border)`, `border-radius: 0`
- Hover: `background: var(--bg-subtle)`, border darkens
- Animated arrow (→) on hover via CSS transform
- No featured image thumbnails

### Tag pill
- `--font-mono`, `0.7rem`, uppercase, `letter-spacing: 0.06em`
- `background: var(--bg-subtle)`, `border: 1px solid var(--border)`, `border-radius: 0`
- Hover: `--tag-hover-bg` (inverted: `--text-main` bg, `--bg-page` text)

### Section labels (eyebrow text)
- Class: `.section-label`
- `--font-mono`, `0.7rem`, uppercase, `letter-spacing: 0.12em`, `--text-muted`

### Understory block
- Class: `.understory-block`
- `background: var(--bg-subtle)`, no border-radius
- On wiobyrne.com: no left border (that's DL-only)

### Prose (article body)
- Font: `--font-serif` (inherits from body default)
- Line-height: `var(--leading-prose)` — 1.75
- Blockquote: `border-left: 3px solid var(--blockquote-border)`, italic, `--text-muted`
- Code inline: `--font-mono`, `0.875em`, `var(--bg-subtle)` background, `border-radius: 0`
- Code block: `border: 1px solid var(--border)`, `border-radius: 0`
- HR inside prose: `display: none` (No-Line rule)

### Links
- Color: `var(--site-link)` = `var(--link)` = `#2d3432` — matches body text
- `text-underline-offset: 3px`, `text-decoration-thickness: 1px`
- Underline color: `color-mix(in srgb, var(--site-link) 35%, transparent)` at rest
- Hover: thickness `2px`, full color
- Never green on wiobyrne.com

### Favicon — locked 2026-04-22
- File: `public/favicon.svg` (primary) + `public/favicon.ico` (fallback for old browsers)
- Both declared in `BaseLayout.astro`: SVG first, `.ico` as `sizes="any"` fallback
- Design: gear mark + dashed ring on `#f9f9f7` warm-white background square
- Source SVG: `04 META/🔗 Assets/mark-light.svg`

### Command Palette
- Replaces the old search modal + separate theme toggle
- Trigger: `/` key (when not in an input), `⌘K`/`Ctrl+K`, or gear button in header
- Header button: `.cmd-trigger` — `1.9rem` square, `border: 1px solid var(--border)`, no background, gear mark SVG (17px, `currentColor`)
- Overlay: `position: fixed; inset: 0; z-index: 300` with blurred backdrop (`rgba(0,0,0,0.4)` + `blur(3px)`)
- Box: `max-width: 540px`, `border: 1px solid var(--border)`, `border-radius: 0`, `var(--bg-page)` background
- Default state: "Go to" nav links + "Toggle theme (T)" action
- Search state: Pagefind results (7 max) — title + sanitized excerpt
- Excerpt sanitization: strips all HTML except `<mark>` highlights, truncates to ~140 chars
- Keyboard: ↑↓ navigate rows, Enter activates, Escape closes, T toggles theme
- Decoupled via `CustomEvent('open-command-palette')` — palette listens, header dispatches
- Pagefind loaded via `new Function` workaround to bypass Vite bundler resolution
- Powered by Pagefind (runs at build time — search unavailable in dev mode)

---

## Featured Images & Social (og:image)

**No featured images on post listings.** Posts are text-only in archive views.

**On individual posts:** `featuredImage` is optional. Only set when:
- You made the image (Excalidraw diagram, original photo, screenshot)
- The image directly illustrates something in the post
- Never use stock photos

**og:image fallback:** `/public/og.png` (1200×630)
The SEO component (`src/components/SEO.astro`) handles all og/twitter meta automatically.

---

## Content Collections

Three collections defined in `src/content/config.ts`:

| Collection | Path | URL pattern |
|------------|------|-------------|
| `posts` | `src/content/posts/` | `/{post.id}/` (flat, matches WP URLs) |
| `garden` | `src/content/garden/` | `/digital-garden/{slug}/` |
| `pages` | `src/content/pages/` | varies |

Post slugs are flat — no `/writing/` prefix. Preserves all existing WordPress URLs.
Date field: `data.date`. Draft filter: `!data.draft`.

---

## Voice & UI Copy

- Direct and specific. No hype language.
- Section labels are nouns or short phrases, not imperative verbs
- CTA buttons: specific action ("Subscribe to Digitally Literate →", not "Subscribe")
- Arrow in CTAs: use `→` not `>`

---

## What Not To Do

- No hero banners or full-bleed images on page headers
- No card grids with thumbnail images in post lists
- No sidebar, ever
- No gradients
- No shadows on cards — borders only, and only where needed
- No rounded corners — `border-radius: 0` everywhere
- No animation beyond subtle hover transitions (`0.15–0.25s ease`)
- No generic green on wiobyrne.com — green is reserved for explicit Digitally Literate / garden bridges
- No colored links — links match text color
- No avatar or headshot on the homepage — writing and mission statement carry credibility; faces read as personal blog, not publication
- Don't break the intro h1 into two lines — the run-on is intentional; the second clause is the landing, not a subtitle
- Don't add color accents to the intro — the only accent in the system is DL green (wrong site), and the sparse warmth is the point
- No font sizes below `0.7rem`
- No structural `hr` or divider lines — use spacing and tonal shifts

---

## Design Decisions Log

| Date | Decision | Reason |
|------|----------|--------|
| 2026-04-16 | No featured images on post listings | Text-first; old stock images were meaningless noise |
| 2026-04-16 | Flat post slugs (`/slug/`) | Preserves all existing WordPress URLs |
| 2026-04-16 | Static `/og.png` fallback | Every post needs a social share image |
| 2026-04-17 | Switched Lora → Source Serif 4 | Better optical sizing, variable font, stronger editorial weight |
| 2026-04-17 | Body defaults to serif, UI overrides to sans | Serif = read, sans = navigate. Prevents drift as site grows. |
| 2026-04-17 | Black links ecosystem-wide | Editorial precision — colored links pull eye away from content |
| 2026-04-17 | Green initially scoped to Digitally Literate only | Early boundary to keep wiobyrne.com from drifting into generic accent color usage |
| 2026-04-23 | Green allowed as ecosystem connective tissue on wiobyrne.com | The homepage needs visible bridges into Digitally Literate and the garden; green is reserved for those portals, not global chrome |
| 2026-04-17 | 0px border radius everywhere | Editorial precision aesthetic — no softening |
| 2026-04-17 | No-Line rule: hr/dividers → display:none | Tonal shifts and spacing carry structure; lines add visual noise |
| 2026-04-17 | Glass nav: backdrop-filter blur(12px) | Sticky nav needs presence without a hard line |
| 2026-04-17 | Warm palette: #f9f9f7 / #2d3432 | Warmer than pure white/black — lived-in, not clinical |
| 2026-04-17 | Token architecture: data-site attribute overrides | Single token file governs wiobyrne.com + DL + Understory |
| 2026-04-17 | Command palette replaces search + theme toggle | Unified interaction surface; `/` glyph as site identity element |
| 2026-04-17 | No avatar on homepage intro | Publication-first register, not personal blog; writing carries the credibility |
| 2026-04-17 | Intro h1 stays as one sentence | Run-on is intentional — second clause is the payoff, not a subtitle |
| 2026-04-17 | No color accent on intro h1 | Only accent in system is DL green (wrong site); sparse warmth is the design |
| 2026-04-20 | Homepage reduced from 6 sections to 5 | "What I do" repeated intro/newsletter intent; removal tightened the sequence |
| 2026-04-20 | Homepage reordered to Intro → Newsletter → Recent writing → Work with me → The Understory | Newsletter is the center of gravity; services and paid layer are downstream |
| 2026-04-20 | Homepage hierarchy solved through spacing and density shifts | Composition problem, not a design-system problem; no new fonts/palette/motifs added |
| 2026-04-20 | Newsletter block first used `var(--bg-subtle)` as a featured surface | Initial pass gave the primary conversion zone visual weight without reopening the whole palette |
| 2026-04-23 | Homepage newsletter block kept as a full green-tinted featured band | The homepage needs visual lift and a clear ecosystem bridge without turning green into a site-wide accent |
| 2026-04-20 | Homepage writing list now shows title + date + description | Improves scanability while preserving the editorial text-first approach |
| 2026-04-20 | Archive proof line added to homepage writing module | Signals decade-long accumulation rather than making the homepage feel like a fresh blog |
| 2026-04-22 | Wordmark changed from serif to boxed all-caps mono | JetBrains Mono is used for tags, dates, labels, code — wordmark as structural label is coherent; box creates a mark without a graphic |
| 2026-04-22 | Wordmark height locked to `1.9rem` matching gear trigger | Both marks same height = visual balance; bilateral framing of nav |
| 2026-04-22 | `/` command palette trigger replaced with gear mark SVG | Gear = Ian's mark since ~2018; dashed ring is distinctive; philosophically: gear = process/friction, garden = outcome — complementary metaphors across wiobyrne.com and DL |
| 2026-04-22 | Gear mark conceptual framing established | Gear represents creative process (churning, building, friction, making); garden represents outcomes (seeds → evergreens). wiobyrne.com shows the full cycle; DL shows what survives it |
| 2026-04-22 | favicon.svg added to public/ | Site had no favicon; SVG-first with .ico fallback; gear mark on warm-white background |
| 2026-04-22 | JetBrains Mono weight 700 added to Google Fonts import | Required for bold wordmark rendering |
