# Bricks Native Framework (BNF)

Apply these rules on every Bricks project. The design system is the Bricksmaven **Bricks Native Framework**: design tokens defined with the Bricks 2.2+ Style Manager (variables, color palette, theme style). There is no third-party CSS framework, no ACSS, and no generated utility classes.

Topic references live in [bnf/](bnf/). Read the matching file before styling that area.

## When to use

Load this doc **before** writing or reviewing any Bricks layout, global class, or CSS. Every styling decision starts with BNF tokens, then BEM global classes, then (rarely) custom CSS.

## Is BNF installed?

The site has BNF when the Bricks editor shows the **BM - Colors** palette and variables such as `--space-m`, `--section-space-m`, `--content-width`, and `--btn-primary-background` (Style Manager → Variables).

- If the user shares fresh exports, those exports win over the values in these docs. The values here are the framework defaults, and each project retunes them.
- If the variables are missing, **do not assume BNF**. Ask the user, or fall back to plain values per [css.md](css.md).

## Root font size: 1rem = 10px

The Style Manager sets `htmlFontSize: 10px`. **On BNF sites 1rem = 10px, not 16px.**

- `1.6rem` = 16px, `2.4rem` = 24px, `12.8rem` = 128px.
- Converting px from a design: divide by 10 (`40px → 4rem`).
- Every token is already in this unit. You rarely need to write rem yourself. When you do, use the 10px base.

## Core rules

- **Tokens first.** Use `var(--space-m)`, `var(--primary)`, `var(--radius-card)`, and so on. Never hardcode hex, px, or `repeat(3, 1fr)` when a token exists.
- **Trust the tokens.** Assume they are configured. Do not look up their computed values before using them.
- **Close is good enough.** If a comp says `88px` of padding, use the nearest `--space-*` or `--section-space-*` token. Never write a one-off value to match a screenshot exactly.
- **Semantic over raw.** Prefer contextual tokens (`--bg-dark`, `--body-text-light`, `--heading-dark`, `--content-gap`, `--radius-card`) over raw scale tokens (`--base-d-5`, `--neutral-l-6`, `--space-m`) when one fits the intent.
- **Never invent token names.** Only use names listed in [bnf/](bnf/). For a rare one-off, set a locally scoped custom property on the class (`--_offset: 1.2rem`), never a fake framework token.
- **Variables over utility classes.** BNF ships no utility classes, by design. Style with BEM global classes that use variables (see [bricks.md](bricks.md)).
- **Don't redeclare what's global.** The theme style already handles body and heading typography, link color, button styles, section padding, container width, and site background (see the table below).
- **Gap first.** Space siblings with `gap` / `_rowGap` / `_columnGap`, not margins.
- **Fluid by default.** The spacing and type tokens are `clamp()`-based. Don't add breakpoint overrides for spacing or font size. Breakpoints are for layout changes (columns, direction, order, visibility).
- **Light and dark modes.** The palette has dark-mode values (default mode: light). Use semantic tokens so both modes work, and read the dark-mode notes in [bnf/colors.md](bnf/colors.md).

## Handled globally by the theme style ("BM CSS theme style", applies site-wide)

| Area | Global setting | Consequence |
|------|----------------|-------------|
| Section padding | `--section-space-m` top/bottom, `--gutter` left/right | Don't add padding to `section` elements. To change rhythm, set a different `--section-space-*` on that section's class. |
| Container | `width: 100%`, `max-width: var(--content-width)` (128rem) | Don't set container widths. Narrow content with `--width-*` tokens. |
| Body text | Figtree, `var(--text-m)`, line-height 1.4, `var(--body-text-dark)` | Don't set font-size or color on body text unless you deliberately deviate. |
| Headings | Outfit, line-height 1.2, `var(--heading-dark)`, h1–h6 → `var(--h1)` … `var(--h6)` | Choose the right heading tag and the size follows. Don't set heading font-size to fix hierarchy. |
| Links | `var(--link-color)` inside text, rich text, lists, post content, and so on | Don't color inline links by hand. |
| Buttons | Full system driven by `--btn-*` tokens | Use the Bricks Button element's `style` / `size` / `outline` / `circle` settings (see [bnf/buttons.md](bnf/buttons.md)). |
| Site background | `var(--bg-body)` | Only set backgrounds on sections that differ. |
| Theme colors | primary = `--primary`, secondary = `--secondary`, light = `--white`, dark = `--black`, border = `--border-color--light` | Feeds the element `style` options (button, etc.). |

## Topic index

| Task | Read |
|------|------|
| Backgrounds, text and heading colors, palette, dark mode | [bnf/colors.md](bnf/colors.md) |
| Headings, body text sizes, fonts | [bnf/typography.md](bnf/typography.md) |
| Spacing, gaps, section rhythm, gutter | [bnf/spacing.md](bnf/spacing.md) |
| Content width, element width, grids | [bnf/layout.md](bnf/layout.md) |
| Borders, radius, box shadows | [bnf/borders.md](bnf/borders.md) |
| Buttons (native and custom) | [bnf/buttons.md](bnf/buttons.md) |
| Links, focus outline, transitions | [bnf/interaction.md](bnf/interaction.md) |
| Known issues in the default framework export | [bnf/known-issues.md](bnf/known-issues.md) |

## Quick do / don't

Do

- `_rowGap: var(--content-gap)`, `_padding: var(--space-l)`, `color: {"raw": "var(--body-text-white)"}`
- `_gridTemplateColumns: var(--grid-3)` with `var(--grid-1)` at `mobile_portrait`
- `_widthMax: var(--width-60)` to narrow a text block
- Bricks Button element with `style: "primary"`, `size: "md"`

Don't

- Hardcode `40px`, `#262626`, or `repeat(3, 1fr)` when a token exists
- Write `font-size: 16px` assuming 1rem = 16px (it's 10px here)
- Add padding to `section` elements or set container max-widths
- Set heading font sizes to fix hierarchy (change the tag instead)
- Use `--at-*` variables (Advanced Themer). They don't exist on BNF sites.

## Related docs

- [bricks.md](bricks.md): how to build in Bricks (structure, classes, JSON output)
- [css.md](css.md): custom CSS when settings and tokens are not enough
- [design.md](design.md): visual design quality
