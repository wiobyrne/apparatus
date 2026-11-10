# Surfaces

Apparatus is portable. It keeps the reading contract stable while changing the
expression to fit the medium.

## Shared layer

These should stay recognizable across surfaces:

- reading-first posture
- clear hierarchy
- selective linking
- metadata as wayfinding
- Source Serif 4 for web reading and headings, JetBrains Mono for web system voice; Source Sans 3 only for slide UI and thumbnails
- one identity mark (finder), with regmarks used as structural punctuation
- the highlighter as an optional title treatment, never body decoration
- calm composition
- accessible behavior
- restrained use of color and chrome

The shared design decisions in this document and `APPARATUS.md` are
authoritative for Apparatus. Individual site repositories own their exact
implementation and any documented surface-specific exception. Vault notes
preserve rationale and history and route readers here; they do not supersede
these shared rules.

## Tunable layer

These can change by surface:

- tone
- density
- motion
- accent usage
- visual roughness
- amount of supporting chrome
- how editorial, connective, or exploratory the surface feels

## Surfaces Apparatus can live in

### Astro sites

- keep the page readable first
- keep the archive and detail shapes distinct
- keep the homepage oriented, not overloaded
- use Source Serif 4 for reading, all headings, and wordmarks; set headings at 600 with optical sizing
- use JetBrains Mono for navigation, menus, labels, dates, metadata, tags, and search
- use no sans-serif on the websites
- wiobyrne.com follows the system theme by default and supports a reader's
  stored light/dark override
- Digitally Literate offers a reader-controlled light/dark theme; its
  implementation owns the exact default, persistence, and token values

### Share cards

- use a single 1200×630 paper layout with one of the two site colorways
- place the mono label above a Source Serif 600 title; never truncate the title
- keep the serif description to one or two lines and end at a sentence or word boundary
- place the finder and domain in the footer, with topics or issue cadence in mono
- use the frontmatter calendar date in UTC, matching page dates
- allow at most one optional highlighted phrase in a title; use typographic quotation marks and apostrophes

### Newsletters

- keep the issue readable on its own
- use the same hierarchy logic as the web
- keep the publication front door simple
- Substack is a separate platform adaptation: preserve Apparatus identity
  within platform constraints, without requiring pixel-identical website
  typography or layout. Its branding and publishing workflow are documented
  with the newsletter surface, not in the website implementation contracts.
- Substack's native post headings and body may use Lora where platform
  constraints call for it. This allowance applies to Substack only; website
  headings and reading text use Source Serif 4. Branded wordmarks and issue
  images use Apparatus typography.

### Open Graph cards

- use a single paper-colored 1200×630 composition for each site's own palette;
  do not add a dark band
- use JetBrains Mono for metadata, Source Serif 4 for the title and a concise
  one- or two-line description, with the finder and domain in the footer
- title highlighting is optional, limited to one phrase, and uses the site's
  own tint; exact rendering and generation behavior belong to each site repo

### Slide decks

- reduce density
- simplify the pattern vocabulary
- use Apparatus to stage ideas, not cram detail
- set titles and body in Source Serif 4, labels in JetBrains Mono, and small UI in Source Sans 3
- build from the 2018 LRA structure: one idea, a highlighted title phrase, rule with finder, then byline
- choose DL colors for educator talks and wiobyrne.com colors for research talks
- legacy lime `#8cc63f` remains available for slides and YouTube thumbnails;
  it is not a website highlight color

### YouTube thumbnails

- use Source Sans 3 for short, heavy thumbnail text (two to four words)
- use the 2018 lime highlight when needed for distance legibility
- keep the finder as identity and highlight at most one title phrase

### Diagrams and teaching visuals

- make one idea visible at a time
- keep the composition compact
- avoid decorative clutter that competes with the lesson

### Note systems

- keep the graph and links legible
- preserve progression and connection
- avoid turning notes into a presentation layer

## Questions to ask for any new surface

1. What is the reader trying to do here?
2. What must remain true for this still to feel like Apparatus?
3. What can change so the surface fits the medium better?
4. What should not be imported from another surface?

## Good default

If you are unsure, keep the layout vertical, keep the record block factual,
and keep the next useful path obvious.
