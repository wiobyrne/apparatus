# Apparatus

Apparatus is the reading-affordance design system for the wiobyrne ecosystem.

It is not a style guide first. It is a system for making pages easier to read, easier to orient in, and easier to keep consistent as the site grows.

## Thesis

Every visual choice should help a reader read. If a pattern does not improve reading, navigation, or orientation, it does not belong.

## Vocabulary

- **Overstory** = newsletter + writing
- **Canopy** = book notes + digital garden + publications
- **Rhizosphere** = contact + about + work with me + structural pages

Use this vocabulary consistently across the public surfaces and the docs.

## Core Rules

1. Mono is the apparatus, serif is the human.
2. Use charcoal, warm white, and restrained green as meaning, not decoration.
3. Keep reg-marks and hairlines structural, not ornamental.
4. Avoid glass, rounded cards, and dashboard chrome.
5. Pages should read top-to-bottom in one column unless the content genuinely needs another structure.

## Public Surfaces

- `/writing/` = essay archive
- `/newsletter/` = newsletter front door
- `/book-notes/` = reading shelf
- `/publications/` = formal record
- static pages = about, contact, work with me, and similar entry points

## Metadata

- `description` = subtitle under the title
- `lede` = optional intro, only when the post needs a more deliberate opening
- `colophon` = optional per-post closing note
- `published` in the vault = should be pushed to Astro
- `draft` in Astro = whether the page renders publicly

## Link Types

- Tags = cross-site discovery
- `see also` = manual sideways link when a post has a real conceptual neighbor
- `prev/next` = reading order

## Notes for Future Work

- Footnotes can be added note by note as posts are migrated.
- The post shell should stay lean by default.
- If a new pattern keeps showing up, document it here before it spreads.

## Reference Screens

These screenshots are the clearest current references for how Apparatus should feel in practice.

- [Homepage, light](screenshots/apparatus-home-light.png)
- [Homepage, dark](screenshots/apparatus-home-dark.png)
- [Live post, light](screenshots/apparatus-live-light.png)
- [Live post, full view](screenshots/apparatus-live-full.png)
- [Writing archive reference](screenshots/current-writing.png)

Keep these in sync with the live shell when the layout changes materially.
