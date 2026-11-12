# Apparatus

## Authority

This repository is the authoritative source for shared Apparatus design
decisions. `APPARATUS.md` states the shared principles; `SURFACES.md` records
how they translate across media. Website repositories own implementation
details, exact tokens, components, build behavior, and documented local
exceptions. The Obsidian vault preserves rationale, dated decisions, and
history, and links readers to these specifications and to the implementations.
If a shared rule changes, update this repository first and then align affected
surface documentation. Do not maintain a second full specification in the
vault or a site repository.

Apparatus is a portable reading interface framework for digital publishing.
It is also a public practice of digital literacy: a way of designing, writing,
and documenting digital spaces where reading, authorship, and judgment remain
visible and negotiable.

It translates print habits into pixel spaces so pages stay readable,
oriented, and human across surfaces.

The framework is one part of that practice. The repository records the shared
agreements that shape Apparatus and why consequential agreements change; it
does not attempt to disclose or preserve every private step in the work.

## Thesis

Every visual choice should help a reader read.

If a pattern does not improve reading, orientation, or navigation, it does not
belong.

## Canonical vocabulary

- **reading-first** = a design posture where reading is the primary job of the page
- **reading contract** = the stable expectations readers can count on across surfaces
- **surface** = a destination where Apparatus is expressed in a specific medium
- **surface translation** = keeping the reading contract stable while changing the expression to fit the medium
- **pattern** = a reusable structural form that repeats across pages or surfaces
- **anti-pattern** = a pattern Apparatus explicitly avoids because it undermines reading
- **portable** = able to move into another medium without losing the core reading behavior
- **interface grammar** = the rules that govern how a page is put together

## What Apparatus includes

- core rules
- surface translation
- reusable patterns
- implementation references
- public-facing documentation

## What it is not

- not a theme
- not a component library
- not tied to a single tool or platform
- not a slide template or note skin
- not a second navigation system

## How to adapt it

- keep the reading contract stable
- tune tone, density, motion, and accent by surface
- add patterns only when they repeat
- keep anti-patterns updated when drift appears
- document surface-specific behavior when a medium proves a stable need

## Where it shows up

- Astro and other web sites
- diagrams and teaching visuals
- newsletters and publication front doors
- slide decks and presentation frames
- note systems such as Obsidian

## Core rules

1. On websites, Source Serif 4 carries reading, headings, and wordmarks; set
   headings at weight 600 with optical sizing. JetBrains Mono carries
   navigation and system information.
2. Source Sans 3 is reserved for slide UI and YouTube thumbnails; websites use no sans-serif.
3. The three-concentric-square finder is the identity mark; use its simplified
   small-size form below about 16px. Regmarks and hairlines are structural
   punctuation, never substitute logos.
4. Use each site's paper, ink, link, and highlight roles consistently. The
   wiobyrne.com light palette uses warm white `#f9f9f7`, charcoal `#2d3432`,
   and green `#006d48`; DL uses its own cream paper, deep-green ink, leaf-green
   links, and leaf-tint highlight. Exact site and card values belong to the
   owning repositories' tokens and OG implementations.
5. A highlighter may mark at most one optional title phrase; it never carries
   meaning on its own and never appears in body text. Use the site's tint on
   websites and cards; the legacy lime `#8cc63f` is reserved for slides and
   YouTube thumbnails.
6. Share cards carry one paper field, a readable title, concise description, and finder footer.
7. Avoid glass, rounded cards, and dashboard chrome.
8. Pages should read top-to-bottom in one column unless the content genuinely needs another structure.

For current site color values and component behavior, consult each site's
implementation tokens and components; this shared specification defines the
color roles and surface distinctions, not a duplicate token inventory.

For a plain-language overview, see `ABOUT.md`.
For the problem statement behind Apparatus, see `WHY.md`.
For the surface-specific adaptation guide, see `SURFACES.md`.
For the implementation reference, see `DESIGN.md`.
