# Changelog

## v0.4 — 2026-09-06

Reconciled the remaining stale sections against the shipped site and removed the
drift list rather than carrying it forward.

- Rewrote the header **nameplate** spec: the live header is a mixed-case "Ian
  O'Byrne" in Grenze Gotisch at weight 500 with an inline crosshair regmark and a
  transparent frame, not the boxed all-caps mono label locked in April.
- Recorded the **ss01 requirement** for personal names set in Grenze — the
  default capital I reads as an eth, so "Ian" renders as "Ðan". Display
  headlines that are phrases keep the ornate default caps.
- Replaced the `.cmd-trigger` gear spec with the live **`MENU` toggle** and its
  three-column panel (Pages, Tools, Connect).
- Corrected the **command palette** to what it actually is: search only, opened
  by `/`, `⌘K`/`Ctrl+K`, or the panel's Search action. No header button, no "Go
  to" rows, no `T` theme action.
- Corrected the **colour tokens** in both modes. The documented dark block
  (`--bg-page: #1a1e1c`) described a build that no longer exists; the live dark
  canvas is `#090b0c`. `#1a1e1c` survives only as the dark `theme-color` meta
  and the OG card ground.
- Corrected the **Digitally Literate dark canvas** from `#1a1e1c` to its live
  token, `oklch(18% 0.028 152)` ≈ `#08150b`. `#1a1e1c` is wiobyrne.com's dark
  plate; the two had been conflated across the kit.
- Corrected the **theme mechanism**: dark mode is manual `data-mode="dark"`
  stored in `localStorage('wiobyrne-reading-mode')`, with no
  `prefers-color-scheme` fallback.
- Listed the real **layout files**. There is no `BaseLayout.astro`; the shell is
  `ApparatusBase.astro` with head tags in `SEO.astro`.
- Corrected the **header shell**: it is a solid `--bg-canvas` bar with a
  hairline bottom border, not a glass-and-no-line nav, and it carries no nav
  links — navigation moved into the menu panel. `--glass-surface` survives as a
  token; the only blur left in the system is the palette backdrop.
- Removed the "Known documentation drift" section added in v0.3. Its three items
  are now reconciled.

## v0.3 — 2026-09-04

Established a single mark hierarchy and corrected canon that had gone stale.

- Adopted the **finder mark** — three concentric squares, the QR finder pattern —
  as the top-level brand mark for wiobyrne.com and digitallyliterate.net.
- Demoted the crosshair from identity mark to one regmark among several.
- Demoted the colophon plate to an optional regmark; it is not a personal
  authorship register.
- Retired the gear mark, and removed the gear's "do not replace" instruction,
  which had described an abandoned plan since roughly May.
- Documented the two-state sizing rule: clean plate at favicon sizes, aged
  (misregistered and weathered) at 180px and up.
- Reserved gold `#a47b2f` to the diptych spine and the social-card stamp rule.
- Corrected asset paths from `04 META/🔗 Assets/` to
  `04 META/48 Assets/Identity Marks/`.
- Removed a `border-radius` that had been shipping on the favicon against the
  `--radius: 0` invariant.
- Added a "Known documentation drift" section listing header and layout
  specifications that still describe an earlier build.

## v0.2 — 2026-06-01

Expanded Apparatus from an Astro-only reference into a portable reading
framework for digital publishing.

- Broadened the thesis to cover multiple surfaces.
- Added a surface-adaptation guide for web, notes, newsletters, slides, and diagrams.
- Added a glossary of canonical terms.
- Reframed the repo as a reference kit people can borrow and adapt.
- Kept the wiobyrne.com Astro implementation as one surface, not the whole system.

## v0.1 — 2026-05-04

Initial public version of Apparatus.

- Established the thesis: every visual choice should help a reader read.
- Locked the core rules around type, color, structure, and layout.
- Defined the site vocabulary:
  - Overstory
  - Canopy
  - Rhizosphere
- Documented the main page recipes and reading affordances.
- Included screenshots from the current Claude Design / live-site system.
