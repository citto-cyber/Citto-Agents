# Known issues in the default BNF export

Found while auditing the framework exports (variables, palette, theme style, style manager; Bricks 2.2 format, March–April 2026). Fix these once per site in the Bricks editor. Until a site is confirmed fixed, don't copy these values into new work. Index: [bnf.md](../bnf.md).

| # | Where | Problem | Effect | Fix |
|---|-------|---------|--------|-----|
| 1 | Theme style → Typography → Focus outline | `var(--at-focus-outline-width) solid var(--at-focus-outline-color)` uses Advanced Themer variables that don't exist | **No visible keyboard focus outline** (accessibility failure) | `var(--focus-outline-width) solid var(--focus-outline-color)` |
| 2 | Variable `--btn-transition` | `all var(--at-duration--fast) ease` uses a missing variable | Buttons don't animate on hover | `all var(--duration--fast) ease`. Better: a faster UI token (see [interaction.md](interaction.md)) and specific properties instead of `all` |
| 3 | Theme style → Button → Size large typography | `color: var(--btn-large-font-size)` puts a font size in the color field | Invalid; ignored by browsers | Clear that color field |
| 4 | `--space-4xs`, `--space-3xs`, `--text-2xs`, `--text-xs`, `--h6` | `clamp()` min is larger than max | Fixed size; doesn't scale | Regenerate the scale or swap min and max |
| 5 | `--h6` | About 12px, smaller than body text (16–18px) | An h6 reads smaller than a paragraph | Avoid h6, or raise it to at least `--text-m` |
| 6 | `--width-*` variables | Values end in a stray `;` | Usually harmless (empty declaration), but can break in strict tooling | Remove the trailing `;` |
| 7 | Theme style → Button radius | Declared with `!important` | Can't be overridden normally | Leave it, but know why a radius override "doesn't work" |

When a site is cleaned up, note it in the project's `discovery/brief.md` (or a site notes file) so agents know which fixes are live.
