# 3. CSS Architecture, Responsive Layout, Media & Typography

## Cascade Strategy (`@layer`)

The stylesheet uses explicit cascade layers in this order:

1. `reset`
2. `tokens`
3. `base`
4. `layout`
5. `components`
6. `utilities`
7. `states`
8. `overrides`
9. `print`

This keeps specificity predictable and makes the architecture self-documenting.

## Design Tokens (`:root`)

- **Color**: Game Boy palette (`#9BBC0F`, `#8BAC0F`, `#306230`, `#0F380F`) plus neutral background/text tokens for readability.
- **Focus**: High-visibility lime-tinted ring.
- **Typography scale**: Modular steps from small meta text to display headings.
- **Spacing, measure, radii, transitions**: Consistent custom properties.
- **Dark / contrast preferences**: Tokens and media queries support `prefers-color-scheme` and `prefers-contrast: more`.

## Typography (Parts 6 & 7 alignment)

- **Stack**: System-ui first → zero network requests, no FOIT/FOUT, no font-related CLS.
- **Measure**: Capped with a readable `ch`-based max width on prose containers.
- **Line-height**: Comfortable body leading (~1.6).
- **No `@font-face`**: Intentional production choice for performance and reliability.

## Media & Layout Stability

- Informative images carry descriptive `alt`, explicit `width`/`height`, and appropriate `loading`/`decoding`.
- CSS `aspect-ratio` on media regions reduces Cumulative Layout Shift.
- Hero image loads `eager`; card images load `lazy`.
- No SVG/audio/video/embeds requiring captions or transcripts.

## Responsive Techniques

- Mobile-first base styles.
- CSS Grid (`auto-fit` / `minmax`) for card and feature grids.
- Flexbox for header and simple alignment.
- Content-driven stacking rather than numerous hard breakpoints.
- Navigation reflows from horizontal to stacked as space requires.

## Accessibility-Related CSS

- Skip-link styles (visible on focus only).
- `:focus-visible` ring using a design token.
- `@media (prefers-reduced-motion: reduce)` disables non-essential transitions/transforms.
- `@media (prefers-contrast: more)` strengthens borders and focus treatment.
- Print layer hides chrome and preserves content readability.
