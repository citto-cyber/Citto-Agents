# Bricks Builder

How to build in Bricks Builder (2.2+) on these projects. Docs: https://academy.bricksbuilder.io

## When to use

Load this doc during workflow step 7 (Development) and for any work on Bricks layouts, templates, global classes, or JSON. Always load [bnf.md](bnf.md) with it, because styling rules live there.

If your AI tool has a dedicated Bricks JSON skill, use it alongside this doc for exact setting keys and value shapes. This doc's project conventions take priority.

## Stack

- **Bricks Builder 2.2+**: page builder and theme
- **Bricks Native Framework (BNF)**: design tokens in the Bricks Style Manager (see [bnf.md](bnf.md))
- No ACSS, Core Framework, or Advanced Themer. Don't use their classes or `--at-*` variables.

## Page structure

```
section            (tag: section | header | footer; root only, never nested)
└── container      (max width is global; one per section)
    ├── block      (intro: heading + text + buttons)
    └── block      (grid / content)
        └── block  (item)
```

- **Section** gets its padding from the theme style. Use the `tag` setting for semantics (`header`, `footer`, `main` regions on templates).
- **Container**: one per section. Its width is global, so don't set it.
- **Block** is the default wrapper (flex column by default). Use `tag` for semantics: `ul`/`li` for lists, `article` for cards, `nav`, `figure`, `aside`.
- **Div** only when you need an unstyled, non-flex wrapper.
- **Label every structural element** (`label` key, for example "Hero", "Intro", "Feature grid"). The framework template labels everything, and the structure panel should read like an outline.
- Content elements: `heading` (with `tag`), `text-basic` for a single paragraph or span, `text` for rich text, `button`, `image`, `icon`, `svg`, `video`, `text-link`.
- Prefer nestable elements: `accordion-nested`, `tabs-nested`, `nav-nested`, `slider-nested`, `dropdown`, `offcanvas`.

## Global classes and BEM

- Style with **global classes**, not ID-level element settings. Element settings are for genuine one-offs (one image's `object-position`, for instance).
- **BEM naming** with a short project prefix: `{prefix}-{block}`, `{prefix}-{block}__{element}`. Example: `acme-hero`, `acme-hero__intro`, `acme-hero__media`. The framework itself uses `bnf-` and `bm-`. Don't reuse those prefixes for project classes.
- **Every structural element gets a class**, even an empty one. It documents the layout and makes later styling easy.
- **Modifiers**: Bricks has no data-attribute styling in its UI. Use BEM modifier classes (`acme-card--featured`) stacked on the base class. Keep them few.
- Class settings use the same keys as element settings, including breakpoint and pseudo suffixes (`_padding:mobile_portrait`, `_background:hover`).
- Class custom CSS (`_cssCustom` on a class) uses the **literal class selector**: `.acme-cta .acme-cta__heading { … }`. On an element (not a class), use `%root%`.
- No utility classes. BNF ships none, by design.

## Responsive

- Breakpoints are desktop-first: the bare key = desktop, `tablet_portrait` ≤991px, `mobile_landscape` ≤767px, `mobile_portrait` ≤478px.
- Breakpoints change **layout**: grid columns, flex direction, order, visibility. Spacing and type are fluid tokens and rarely need breakpoint overrides.
- Every layout must work at 360px wide with no horizontal scroll.

## Templates

- Header, footer, single, archive, search, 404, popup, and section templates are Bricks templates with conditions. Don't build the header or footer into pages.
- Repeated page parts (CTA banner, logo strip) become **section templates** or **components**, not copy-pasted sections.
- **Components** (Bricks 1.12+) for repeated UI with editable content (card, testimonial, CTA). Expose text, link, and image as component properties.

## Dynamic data and query loops

- Use dynamic tags (`{post_title}`, `{featured_image}`, `{acf_field_name}`, `{woo_*}`) instead of hardcoding content that lives in WordPress.
- Lists of posts, products, team members, and so on are **query loops** (`hasLoop: true` + `query`) on a block, with the card markup inside. Don't use the legacy Posts element.
- Confirm field names with the user before writing `{acf_*}` or meta tags. Never guess them.

## Delivering Bricks JSON

When asked for a section, page, or template, deliver a **`.json` file** the user pastes into the builder (Ctrl/Cmd+V in the structure panel) or imports under Bricks → Templates.

Clipboard format:

```json
{
  "content": [ /* flat array of elements */ ],
  "source": "bricksCopiedElements",
  "sourceUrl": "https://example.com",
  "version": "2.2",
  "globalClasses": [ /* full objects for every class referenced */ ],
  "globalElements": []
}
```

Rules:

1. **Flat tree.** Each element has `id` (6 random lowercase letters or digits, unique), `name`, `parent` (`0` for root), `children` (ordered ids), and `settings` (an object, never `[]`).
2. **Classes ride along.** Every id in `_cssGlobalClasses` has a full object (`id`, `name`, `settings`) in `globalClasses`. On paste, Bricks merges classes by name, so use stable, prefixed names.
3. **Colors are objects**: `{"raw": "var(--primary)"}`. Typography keys are CSS property names (`"font-size"`, not `fontSize`).
4. **Units are strings** (`"100%"`, `"2.4rem"`). A bare number gets `px`. Remember **1rem = 10px**.
5. **Tokens only.** Every spacing, color, radius, width, and grid value is a BNF variable (see [bnf.md](bnf.md)).
6. **Don't restyle globals.** No section padding, container width, heading sizes, or button styling.
7. **Semantic HTML**: one `h1` per page, no skipped heading levels, meaningful `tag` settings.
8. **Don't invent setting keys.** Unknown keys are silently ignored.
9. **Images**: use absolute URLs or placeholders (never attachment ids from another site), with real `alt` text.

Before delivering, check: the JSON parses; every parent/children reference resolves; ids are unique; every class referenced is included; breakpoint keys are valid; and the copy matches the approved copy deck.

## Related docs

- [bnf.md](bnf.md) and [bnf/](bnf/): design tokens and global styles
- [html.md](html.md): semantics and accessibility
- [css.md](css.md): when and how to write custom CSS
- [design.md](design.md): visual quality bar
