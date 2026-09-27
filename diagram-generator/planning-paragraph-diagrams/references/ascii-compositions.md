# ASCII Composition Rules

These rules define the structural composition sketch for each planned diagram.

## Interpretation boundary

The ASCII composition specifies the diagram's semantic structure, not its final rendering. Its binding information is:

- the elements and their semantic kinds or roles;
- which elements are connected, grouped, contained, ordered, or branched;
- connection direction (source and target), semantic order, and coarse relative placement; and
- labels needed to identify those elements and relationships.

Coarse relative placement means that left/right, above/below, the primary layout direction, and the rough ordering of elements remain recognizable. Do not reverse these relations or turn a horizontal arrangement into a vertical one. Exact coordinates, distances, alignment, occupied sizes, aspect ratios of individual elements, and proportions are not binding. For example, a target drawn below its source remains broadly below it, but its offset, distance, alignment, and size may change.

The ASCII composition also does not specify final shape geometry, color, typography, line treatment, decoration, or visual style. The outer border defines the composition canvas and is not itself a diagram element unless the plan explicitly identifies a semantic container.

A downstream implementer preserves the elements, topology, and coarse relative placement while choosing exact positions, sizes, shapes, styling, emphasis, and visual hierarchy appropriate to the target medium. Faithful implementation therefore preserves the sketch's recognizable spatial organization without literally tracing its text grid. Implementations should use the medium's visual capabilities to produce an effective design rather than defaulting every element to the same shape, size, or color.

One cell is one full-width character, two half-width characters, or one emoji grapheme cluster. Code points inside an emoji grapheme cluster are not counted again. Ratios are width:height and use the area inside the outer border.

Because a horizontal text cell carries more information than one text row, convert a requested aspect ratio `W:H` to an inner cell ratio of `1.5W:H`. Thus 16:9 becomes 24:9. This is an exact ratio of measured inner width cells to inner rows, not a target or approximation. Choose integer dimensions proportional to the converted ratio; for example, 24×9 or 48×18 cells both satisfy 24:9, while 24×18 cells do not.

## Border and symbols

- Each diagram entry has exactly one fenced code block containing one rectangular, bordered ASCII composition and any annotations directly below the border.
- Drawing occurs only inside the rectangular border.
- Borders and internal lines use `┌ ┐ └ ┘ ─ │ ├ ┤ ┬ ┴ ┼`, not ASCII or full-width substitutes.
- Adjacent lines are visibly continuous; corners, branches, and crossings use the matching box-drawing character.
- Arrows use `→ ↑ ↓ ←`.
- Every bordered row has the same width in cells. Box-drawing characters count as one half-width character, and every row has an even total number of half-width characters.

## Dimensions

- All compositions in one plan use the same inner width and height, including diagrams with fewer elements.
- With no requested aspect ratio, use 16:9 and therefore an exact 24:9 inner cell ratio.
- When an aspect ratio `W:H` is requested, multiply only its width by 1.5 and use the resulting `1.5W:H` as the exact inner cell ratio for every composition in the plan.
- The measured inner width in cells divided by the measured inner row count equals the required corrected ratio exactly. Reduce both ratios or cross-multiply them when checking equality; visual approximation and rounded ratio equality are not sufficient.
- If the user gives only inner width or height, derive the other dimension from the corrected cell ratio. The derived dimension must be an integer; if it is not, report that the requested dimension conflicts with the exact ratio rather than rounding it.
- If neither dimension is given, use the smallest common integer multiple of the corrected ratio in which every composition can pass its blind evaluation and keep required elements, labels, and connections distinguishable. Test smaller candidates only at the same corrected ratio.
- Determine common dimensions from the composition needing the most space; do not shrink individual diagrams.

## Composition and annotations

- The composition makes its elements, semantic relationships, connection sources and targets, semantic order, and coarse relative placement distinguishable. These qualitative spatial relations are preserved, but the sketch does not prescribe exact coordinates, distances, alignment, proportions, or dimensions.
- The bordered area contains composition only, not color, emphasis, or art-style instructions.
- Put non-compositional visual instructions below the border but inside the same code fence. Annotations do not count toward the composition dimensions.

## Measurement

- Measure every composition, not a representative sample: row width, inner row count, half-width character count, inner width in cells, exact corrected cell ratio, and box-line connectivity.
- Blank inner rows count toward height.
- Dimension notes never substitute for measuring the drawn composition itself.
