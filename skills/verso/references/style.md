# The style: a High Renaissance working notebook

The style comes from Leonardo da Vinci's notebooks, about 1487 to 1510. The skill
was built from five sheets, read side by side:

| Sheet | What it shows | Preset |
|---|---|---|
| Windsor, RCIN 919070 verso, about 1508 to 1510 | notes on the brain and cranial nerves, skull studies, a packing list for Pavia | `windsor` (default) |
| Codex Leicester, about 1506 to 1510, an opened spread | text blocks on the earth and the moon, a column of diagrams down the fold, ruled-off paragraphs, large initials | `leicester` |
| Vitruvian Man, Venice, Accademia, about 1490 | one figure in a circle and a square, a scale ruled under it, text above and below | `leicester` |
| Codex Arundel, British Library, a spread | calculations, compass studies, rotated notes, water stains, ink blots | `arundel` |
| Codex Forster, V&A, a pocket notebook | a column of text, a column of hatched solids numbered down the margin, crossings-out | `forster` |

The style is not "old paper". It is a set of specific physical facts, and each
fact maps to one decision in a UI. Sections 1 to 4 come from the Windsor sheet,
section 5 adds what the other four sheets teach.

## 1. The support: laid rag paper

Paper in 1500 was made from linen and cotton rags beaten to pulp, then lifted on a
wire mould. The mould leaves two kinds of mark you can still see against light:

- **Laid lines.** Many fine wires, close together, run one way. They leave a faint
  ribbed texture about 1 mm apart.
- **Chain lines.** Thicker wires that hold the laid wires, about 25 mm apart, run
  across them. They leave faint lines, darker at the edges where pulp collected.

Other paper facts on this sheet:

- **Tone.** The paper is not cream. It is a grey ivory, about `#ebe4d3`, warmer and
  darker at the edges where hands touched it.
- **Mottle.** Rag pulp is uneven, so the tone drifts in soft clouds.
- **Foxing.** Small brown spots from iron and mould in the fibres.
- **Damage and repair.** The lower left of the sheet is a later infill of lighter
  paper with a torn, irregular join. The edge of a handmade sheet is never straight.

UI mapping: one paper surface with noise grain, mottle, faint laid and chain lines,
a darker edge, a deckled (torn) border, and an optional lighter repair patch.

## 2. The medium: iron gall ink and sepia wash

Iron gall ink is made from oak galls and iron sulphate. It goes on near black and
oxidises over centuries to brown, then to tan where thin. So one sheet shows a
whole range of browns, from deep brown in fresh heavy strokes to amber in faint
ones. Washes are the same ink thinned with water and laid with a brush.

- **Ink pools** where the quill starts and stops, so line weight varies.
- **No line is mechanical.** Rules wander, boxes do not close square, a line is
  sometimes gone over twice.
- **Shading is hatching**, parallel strokes at about 45 degrees, from upper left
  to lower right for a left-handed pen. Shadow is never a soft grey fill.
- **Wash** pools unevenly into the fibres, with soft, ragged edges.

UI mapping: text and lines in browns only, a ramp of four ink strengths, every
line slightly displaced, hatching for every shadow and for depth, sepia wash for
emphasis behind figures. One extra colour is allowed: sanguine, the red chalk
Leonardo used in other drawings, kept for the single primary action.

## 3. The hand: left-handed mirror script

Leonardo wrote right to left with each letter reversed, a fast and dense Italian
cursive in a fine quill. Lines run edge to edge with almost no spacing between
blocks. Abbreviations and flourishes are common.

UI mapping: mirror script is texture, not content. Real UI text must stay
readable. So the theme uses three faces:

- a Renaissance roman for reading (EB Garamond, after Garamond's types of the
  1530s),
- an old printed face for titles (IM Fell, from 17th century types, close enough
  in feeling),
- a quick hand for margin notes (La Belle Aurore), used only for short notes.

Mirror text appears only as decoration, marked `aria-hidden`, set with
`transform: scaleX(-1)` at low opacity. It is never a label, a value or an
instruction.

## 4. The composition: a private working canvas

The sheet was not designed. It was filled. That gives it its layout rules:

- **Columns of different widths.** Blocks of text sit beside each other with
  ragged edges, wherever they fit.
- **Text wraps around figures.** Sketches sit in the text, not in a separate band.
- **Notes are boxed and joined.** Some blocks of text have a loose pen line drawn
  round them, and lines connect a note to the thing it is about.
- **Nothing is square.** Blocks sit at small angles.
- **Margins hold notes.** The edges of the sheet carry afterthoughts.
- **Scale differs.** Small dense writing beside a large careful drawing.

UI mapping: an asymmetric folio, a main column plus a margin for notes, a few
blocks at small rotations (under 1.5 degrees), loose pen frames in place of cards,
leader lines from a margin note to its subject, and one sketch per surface.

## 5. What the other sheets add

### Codex Leicester: the ordered working page

- **Paper yellowed to straw** with a strong, darker toned band at the edge and a
  warm glow at the centre. The ink has gone red-brown.
- **Text blocks are ruled off.** A paragraph ends with a pen line across the
  column and a small flourish at its right end. This is the clearest way the
  page marks "this thought is finished". UI: `.ms-endrule` after a section.
- **Large plain initials.** A new section starts with one large capital in the
  margin or at the start of the line, ink only. UI: `.ms-initial` on the first
  paragraph of a section. Never gilded, never boxed.
- **A column of diagrams.** Small diagrams stack down the fold between text
  blocks, each beside the passage it explains. UI: figures in the margin column,
  aligned to their text.
- **Lettered diagrams.** Points on a drawing are named a, b, c, and the text
  refers to them. UI: label chart points, steps or regions with italic letters.
- **The fold.** An open codex has a darker shade down the gutter. UI: `.ms-spread`
  for two equal columns.
- **Show-through.** Writing on the back of the leaf shows faintly through, so
  the whole sheet carries a ghost of mirrored text. UI: `.ms-showthrough`, very
  faint, decorative only.
- **Water damage.** A stain with a darker tide line where it dried. UI:
  `.ms-stain`, at most one.

### Vitruvian Man: the measured figure

- **One subject, centred, set in geometry.** A circle and a square drawn with
  compass and rule, and the figure inside them. UI: a hero or an empty state can
  carry one centred figure in a construction.
- **The scale.** A line ruled under the figure with tick marks, the end divisions
  cut finer, and the unit written beside it. UI: `.ms-scale` for a progress bar,
  a meter or a slider track.
- **Ground hatching.** Close horizontal strokes under the feet give the figure a
  floor. UI: `.ms-ground` under a figure or a sketch.
- **Text above and below**, centred on the figure, not wrapped round it.

### Codex Arundel: the scattered sheet

- **Grey paper and the darkest ink** of the four.
- **Calculations in the margin.** Figures stacked, ruled, summed. UI: `.ms-sum`
  for totals and breakdowns.
- **Notes at any angle.** Whole blocks are turned 90 degrees to fit the space.
  UI: decorative text only. Never rotate real content past a few degrees.
- **Many small sketches at once**, compass arcs, an ink blot, a stain.

### Codex Forster: the pocket notebook

- **A small bound book.** Lighter, cleaner paper. The edge is cut, not torn, and
  the stack of leaves shows down the binding side. UI: `.ms-bound` with
  `data-ms-paper="forster"`, good for narrow and mobile surfaces.
- **Two columns: text and drawings.** Each solid is hatched on its shadow faces,
  and numbered down the outer margin. UI: `.ms-figno` for step numbers, ranks and
  list indices.
- **Corrections in place.** A word struck through with a pen line and the new
  word written after it. UI: `<del>` and `<ins>`, styled by the theme. Use for
  changed values, diffs, and "was, now".
- **A folio number** in the top corner. UI: `.ms-folio-no` for a page or step
  number.

## 6. Choosing a preset

| The portion is | Preset | Composition |
|---|---|---|
| a form, a settings screen, a dense tool panel | `windsor` | `.ms-folio`, boxed notes, margin |
| an article, docs, release notes, long reading | `leicester` | ruled-off blocks, initials, diagrams in the margin, or `.ms-spread` |
| a hero, a landing section, an empty state | `leicester` | one centred figure in a construction, text above and below, a scale |
| a dashboard, a canvas, a board of many small parts | `arundel` | scattered blocks, sums in the margin, several small sketches |
| a narrow card, a sidebar, a mobile screen, a list | `forster` | `.ms-bound`, text column, numbered figures in the margin |

Pick by the portion's shape, not by taste. Use one preset per surface.

## 7. What it is not

These read as "fantasy parchment" and work against the reference:

- yellow or orange parchment, burnt edges, coffee rings, wax seals,
- blackletter (gothic) type, which is northern and earlier,
- drop caps with gold, illuminated borders, which belong to finished books,
- heavy textures that lower contrast,
- every element rotated, or rotations over 2 degrees,
- a collector's or a library's stamp, such as the red mark on the Arundel sheet.
  It belongs to that institution, and copying it imitates a real organisation.

The reference is a scientist's working page: restrained, monochrome, precise
lines, a dense but quiet surface.

## Palette (windsor)

Each preset sets the same tokens. Measured on its own paper:

| Preset | ink | ink-2 | ink-3 | sanguine |
|---|---|---|---|---|
| windsor | 10.6 | 6.3 | 4.9 | 5.9 |
| leicester | 10.3 | 7.0 | 5.8 | 5.7 |
| arundel | 12.0 | 7.3 | 5.2 | 5.7 |
| forster | 11.2 | 6.6 | 5.2 | 6.3 |

The toned edge band is darker, so keep real text out of it with padding.


| Token | Value | Use | On paper |
|---|---|---|---|
| paper | `#ebe4d3` | the sheet | |
| paper-light | `#f2ede1` | later repair, infill | |
| paper-dark | `#d9cdb2` | edges, handled areas | |
| ink | `#3f2a1a` | body text, titles | 10.6:1 |
| ink-2 | `#6b4a30` | secondary text, rules, frames | 6.3:1 |
| ink-3 | `#7d5a3a` | captions, placeholders, the floor for text | 4.9:1 |
| wash | `#b08a5e` | washes, hatching, never text | 2.5:1 |
| sanguine | `#8e3b23` | the one accent, primary action, focus | 5.9:1 |

## Mapping from a typical UI

| Typical UI | Manuscript |
|---|---|
| white or grey surface | paper with grain, laid and chain lines, deckled edge |
| card with border and shadow | loose pen frame, or no frame at all, hatched cast shadow if depth is needed |
| `box-shadow` | hatching (`.ms-cast`, `.ms-hatch`) |
| rounded corners | the hand radius, or none |
| brand colour | sanguine, once per surface |
| sans serif body | EB Garamond, old style figures |
| heading | IM Fell, italic for section heads, a double hand rule under it |
| divider | a freehand rule |
| input box | a word written on a ruled line |
| textarea | ruled lines for each line of writing |
| toggle or checkbox | an ink square marked with a cross |
| pill badge | a word circled by hand |
| table or stats grid | a ledger: rows on hand rules, dotted leaders to the value |
| icon | keep the icon, draw it in ink tone through the quill filter |
| image | sepia, multiplied into the paper |
| chart | pen lines and hatched fills, no gradients |
| empty space | margin notes, a sketch, or decorative mirror script |
| loading spinner | a line drawing itself on |
| toast or tooltip | a small slip of lighter paper |
| progress bar, meter, slider track | the scale (`.ms-scale`), end divisions finer |
| step numbers, ranks, list indices | figure numbers in the margin (`.ms-figno`) |
| changed value, diff, "was, now" | a correction, `<del>` struck by pen, `<ins>` in the hand |
| totals, breakdowns | a worked sum (`.ms-sum`) |
| section start | a plain initial (`.ms-initial`) |
| end of a section | a ruled-off line with a flourish (`.ms-endrule`) |
| chart points, regions | letters a, b, c |
| two equal columns | an open spread with the fold (`.ms-spread`) |
| page or step number | a folio number in the corner (`.ms-folio-no`) |

