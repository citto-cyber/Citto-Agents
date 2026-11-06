# Typography

Load when working on headings, body text, or fonts. Index: [bnf.md](../bnf.md). Remember: **1rem = 10px**.

## Global defaults (theme style)

- **Body:** Figtree, `var(--text-m)`, line-height 1.4, `var(--body-text-dark)`
- **Headings:** Outfit, line-height 1.2, `var(--heading-dark)`
- **h1–h6** get `var(--h1)` … `var(--h6)` automatically from their tag.

Figtree and Outfit are the **framework placeholders**. Every project picks its own fonts during design (step 4) and swaps them in the theme style. Outfit is on the overused-font list in [design.md](../design.md), so don't keep it by default.

## Heading scale (fluid)

| Token | Range (px) |
|-------|-----------|
| `--h1` | 37.5 → 64 |
| `--h2` | 30 → 45 |
| `--h3` | 24 → 32 |
| `--h4` | 19 → 23 |
| `--h5` | 15.4 → 16 |
| `--h6` | about 12 (doesn't scale, see known issues) |

## Text scale (fluid)

| Token | Range (px) | Typical use |
|-------|-----------|-------------|
| `--text-2xs` | about 8 | Fine print only (fixed) |
| `--text-xs` | about 10 | Labels, small button text (fixed) |
| `--text-s` | 12.8 → 13.5 | Captions, meta |
| `--text-m` | 16 → 18 | Body (default) |
| `--text-l` | 20 → 24 | Lead paragraph, sub-heading |
| `--text-xl` | 25 → 32 | Large intro text |
| `--text-2xl` … `--text-4xl` | 31 → 76 | Display text, oversized numbers |

## Rules

- **Pick the heading tag for document structure; the size follows.** One `h1` per page, no skipped levels.
- **Visual size ≠ structure.** If an `h2` must look smaller, give its class `font-size: var(--h4)`. Don't change the tag.
- Use `--text-*` tokens for non-heading text sizes. Never type px or rem sizes.
- Keep body text at least `--text-m`. `--text-xs` and `--text-2xs` are too small for reading copy.
- Limit long text to about 65–75 characters per line (`max-width: 65ch` on the text's class, or a `--width-*` token).
- Accent or eyebrow text above a heading: put it **after** the heading in the markup and pull it above visually with `order: -1` (framework pattern `bm-accent-heading`). This keeps the heading first for screen readers.
