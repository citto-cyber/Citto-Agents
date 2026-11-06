# Buttons

Load when adding buttons or button-like links. Index: [bnf.md](../bnf.md).

## Use the native Bricks Button element

All button styling comes from the theme style, driven by `--btn-*` tokens. Set only these element settings:

| Setting | Values | Notes |
|---------|--------|-------|
| `style` | `primary`, `secondary`, `light`, `dark` | `light` on dark backgrounds, `dark` on light backgrounds when you need neutral |
| `size` | `sm`, `md`, `lg`, `xl` | Omit for the default (medium padding, large text) |
| `outline` | `true` | Transparent background with a colored border |
| `circle` | `true` | Pill-shaped |

```json
{ "id": "btn001", "name": "button", "parent": "cta001", "children": [],
  "settings": { "text": "Book a call", "style": "primary", "size": "md",
    "link": { "type": "external", "url": "/contact" } } }
```

Don't add background, color, padding, border, or radius to a Button element. If a button needs to look different, change the tokens (site-wide) or build a custom button (below).

## Button pairs

Primary plus secondary action side by side: wrap them in a block with the `cta-combo` pattern (flex, centered, `column-gap: calc(var(--content-gap) / 2)`, stacked on `mobile_portrait`). The secondary action is usually `outline: true` with the same `style`.

## Custom buttons (rare)

When a design needs a button the native styles can't express, build a BEM class that **uses the button tokens**, so it still follows the system:

- Shape: `--btn-border-radius`, `--btn-border-width`, `--btn-shadow`, `--btn-shadow-hover`, `--btn-transition`
- Outline: `--btn-outline-border-radius`, `--btn-outline-border-width`, `--btn-outline-shadow`, `--btn-outline-shadow--hover`
- Color (for primary, secondary, light, dark): `--btn-{color}-color`, `--btn-{color}-background`, `--btn-{color}-border-color`, each with a `--hover` variant
- Outline color: `--btn-{color}-outline-color`, `--btn-{color}-outline-background`, `--btn-{color}-outline-border-color`, each with `--hover`
- Size (small, medium, large, x-large): `--btn-{size}-font-size`, `--btn-{size}-block`, `--btn-{size}-inline`

Example: `padding: var(--btn-medium-block) var(--btn-medium-inline);`

## Copy

Button labels are verb plus object ("Book a call", "Get the guide"). Never "Click here", "Submit", or a bare "Learn more" (see [copywriting.md](../copywriting.md)).
