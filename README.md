# Apparatus

Apparatus is a reading-affordance design system for Astro sites.

The goal is simple: pages should help people read. If a visual pattern does not improve reading, orientation, or navigation, it does not belong.

## What's in this repo

- [`APPARATUS.md`](APPARATUS.md) - the short operational version
- [`WHY.md`](WHY.md) - the origin story and design thesis
- [`ANTI-PATTERNS.md`](ANTI-PATTERNS.md) - what the system is not
- [`RECIPES.md`](RECIPES.md) - a few page patterns you can reuse
- [`CHANGELOG.md`](CHANGELOG.md) - the current public version history
- [`DESIGN.md`](DESIGN.md) - the implementation reference for the wiobyrne Astro site
- [`screenshots/`](screenshots) - current visual references from Claude Design and the live site

## Core Vocabulary

- **Overstory** = newsletter + writing
- **Canopy** = book notes + digital garden + publications
- **Rhizosphere** = contact + about + work with me + structural pages

## Core Rules

1. Mono is the apparatus, serif is the human.
2. Use charcoal, warm white, and restrained green as meaning, not decoration.
3. Keep reg-marks and hairlines structural, not ornamental.
4. Avoid glass, rounded cards, and dashboard chrome.
5. Pages should read top-to-bottom in one column unless the content genuinely needs another structure.

## Pages

- `/writing/` - essay archive
- `/newsletter/` - newsletter front door
- `/book-notes/` - reading shelf
- `/publications/` - formal record
- static pages - about, contact, work with me, and similar entry points

## References

- [Homepage, light](screenshots/apparatus-home-light.png)
- [Homepage, dark](screenshots/apparatus-home-dark.png)
- [Live post, light](screenshots/apparatus-live-light.png)
- [Live post, full view](screenshots/apparatus-live-full.png)
- [Writing archive reference](screenshots/current-writing.png)

## Notes

This repo is intentionally lean. It is a system reference, not a component library.
If you fork it, start by reading `WHY.md` and `ANTI-PATTERNS.md`.

## License

MIT
