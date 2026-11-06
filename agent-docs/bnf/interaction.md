# Links, focus and motion

Load when styling links, hover states, focus states, or transitions. Index: [bnf.md](../bnf.md).

## Links

- `--link-color` (`--primary`), `--link-color--hover` and `--link-color--active` (`--primary-d-2`)
- The theme style already colors links inside Text, Rich Text, Basic Text, lists, post content, accordions, tabs, and the Text Link element. Don't color those by hand.
- Links in custom components (cards, nav) use these tokens in the component's class.
- Inline links in body copy must look different from the surrounding text by more than color alone (an underline is the safe default).

## Focus

- Tokens: `--focus-outline-color` (`--neutral`), `--focus-outline-width` (3px), `--focus-outline-offset` (3px)
- Never remove focus outlines. Custom interactive components use:

```css
.my-card__link:focus-visible {
  outline: var(--focus-outline-width) solid var(--focus-outline-color);
  outline-offset: var(--focus-outline-offset);
}
```

Check the theme style's focus outline setting too, because the default export points at variables that don't exist (see [known-issues.md](known-issues.md)).

## Transitions

- Durations: `--duration--fast` (0.5s), `--duration--medium` (0.8s), `--duration--slow` (1.5s), and `--duration` (= fast)
- These are long for UI feedback. For hover and focus on buttons, links, and cards, aim for about 150–250ms. Use the tokens for reveal or section animations, not for hover states. If a project wants faster UI motion, add a project token such as `--duration--ui: 0.2s` to the variables, and don't hardcode it.
- Animate `transform` and `opacity` only, never layout properties. Use exponential ease-out curves, not bounce (see [design.md](../design.md)).
- Respect `prefers-reduced-motion` for anything larger than a color change.
