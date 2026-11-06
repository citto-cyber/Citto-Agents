# Colors

Load when setting backgrounds, text, heading, or border colors. Index: [bnf.md](../bnf.md).

## How to apply a color in Bricks

Colors are objects. Use `raw` with a variable:

```json
"_background": { "color": { "raw": "var(--bg-dark)" } },
"_typography": { "color": { "raw": "var(--body-text-white)" } }
```

Don't use palette `id`s or `hex` values for framework colors.

## Semantic tokens (use these first)

**Backgrounds**

| Token | Maps to | Use |
|-------|---------|-----|
| `--bg-body` | `--white` | Page background (already global) |
| `--bg-ultra-light` | `--base-l-10` | Subtle alternate section or panel |
| `--bg-light` | `--base-l-8` | Light panel |
| `--bg-semi-light` | `--base-l-5` | Mid-light surface |
| `--bg-dark` | `--base` | Dark section |
| `--bg-semi-dark` | `--base-d-5` | Darker surface |
| `--bg-ultra-dark` | `--base-d-10` | Darkest surface |
| `--bg-body-reverse` | `--black` | Inverted page surface |

**Body text:** `--body-text-dark` (default), `--body-text-semi-light`, `--body-text-light`, `--body-text-ultra-light`, `--body-text-white`

**Headings:** `--heading-dark` (default), `--heading-semi-light`, `--heading-light`, `--heading-ultra-light`, `--heading-white`

**Rule:** on a dark background (`--bg-dark`, `--bg-semi-dark`, `--bg-ultra-dark`), set **both** body text and headings to the white tokens. Headings carry their own global color, so changing the parent's text color won't recolor them. Do it on the section's class:

```css
.cta-banner { color: var(--body-text-white); }
.cta-banner :is(h1, h2, h3, h4, h5, h6) { color: var(--heading-white); }
```

## Palette ("BM - Colors")

Brand roots: `--primary`, `--secondary`, `--tertiary`, `--accent`, `--base`, `--neutral`
Fixed: `--white`, `--black`
Status: `--success`, `--warning`, `--info`, `--danger`

Each brand root (and base and neutral) has 10-step scales:

- **Tints** `--{color}-l-1` … `--{color}-l-10` (lighter as the number rises)
- **Shades** `--{color}-d-1` … `--{color}-d-10` (darker as the number rises)
- **Transparent** `--{color}-t-1` … `--{color}-t-10` (more opaque as the number rises, about 9% → 91%)

`--white` and `--black` only have `-t-1` … `-t-10`.

Framework defaults: primary, base, and neutral are near-black grays (`hsl(0 0% 15%)`), secondary is gold (`hsl(46 100% 44%)`), tertiary is blue (`hsl(199 80% 49%)`), and accent is magenta (`hsl(318 98% 46%)`). **Every project sets its own brand values in the palette.** Never assume these hues.

## Roles

- **Primary**: brand color and primary actions (buttons, links).
- **Secondary / tertiary**: supporting colors. Decide their job before using them.
- **Accent**: rare emphasis. It works because it's scarce (see [design.md](../design.md)).
- **Base**: surfaces and backgrounds (the `--bg-*` tokens point here).
- **Neutral**: text (the `--body-text-*` and `--heading-*` tokens point here).
- **Status colors**: form states and alerts only.

The framework author recommends a **monochrome scheme** (one brand hue plus neutrals) unless the project truly needs more. If it does, decide each color's role in the design before using it.

## Dark mode

The palette defines dark-mode values for the roots and their scales. Default mode is light.

- `--white` and `--black` **swap** in dark mode (`--white` becomes black). Read them as "surface" and "ink", not literal colors.
- That means `--heading-white` / `--body-text-white` become dark in dark mode. Check dark sections in both modes when the site offers a mode toggle.
- Tints and shades are remapped in dark mode so that `-l-*` stays "toward the background". Use semantic tokens and contrast usually holds.

## Contrast

Meet WCAG AA: 4.5:1 for body text, 3:1 for large text and UI parts. Light text tokens (`--body-text-light`, `--body-text-ultra-light`) are for de-emphasis on light surfaces, never for main copy. Never use gray text on a colored background. Use a deeper shade of that background, or `--white-t-*` / `--black-t-*`.
