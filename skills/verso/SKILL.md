---
name: verso
description: Restyle a chosen portion of an existing UI as a High Renaissance scientific manuscript, after Leonardo da Vinci's working notebooks (the Windsor sheets, Codex Leicester, the Vitruvian Man, Codex Arundel, Codex Forster) with four paper presets (iron gall ink faded to browns on laid rag paper, freehand rules, hatched shading, margin notes, decorative mirror script, pen sketches, an asymmetric working-page layout). Use when the user asks to turn a component, section, page or screen into a "manuscript", "Leonardo", "da Vinci", "Renaissance notebook", "codex", "old paper sketchbook", "sepia ink" or "parchment sketch" style, or runs /verso or /manuscript-ui with a target. Converts only the portion named, keeps the content, semantics and behaviour, and keeps every piece of real text readable.
---

# Verso

Turn a portion of an existing interface into a page from a High Renaissance
working notebook: iron gall ink, faded to browns, on laid rag paper.

The references are five of Leonardo da Vinci's sheets: the Windsor anatomical
notes (RCIN 919070 verso), a Codex Leicester spread, the Vitruvian Man, a Codex
Arundel spread and a Codex Forster notebook page. Read `references/style.md`
before the first conversion in a session. It explains
each physical fact of the style and the UI decision that follows from it. The
decisions below only make sense with it.

## Files in this skill

- `references/style.md` the research: paper, ink, hand, composition, palette with
  measured contrast, and a mapping table from common UI parts to manuscript parts.
- `assets/manuscript.css` the theme as plain CSS, scoped under `.ms-scope`, with
  four paper presets set by `data-ms-paper`. The source of truth for every value.
- `assets/defs.svg` four SVG filters (quill, freehand line, deckle, wash). Mount
  once per document.
- `assets/sketches.svg` pen sketches to place in a page: a geometry construction,
  a mechanism, a leader line, an ink blot, light rays with lettered points, a
  hatched solid.
- `examples/` two worked conversions, each a before and an after:
  `before.html` and `after.html` (a settings card, `windsor`), and
  `release-before.html` and `release-after.html` (release notes, `leicester`).
  `examples/index.html` shows them side by side and switches the preset. Read the
  after files as the standard a finished conversion has to meet.

## Step 1. Fix the scope

The user names a portion: a file, a component, a route, a selector, or a
description. Convert that portion and nothing else.

- If no target was given, ask for one. Do not restyle a whole app on a guess.
- Find the root element of the portion. Everything the theme does hangs off one
  `ms-scope` class on that root, so the rest of the app is untouched.
- If the portion is shared by other screens (a design-system button, a layout),
  say so and ask whether to convert the shared part or wrap a local copy.

## Step 2. Read the project before writing

- Find how the project styles things: Tailwind, CSS modules, plain CSS, a CSS-in-JS
  library, a component library. Port the theme into that idiom. Do not drop a
  second styling system into a project that has one.
- Read the project's rules file (`CLAUDE.md`, `AGENTS.md` or similar). If it bans
  raw hex in components, add the `--ms-*` values as tokens in its one stylesheet
  first, then use the tokens. If it has a type scale or a font loader, add the
  three faces through that loader (for example `next/font/google` in Next.js) and
  not through the `@import` line, which is only for plain HTML.
- Keep the project's own primitives. Restyle its `Button` through a variant or a
  class; do not replace it with a raw `<button>`.

## Step 3. Install the primitives once

1. **Tokens and classes.** Bring in `assets/manuscript.css`, or its equivalent in
   the project's idiom. In Tailwind v4, the tokens go in `@theme` and the
   multi-layer pieces (`.ms-page::before`, `.ms-frame`, `.ms-cast`, `.ms-button`)
   go in `@layer components`, since pseudo-element stacks do not fit utilities.
2. **Filters.** Mount `assets/defs.svg` once, inside or before the scoped root.
   In React, make it a small component. Without it the frames and rules render
   straight and the deckle disappears, which is a silent failure: check for it.
3. **Fonts.** EB Garamond (reading), IM Fell English (titles), La Belle Aurore
   (margin notes). Load only the weights used.

## Step 4. Choose a preset

Pick the preset by the portion's shape, with the table in section 6 of
`references/style.md`. In short:

- `windsor` for forms, settings and dense tool panels,
- `leicester` for articles, docs, release notes, heroes and empty states,
- `arundel` for dashboards, canvases and boards of many small parts,
- `forster` for narrow cards, sidebars, lists and mobile screens.

Set it as `data-ms-paper="..."` on the scoped root. `windsor` needs no
attribute. The user may name a preset or a codex, and that wins. One preset per
surface.

## Step 5. Convert, part by part

Work through the portion with the mapping table in `references/style.md`. The
rules that matter most:

- **Surface.** The root of the portion becomes `.ms-page`: paper, grain, laid and
  chain lines, deckled edge. Inner white or grey surfaces go. Use `.ms-repair`
  for at most one lighter patch, where a block needs separating.
- **Cards.** A card becomes a loose pen frame (`.ms-frame`) or nothing. Most
  groups need no frame: space and a hand rule separate them, as on the sheet. Use
  frames for the one or two blocks that are boxed notes.
- **Shadows.** Every `box-shadow` and elevation becomes hatching (`.ms-cast`) or
  goes. There are no soft grey shadows in this theme.
- **Corners.** Replace radii with `--ms-radius` (a hand-drawn radius) or none.
- **Colour.** Brown ink only. Body in `--ms-ink`, secondary in `--ms-ink-2`,
  captions in `--ms-ink-3`. The brand colour becomes sanguine, spent once per
  surface: the primary action, links and the focus ring.
- **Type.** Body in EB Garamond with old style figures. The title in IM Fell. A
  section heading in IM Fell italic with a double hand rule under it. Never set
  body text in the hand face: it is for short notes only.
- **Fields.** An input is a ruled line (`.ms-input`), a textarea is ruled lines,
  a checkbox is an ink square with a cross (`.ms-check`). Keep the real
  `<input>` and `<label>`; only the drawing changes.
- **Badges and tags** become circled words (`.ms-circled`).
- **Lists of values, stats and tables** become a ledger (`.ms-ledger`): rows on
  hand rules, dotted leaders to the value, old style figures.
- **Icons.** Keep the project's icons. Put them in ink tone and through the
  `ms-ink` filter. Do not swap them for emoji or glyphs.
- **Images** take `.ms-plate`: sepia, multiplied into the paper.
- **Charts** become pen lines and hatched fills. No gradients. Name points and
  regions with italic letters (`.ms-point`) the way the Leicester diagrams do.
- **Progress bars, meters and slider tracks** become the Vitruvian scale
  (`.ms-scale` with `--value`). Keep the element's role and aria values. For a
  native `<input type="range">` or `<progress>`, keep the native element and draw
  the scale behind it.
- **Step numbers, ranks and indices** become figure numbers in the margin
  (`.ms-figno`), as in Forster.
- **A changed value** is a correction: `<del>` struck by pen, `<ins>` in the
  hand. Only where the UI already shows an old and a new value.
- **Totals and breakdowns** can be a worked sum (`.ms-sum`), as in Arundel.
- **Sections in long text** start with a plain initial (`.ms-initial`) and end
  with a ruled-off line (`.ms-endrule`), as in Leicester.

## Step 6. Compose it as a working page

A straight conversion of a grid of cards into brown cards is the failure mode.
Re-compose the portion so it reads as a sheet that was filled, not designed:

- Use `.ms-folio`: the main column and a margin. Move secondary facts, hints and
  help text into the margin as `.ms-note`, with a leader sketch pointing at their
  subject where it helps.
- Let blocks differ in width. Put a sketch inside the text, not in its own band.
- Tilt two or three small blocks with `.ms-tilt-l`, `.ms-tilt-r` or `.ms-tilt-s`.
  Never tilt a form field, a table, or anything over about a third of the page.
- Add one pen sketch from `assets/sketches.svg` that fits the subject: the
  mechanism for settings or systems, the construction for layout, data or
  measurement. Draw a new one in the same manner if neither fits. One per surface.
- Keep to the decoration budget for one surface: one sketch (two at most), one
  stain or blot, one show-through, two mirror blocks. A page that carries all of
  them reads as a costume. Most surfaces need two or three of these, not all.
- Fill true empty space with at most two blocks of decorative mirror script
  (`.ms-mirror`, `aria-hidden="true"`). Write it in Italian of the period's
  manner (notes to self, lists, measurements). Do not present it as a real quote.
- DOM order stays the reading order. The layout may move things visually; the
  source order must still make sense to a screen reader and to Tab.

## Step 7. Guardrails

- **Contrast.** Real text never uses `--ms-wash`. Measure anything new against
  the paper: 4.5:1 for text, 3:1 for a meaningful graphic or a control's edge.
- **Mirror text is never content.** Labels, values, errors and instructions stay
  readable and the right way round.
- **Semantics stay.** Same elements, roles, names, states and handlers. A
  converted component must behave exactly as before.
- **Controls stay recognisable.** A button still looks pressable, a field still
  looks writable, focus is always visible (sanguine outline).
- **Motion.** The theme's motion is ink: a sketch drawing itself on with
  `data-draw`, a mark appearing in a checkbox. Hover and press are a wash, never
  a scale. Respect `prefers-reduced-motion`, which `manuscript.css` already does.
- **Cost.** Each filtered element is a filter pass. Keep filters on pseudo
  elements, frames and sketches, not on long lists of rows or on scrolling
  content. Do not put `ms-ink` on body text.
- **No institutional marks.** Do not copy a library's or a collector's stamp, a
  museum's catalogue number as branding, or Leonardo's name as a signature. The
  page is in his manner, not presented as his.
- **Light only.** The sheet is an object, so it does not invert in dark mode.
  If the app has a dark theme, the scoped portion keeps its paper.

## Step 8. Verify

1. Render the converted portion and take a screenshot. If a browser tool is
   available (agent-browser, Playwright, the preview pane), use it. Look at it.
2. Check the frames and rules are wavy. Straight ones mean the defs are not
   mounted, or the filter ids clash.
3. Tab through the portion. Every control is reached in a sensible order and
   shows the focus ring.
4. Check the page at a phone width. The folio collapses to one column.
5. Run the project's own check (typecheck, lint, build) if it has one.

## Report

When done, tell the user in a few short lines:

- what portion changed and which files,
- which preset, and why it fits the portion,
- what was added once (tokens, fonts, filters) and where,
- any part left as it was, and why,
- how to see it (the route or the file to open).
