# Layout: widths and grids

Load when setting element widths or building columns. Index: [bnf.md](../bnf.md).

## Content width

- `--content-width` = `128rem` (1280px). The theme style caps every **container** at this width, so don't set container widths yourself.
- The Style Manager's max screen width is also `var(--content-width)`.

## Width tokens

All are fractions of `--content-width`.

| Percentage | T-shirt | Fraction |
|-----------|---------|----------|
| `--width-10` | `--width-xs` | 10% |
| `--width-20` | `--width-s` | 20% |
| `--width-30` | | 30% |
| `--width-40` | `--width-m` | 40% |
| `--width-50` | | 50% |
| `--width-60` | `--width-l` | 60% |
| `--width-70` | | 70% |
| `--width-80` | `--width-xl` | 80% |
| `--width-90` | `--width-2xl` | 90% |
| `--width-content` | | 100% |

Use them as a **max** width (`_widthMax`) so elements still shrink on small screens. A typical centered intro is `_widthMax: var(--width-60)` plus `margin-inline: auto` (or `_alignItems: center` on the parent).

## Grid tokens

Equal columns: `--grid-1` … `--grid-12` (`repeat(n, minmax(0, 1fr))`)

Ratio columns:

| Token | Columns |
|-------|---------|
| `--grid-1-2` | 1fr 2fr |
| `--grid-2-1` | 2fr 1fr |
| `--grid-1-3` | 1fr 3fr |
| `--grid-3-1` | 3fr 1fr |
| `--grid-2-3` | 2fr 3fr |
| `--grid-3-2` | 3fr 2fr |

## Grid pattern in Bricks

```json
"_display": "grid",
"_gridTemplateColumns": "var(--grid-3)",
"_gridTemplateColumns:tablet_portrait": "var(--grid-2)",
"_gridTemplateColumns:mobile_portrait": "var(--grid-1)",
"_gridGap": "var(--grid-gap)"
```

- Bricks breakpoints here are desktop-first: the bare key is desktop, and `tablet_portrait` (≤991), `mobile_landscape` (≤767), and `mobile_portrait` (≤478) override it going down.
- Prefer grid tokens to `repeat(auto-fit, minmax(…))`, unless the item count is unknown (query loops), where auto-fit is fine.
- Two-column split layouts (text plus image) collapse to `--grid-1` at `mobile_landscape` or `tablet_portrait`.
