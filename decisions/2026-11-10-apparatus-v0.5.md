---
title: Apparatus v0.5 — Type, Marks, and Share Surfaces
created: 2026-11-10
last_updated: 2026-11-10
status: canonical
categories:
  - Meta
tags:
  - apparatus
  - design
  - decisions
dg-publish: false
shelf: active
description: Decision record for Apparatus v0.5 typography, marks, and share surfaces.
---

# Apparatus v0.5 — Type, Marks, and Share Surfaces

Decision record · November 10, 2026  
Applies to: wiobyrne.com (live), digitallyliterate.net (in progress), slides, YouTube, share cards  
Supersedes: any earlier guidance naming Grenze Gotisch or Inter as Apparatus faces

## Why this revision

Apparatus asks whether each design choice helps someone read, orient, and move through the work. Reviewing the share layer (OG cards, slides, thumbnails) showed two problems:

1. The display face, Grenze Gotisch, worked as a short wordmark but failed at headline and thumbnail sizes. "AI", the most important word in most titles, became hard to read, and blackletter carries associations the work should not have to explain.
2. Personality had drifted into decoration. The system's real signatures are structural: the finder mark, the highlighter, issue numbering, and consistency across surfaces.

The fix follows the existing rule: structure first, personality at the edges.

## Type roles

### Websites: two families

| Role | Face | Notes |
|---|---|---|
| Reading and all headings | Source Serif 4 (variable) | Optical sizing on. Headings weight 600, display optical size (~60) for large headlines. Wordmarks set in this face. |
| System voice | JetBrains Mono | Navigation, menus, labels, dates, issue numbers, tags, metadata, search UI. |

No sans-serif on the websites.

### Slides and thumbnails: add one sans

| Role | Face | Notes |
|---|---|---|
| Thumbnail text, small slide UI | Source Sans 3 | Designed as Source Serif's companion. YouTube thumbnails: 2–4 words, heavy weight. Never used on the websites. |

### Retired

- **Grenze Gotisch**: retired from all surfaces.
- **Inter**: retired from all surfaces.

## Colour

Paper and ink distinguish the sites; structure unites them.

| | wiobyrne.com | Digitally Literate |
|---|---|---|
| Paper | Cool off-white `#f9f9f7` | Cream (OKLCH token in `000-tokens.scss`) |
| Ink | Charcoal `#2d3432` | Deep green |
| Accent | Green `#006d48` | Leaf green |
| Highlight tint | Pale green `#cfe5da` | Leaf tint `~#d9e4b5` |
| Dark mode | Follows system preference | Light only (revisit separately) |

Each site keeps one accent hue in both light and dark modes.

## The highlighter

The highlighter is a reader's act: marking what matters. It comes from the 2018 LRA deck and is the system's main voice.

- At most one highlighted phrase per title.
- Never in body text.
- Optional. Meaning must not depend on it.
- Websites and share cards: the site's own green tint.
- Slides and YouTube: the 2018 lime `#8cc63f` is allowed, because it must read from a distance.
- On wiobyrne.com, set per post with the optional `og_highlight` frontmatter field.

## Marks

| Mark | Role | Rules |
|---|---|---|
| Finder (three concentric squares) | Identity | Top-level mark for both sites, headers, favicons, card footers. Below ~16px use the simplified two-square version. Ink follows the site's ink or link colour. Optional offset ghost in the sibling site's colour. |
| Regmarks (crosshair, line with mark) | Punctuation | Structural only: slide cover rules, section heads, diagram corners, card footers. Never a substitute logo, never decoration in every corner. |
| Colophon plate | Optional | Unchanged. |

Hierarchy: the finder is the identity, the highlighter is the voice, regmarks are punctuation.

## Share cards

One layout, two colourways.

- 1200×630, single paper. No dark band.
- Top: mono label line (`ESSAY · NOV 5, 2026`, `NO. 455 · DIGITALLY LITERATE · NOV 4, 2026`).
- Title: Source Serif 600, display optical size. Never truncated; scale through set size steps instead.
- One to two lines of serif description, ending at a sentence or word boundary.
- Footer: finder mark and domain at left, topics or cadence in mono at right.
- Typographic quotes and apostrophes (’ “ ”), not straight ones.
- Dates use the frontmatter calendar date, formatted in UTC, identically on pages and cards.

## Slides

Built from the 2018 LRA structure: white space, one idea per slide, a highlighted phrase in the title, a thin rule with the finder mark sitting on it, then the byline.

- Titles: Source Serif 600. Body: Source Serif. Labels: JetBrains Mono. Small UI: Source Sans 3.
- Colourway by audience: DL colours for educator talks, wiobyrne.com colours for research talks.
- Core layouts: cover, section head, content, closing ("Follow the ideas" with both sites and an optional QR code).

## Working rules for AI-assisted changes

Learned during the wiobyrne.com pass:

- Work on a branch. Preview locally. Review before merging.
- Check `git status` before starting; separate unrelated uncommitted work instead of shipping it.
- Stage files explicitly, never `git add -A`.
- Never strip whitespace across a whole Markdown file; trailing double spaces are line breaks.
- Verify deployment constraints in the runbook rather than assuming them.
- Save build logs when a build fails.

## Status

- **wiobyrne.com**: complete (November 10, 2026). Grenze and Inter removed, finder mark in header, single-paper cards, default card regenerated, figures re-rendered without retired fonts, `og_highlight` documented.
- **digitallyliterate.net**: in progress. Replace Grenze in masthead, H1s, and footer; rebuild the default card in DL colours; add per-issue cards at build time.
- **Slides**: Google Slides master from the 2018 deck, not started.
- **YouTube**: thumbnail template, not started.
