# HTML

Markup conventions for Bricks projects. Apply during workflow step 7 (Development) and any markup review.

## When to use

Load this doc when building or reviewing pages, sections, components, and templates. In Bricks, "markup" means the element tree plus each element's `tag` setting (see [bricks.md](bricks.md)).

## Semantic structure

- Use semantic elements first: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`, `figure`, `figcaption`, `button`, `ul`/`ol`/`li`. In Bricks, set them through the `tag` setting on Section, Block, and Div elements.
- Reach for a plain `div` only when no semantic element fits.
- One `h1` per page. Do not skip heading levels.

## Accessibility

- Every interactive control needs an accessible name (visible label, `aria-label`, or `aria-labelledby`).
- Every meaningful image needs descriptive `alt` text. Decorative images use `alt=""`.
- Use native elements for their built-in behavior (`button` for actions, `a` for navigation, `input` + `label` for forms).
- Add ARIA only when native semantics are insufficient. Do not override native roles.

## Class and attribute hooks

- Give every structural element a **BEM global class** with the project prefix (`acme-card`, `acme-card__title`). See [bricks.md](bricks.md).
- Express variations with a small number of **BEM modifier classes** (`acme-card--featured`), because Bricks styles classes, not attributes.
- Use **custom attributes** (`_attributes`) for state and behavior (`aria-*`, `data-state="open"`), not for styling variations.
- Don't use one hook for both JavaScript and styling. One hook, one purpose.

## Content patterns

- Links use descriptive text. Avoid "click here" or "read more" without context.
- Lists contain only `li` (or script-supporting) children. Tables are for tabular data, not layout.
- Forms group related fields with `fieldset`/`legend` when it aids comprehension.
