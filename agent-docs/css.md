# CSS

Stylesheet conventions for Bricks projects. Apply during workflow step 7 (Development) and any styling review.

## When to use

Load this doc when a design needs styling beyond what Bricks settings and BNF tokens express in the builder UI.

## Order of preference

1. **Global styles**: the theme style already handles it. Do nothing (see [bnf.md](bnf.md)).
2. **Global class settings** in the Bricks UI, using BNF tokens (see [bricks.md](bricks.md)).
3. **Class custom CSS** (`_cssCustom` on the global class) for what the UI can't do: descendant selectors, `:focus-visible`, `::before` / `::after`, `:has()`, complex grid areas, reduced-motion queries.
4. **Element custom CSS** (`%root%`) only for true one-offs.
5. **Site-wide custom CSS** (Bricks → Settings → Custom code) only for genuine globals that belong in no class.

## Writing custom CSS

- **Vanilla CSS** only. No preprocessors, no Tailwind, no utility frameworks.
- **Tokens, not values.** Use BNF variables for every color, space, radius, width, shadow, and duration. Never hardcode a value a token covers. Remember **1rem = 10px**.
- **Literal selectors in class CSS:** `.acme-card:hover .acme-card__media { … }`. On an element, use `%root%`.
- **Native nesting** is fine and keeps related rules together:

```css
.acme-card {
  &:hover .acme-card__media { transform: scale(1.03); }
  &:focus-within { outline: var(--focus-outline-width) solid var(--focus-outline-color); }
}
```

- Keep specificity flat. Never use `!important` to beat Bricks. Put the rule in the right place instead (a class setting beats the theme style, and an element setting beats a class).
- Prefer **logical properties** (`padding-inline`, `margin-block`, `inline-size`, `max-inline-size`).
- Use `gap` for sibling spacing.
- Limit nesting to about three levels. Flatten anything deeper.

## Don't

- Write reset CSS. Bricks and the theme style handle it.
- Restyle section padding, container width, heading sizes, link colors, or buttons in CSS.
- Create utility classes (`.mt-20`, `.text-center`).
- Use `--at-*` (Advanced Themer) or ACSS variables.
- Leave unused classes and CSS behind.

## Related

- [bnf.md](bnf.md) and [bnf/](bnf/): tokens and global styles
- [bricks.md](bricks.md): classes, structure, JSON
- [design.md](design.md): spacing rhythm, color, motion rules
