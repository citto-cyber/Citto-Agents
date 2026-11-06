# Spacing

Load when setting padding, gaps, or section rhythm. Index: [bnf.md](../bnf.md). Default: no custom values, use tokens.

## Spacing scale (`--space-*`, fluid)

| Token | Range (px) |
|-------|-----------|
| `--space-4xs` | about 5 (fixed) |
| `--space-3xs` | about 6.5 (fixed) |
| `--space-2xs` | about 8 |
| `--space-xs` | 10 → 11 |
| `--space-s` | 13 → 15 |
| `--space-m` | 16 → 20 |
| `--space-l` | 20 → 27 |
| `--space-xl` | 25 → 36 |
| `--space-2xl` | 31 → 47 |
| `--space-3xl` | 39 → 63 |
| `--space-4xl` | 49 → 84 |

Use these inside components: card padding, gaps, offsets.

## Section spacing (`--section-space-*`, fluid)

`--section-space-2xs`, `-xs`, `-s`, `-m`, `-l`, `-xl`, `-2xl` (from about 20–39px up to 78–218px).

- Sections get `--section-space-m` top and bottom **automatically** from the theme style.
- To change a section's rhythm (tight logo strip, roomy hero), set a different section-space token on **that section's class**, for example `_padding: {"top": "var(--section-space-xl)", "bottom": "var(--section-space-xl)"}`. Never type a value.

## Contextual spacing (use these by default)

| Token | Value | Use |
|-------|-------|-----|
| `--container-gap` | `--space-3xl` | Gap between major groups in a section (intro → grid → CTA) |
| `--content-gap` | `--space-m` | Gap between content items (heading → text → buttons) |
| `--grid-gap` | `--space-m` | Gap in grids |
| `--card-gap` | `--space-m` | Gap inside cards |
| `--gutter` | `--section-space-s` | Left and right section padding (already global) |

Halves and multiples are fine and used by the framework: `calc(var(--content-gap) / 2)`, `calc(var(--grid-gap) * 2)`.

## Rules

- **Gap first.** Give the parent flex or grid, then `_rowGap` / `_columnGap` / `_gridGap`. Avoid margins between siblings.
- **No spacing breakpoints.** The tokens are fluid. Only change spacing at a breakpoint when the layout itself changes.
- Vary the rhythm on purpose: tighter inside groups, looser between groups (see [design.md](../design.md)).
