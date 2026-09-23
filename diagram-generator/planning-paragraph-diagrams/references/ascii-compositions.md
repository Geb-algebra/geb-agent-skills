# ASCII Composition Rules

These rules define the canonical composition sketch for each planned diagram.

One cell is one full-width character, two half-width characters, or one emoji grapheme cluster. Code points inside an emoji grapheme cluster are not counted again. Ratios are width:height and use the area inside the outer border.

Because a horizontal text cell carries more information than one text row, convert a requested aspect ratio `W:H` to an inner cell ratio of `1.5W:H`. Thus 16:9 becomes 24:9.

## Border and symbols

- Each diagram entry has exactly one fenced code block containing one rectangular, bordered ASCII composition and any annotations directly below the border.
- Drawing occurs only inside the rectangular border.
- Borders and internal lines use `┌ ┐ └ ┘ ─ │ ├ ┤ ┬ ┴ ┼`, not ASCII or full-width substitutes.
- Adjacent lines are visibly continuous; corners, branches, and crossings use the matching box-drawing character.
- Arrows use `→ ↑ ↓ ←`.
- Every bordered row has the same width in cells. Box-drawing characters count as one half-width character, and every row has an even total number of half-width characters.

## Dimensions

- All compositions in one plan use the same inner width and height, including diagrams with fewer elements.
- With no requested ratio, use 16:9 and therefore a 24:9 inner cell ratio.
- If the user gives only inner width or height, derive the other dimension from the corrected cell ratio and round exact halves upward.
- If neither dimension is given, use the smallest common dimensions in which every composition can pass its blind evaluation and keep required elements, labels, and connections distinguishable.
- Determine common dimensions from the composition needing the most space; do not shrink individual diagrams.

## Composition and annotations

- The composition makes the position, occupied size, applicable direction, and connections of its elements distinguishable.
- The bordered area contains composition only, not color, emphasis, or art-style instructions.
- Put non-compositional visual instructions below the border but inside the same code fence. Annotations do not count toward the composition dimensions.

## Measurement

- Measure every composition, not a representative sample: row width, inner row count, half-width character count, corrected cell ratio, and box-line connectivity.
- Blank inner rows count toward height.
- Dimension notes never substitute for measuring the drawn composition itself.

