# Borders, radius and shadows

Load when adding borders, rounding corners, or elevating elements. Index: [bnf.md](../bnf.md).

## Borders

| Token | Value |
|-------|-------|
| `--border--light` | 1px solid `--border-color--light` (`--base-l-9`) |
| `--border--semi-light` | 1px solid `--border-color--semi-light` (`--base-l-5`) |
| `--border--dark` | 1px solid `--border-color--dark` (`--base`) |
| `--border--white` | 1px solid `--border-color--white` (`--white`) |

Building blocks: `--border-width` (1px), `--border-type` (solid), plus the `--border-color--*` tokens.

In Bricks settings, borders are an object with a width, style, and color:

```json
"_border": {
  "width": { "top": "var(--border-width)", "right": "var(--border-width)", "bottom": "var(--border-width)", "left": "var(--border-width)" },
  "style": "solid",
  "color": { "raw": "var(--border-color--light)" }
}
```

In custom CSS, use the shorthand: `border: var(--border--light);`

No side-stripe accent borders (thick colored `border-left`). That pattern is banned in [design.md](../design.md).

## Radius

Scale: `--radius-xs` (8px), `--radius-s` (16px), `--radius-m` (24px), `--radius-l` (32px), `--radius-xl` (40px), `--radius-2xl` (64px), `--radius-50` (50%), `--radius-circle` (999px)

**Contextual (use these first):**

| Token | Default | Use |
|-------|---------|-----|
| `--radius-card` | `--radius-s` | Cards and panels |
| `--radius-img` | `--radius-s` | Images and media |
| `--radius-btn` | `--radius-xs` | Custom button-like elements |

```json
"_border": { "radius": { "top": "var(--radius-card)", "right": "var(--radius-card)", "bottom": "var(--radius-card)", "left": "var(--radius-card)" } }
```

Nested rounded elements: the inner radius should be about the outer radius minus the padding, so the corners look parallel.

## Box shadows

`--box-shadow-xs`, `-s`, `-m`, `-l`, `-xl`: soft, even shadows tinted with `--black-t-3`.

In Bricks, pass the whole token as a raw color (framework pattern):

```json
"_boxShadow": { "color": { "raw": "var(--box-shadow-m)" } }
```

Use shadows to show real elevation (sticky header, dropdown, modal, hover lift). Don't use them as decoration on every card.
