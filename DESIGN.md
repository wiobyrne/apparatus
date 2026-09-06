# DESIGN.md — wiobyrne.com

This file is the canonical implementation reference for the Astro site at
wiobyrne.com. It describes one surface expression of Apparatus, not the whole
system.

Token source of truth: `src/styles/tokens.css`
Global styles: `src/styles/global.css`
Site identifier: `data-site="wiobyrne"` on `<html>`

Layout files, corrected 2026-09-06 — there is no `BaseLayout.astro`:

- `src/layouts/ApparatusBase.astro` — the shell every page renders into
- `src/components/SEO.astro` — all head tags: icons, manifest, theme-color,
  og/twitter meta
- `src/layouts/WritingPost.astro`, `PublicationPost.astro`, `BookNotePost.astro`
  — the content layouts
- `src/components/Header.astro`, `Footer.astro`, `CommandPalette.astro`,
  `RegMark.astro` — the shared furniture

For the portable reading system and surface-adaptation rules, see
`APPARATUS.md` and `SURFACES.md`.

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

Values below reconciled against `tokens.css` and `apparatus-themes.css` on
2026-09-06.

### Light mode (default) — `:root` in `tokens.css`
```
--warm-white:    #f9f9f7    /* warm lived-in white — base surface */
--bg-canvas:     #f9f9f7    /* the canvas; --bg-page is an alias of this */
--bg-subtle:     #f2f4f2    /* elevated surface — code blocks, wells, understory */
--charcoal:      #2d3432    /* charcoal ink — warm, not cold black */
--text-main:     #2d3432
--text-secondary:#5a605e    /* metadata, captions */
--text-muted:    #6b716f    /* secondary text */
--text-soft:     #8a908e    /* timestamps, tertiary labels */
--border-ghost:  rgba(45, 52, 50, 0.15)   /* ghost border; --border aliases it */
--site-link:     #2d3432    /* links match text — black, editorial */
--hermes-gold:   #a47b2f    /* reserved: diptych spine, OG stamp-rule */
```

### Dark mode — `[data-mode="dark"]` in `apparatus-themes.css`
A desk-lamp posture, not an inverted day.
```
--bg-canvas:          #090b0c
--bg-subtle:          #101516
--warm-white:         #090b0c
--charcoal:           #ece8e2    /* primary text/strokes — now cream */
--text-main:          #ece8e2
--text-secondary:     #b8b2ab
--text-muted:         #848b86
--text-soft:          #646b66
--border-ghost:       rgba(236, 232, 226, 0.14)
--site-link:          #ece8e2
--hermes-gold:        #c9a84a
--shell-plate:        #0f1312
--shell-plate-strong: #151a19
--green-accent:       #7ea78e    /* desaturated so it doesn't glow */
```

`#1a1e1c` is **not** a canvas token. It survives only as the dark
`theme-color` meta in `SEO.astro` and as the OG card ground in
`src/lib/og-card.ts` — the dark plate the mark is stamped on, not the page
behind it. The earlier `--bg-page: #1a1e1c` / `--bg-subtle: #222826` /
`--text-main: #e6e4e1` block documented here described a build that no longer
exists.

Dark mode is a **manual** posture: `data-mode="dark"` on `<html>`, toggled from
the menu panel and stored in `localStorage('wiobyrne-reading-mode')`. There is
no `prefers-color-scheme` fallback. `ApparatusBase.astro` also accepts an
optional `theme` prop that stamps `data-theme` on `<html>`, but nothing sets it
and no stylesheet reads it — it is a hook, not a colour switch.

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

**Glass nav — retired 2026-09-06.** `--glass-surface`
(`rgba(249, 249, 247, 0.72)`) and a `blur(12px)` backdrop are still defined in
`tokens.css`, but the header stopped using them: it is a solid
`var(--bg-canvas)` bar with a hairline bottom border. The one surviving blur in
the system is the command palette backdrop. Kept here as a named token, not as a
header rule.

**Ambient shadow (used sparingly):**
```
--ambient-shadow: 0 0 40px rgba(45, 52, 50, 0.04)
```
0px offset. Never a drop shadow. Never on cards.

---

## Components

### Header — reconciled 2026-09-06
- `.app-header`: `position: sticky; top: 0; z-index: 100`
- Background: solid `var(--bg-canvas)` with a
  `1px solid var(--border-ghost)` bottom border. The glass-and-no-line
  treatment documented here previously — `var(--glass-surface)` plus
  `backdrop-filter: blur(12px)` — is not what ships; `--glass-surface` still
  exists as a token but the header does not use it
- No fixed height. `.app-header-inner` sets it through
  `padding: 16px clamp(20px, 2.75vw, 30px) 14px` inside `max-width:
  var(--width-site)`, flex, space-between, `gap: 20px`
- **There are no nav links in the header bar.** Navigation lives in the menu
  panel: `.app-menu-link` in `--font-mono` `0.8rem`, `letter-spacing: 0.06em`,
  no `text-transform`, `min-height: 1.85rem`, borderless and transparent
- Active page: `aria-current="page"` plus an `.is-active` class on the panel link
- The panel opens off `data-open="true"` on `.app-header`, animating
  `max-height` to `36rem`

#### Nameplate (left) — reconciled 2026-09-06
`.app-wordmark` is a link to `/` holding an inline regmark and the name.

- Treatment: **mixed-case name in Grenze Gotisch**, not a boxed mono label
- Name (`.wordmark-text`): `--font-identity` (Grenze Gotisch), `1.38rem`,
  weight `500` via `font-variation-settings: "wght" 500`,
  `letter-spacing: 0.01em`, no `text-transform`
- **`font-feature-settings: "ss01" 1` is required here.** Grenze's default
  capital I reads as an eth, so "Ian" renders as "Ðan". ss01 is the alternate
  capital set with a clean I, O, and B. Personal names take ss01 wherever they
  appear, including when a page hero is a name; display headlines that are
  phrases keep the ornate default caps
- Inline mark: `RegMark` `crosshair`, `size={14}`, `weight={1.45}`,
  `dotRadius={1}`, `gap: 0.55rem` from the name. This is regmark furniture
  beside the nameplate, not the identity mark — see "Marks" below
- Frame: `border: 1px solid transparent`, no background, no box-shadow,
  `border-radius: 0`, `min-height: 2.05rem`
- Hover: `opacity: 0.72`, no underline
- Rationale: the name is the nameplate. The boxed all-caps mono treatment locked
  on 2026-04-22 was a mark standing in for a graphic; once the finder mark
  arrived there was a real mark, and the wordmark could go back to being a name

#### Menu toggle (right) — reconciled 2026-09-06
- **The gear is retired.** It was pixel-identical to the Material Design
  settings icon and read as generic UI. There is no `.cmd-trigger` button, and
  the command palette has no header button at all
- `.app-menu-toggle` — a labelled control, not an icon: `MENU` in `--font-mono`
  `0.74rem`, `letter-spacing: 0.18em`, uppercase, with a `+` glyph
  (`.app-menu-toggle-glyph`) beside it
- Frame: `min-height: 2.05rem` (matching the nameplate), `padding: 0.38rem
  0.75rem 0.36rem`, `border: 1px solid var(--shell-border-strong)`,
  `border-radius: 0`, a plate gradient background with inset top highlight and
  bottom shadow
- Hover inverts to a charcoal plate with `--bg-page` text
- State: `aria-expanded` on the button, `aria-controls="app-menu-panel"`, and
  `data-open` on the header element
- Opens `#app-menu-panel`, a shallow drawer in three columns — **Pages**,
  **Tools** (theme, text size, search, topics, RSS), **Connect**

### Marks

There is one hierarchy. Do not describe any two marks as co-primary.

**Top level — the finder mark.** Three concentric squares, the orientation
target from the corner of a QR code: *here is the frame, orient yourself,
reading begins here*. It carries the favicon, app icon, social card, and the
joint diptych, and it represents the brand at the top level generally.

- Geometry: 24×24 grid centred on (12,12); outer rect 2.8→21.2, inner rect
  6.8→17.2, filled eye 9.8→14.2
- `fill: none`, `stroke-linecap: square`, `stroke-linejoin: miter`, no radius
- Stroke `1.6` at icon sizes; inline and decorative uses may drop to `1.2`
- Ink is the site's link colour: charcoal `#2d3432` on wiobyrne.com, green
  `#006d48` on Digitally Literate, lifting to `#3a8f68` on DL's dark canvas
  (`oklch(18% 0.028 152)` ≈ `#08150b`). `#1a1e1c` is wiobyrne.com's dark plate —
  its `theme-color` and OG card ground — not DL's canvas; the two were conflated
  until 2026-09-06
- Aged states — a misregistered ghost in the *other* property's accent, and
  weathering on the outer ring only — appear at **180px and up, never on favicons**
- The joint diptych is two clean finders facing a reserved gold `#a47b2f` spine,
  used only where both properties are credited together

**Beneath it — regmarks.** In-page instrument furniture, rendered through
`RegMark.astro` (`variant`, `size`, `weight`, `stroke`, `dotRadius`). `crosshair`,
`brackets`, `sighting`, and `quartered` ship today. The `colophon` plates are
optional regmarks: drawn, undeployed, usable if they earn a spot. None of these
is an identity mark, and none is the favicon.

**Retired, with reason — do not revisit:** gear (generic UI), mosaic/glitch
tiles (atmosphere, not identity), monogram (mud at 16px), dot-dissolve rings
(die below ~24px), collation tick.

**Acceptance test.** Any new mark earns its place by passing true 16/32/64px
rasterization — real pixel grids, not scaled vectors. Sources, proofs, and the
test script live in `04 META/48 Assets/Identity Marks/`.

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

### Favicon — updated 2026-09-04
- File: `public/favicon.svg` (primary) + `public/favicon.ico` (fallback), plus
  `apple-touch-icon.png`, `icon-512.png`, and `site.webmanifest`
- Declared in `src/components/SEO.astro`: SVG first, `.ico` as `sizes="any"`
  fallback, with a `?v=` cache-buster that bumps whenever the plate changes
- Design: the **finder mark**, charcoal `#2d3432`, inverting to `#e6e4e1` in dark
  via an embedded `prefers-color-scheme` block. Clean single-colour plate, no
  background square, no rounded corners
- Source SVG: `04 META/48 Assets/Identity Marks/svg/mark-wio-finder.svg`

### Command Palette — reconciled 2026-09-06
- Replaces the old search modal. It is **search only**: navigation and theme
  moved into the menu panel, so the palette no longer carries "Go to" rows or a
  theme action
- Trigger: `/` key (when not in an input), `⌘K`/`Ctrl+K`, or the **Search**
  action inside the menu panel. **There is no header button** — the gear that
  used to open it is retired
- Component: `src/components/CommandPalette.astro`, mounted once in
  `ApparatusBase.astro`
- Overlay: `position: fixed; inset: 0; z-index: 300` with blurred backdrop (`rgba(0,0,0,0.4)` + `blur(3px)`)
- Box: `max-width: 540px`, `border: 1px solid var(--border)`, `border-radius: 0`, `var(--bg-page)` background
- Empty state: an empty results region behind a `/` glyph and the input — no
  default row list
- Search state: Pagefind results (7 max) under a "Posts" group label — title + sanitized excerpt
- Excerpt sanitization: strips all HTML except `<mark>` highlights, truncates to ~140 chars
- Keyboard: ↑↓ navigate rows, Enter activates, Escape closes
- Decoupled via `Event('open-command-palette')` — palette listens; the header and
  the homepage dispatch
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
| 2026-09-04 | Finder mark adopted as the top-level brand mark for both properties | Survives 16px where dot-decay and barcodes fail; reads as native instrument vocabulary; a finder pattern is literally an orientation device, so form and thesis agree |
| 2026-09-04 | Crosshair demoted from identity mark to one regmark among several | At real size it reads unambiguously as a rifle scope; fine as page furniture, wrong as identity |
| 2026-09-04 | Colophon plate demoted to optional regmark | Its exploration stalled rather than concluded; kept as drawn-but-undeployed furniture, not a personal-authorship register |
| 2026-09-04 | Gear mark retired | Pixel-identical to the Material Design settings icon; reads as generic UI |
| 2026-09-04 | `rx="4"` removed from `public/favicon.svg` | Rounded corners had been shipping against the `--radius: 0` invariant |
| 2026-09-06 | Header nameplate reconciled to the live build | The 2026-04-22 boxed all-caps mono spec described a mark standing in for a graphic; once the finder mark existed, the wordmark could go back to being a name in Grenze |
| 2026-09-06 | `.cmd-trigger` spec removed; menu toggle documented instead | The gear it described was retired 2026-09-04 and the palette has had no header button since; the live control is a labelled `MENU` toggle opening a three-column panel |
| 2026-09-06 | Command palette documented as search-only | Navigation and theme moved into the menu panel; the "Go to" rows and the `T` theme action no longer exist |
| 2026-09-06 | Layout file names corrected | There is no `BaseLayout.astro`; the shell is `ApparatusBase.astro` with head tags in `SEO.astro` |
| 2026-09-06 | DL dark canvas corrected from `#1a1e1c` to `oklch(18% 0.028 152)` ≈ `#08150b` | `#1a1e1c` is wiobyrne.com's dark plate; DL's live token in `000-tokens.scss` is a different, darker green-black, and the two had been conflated across the kit |
| 2026-09-06 | "Known documentation drift" section removed | Its three items were reconciled against the live build rather than left standing |

---
