# 4. Build Evidence (Modules 2–6 Alignment)

## Semantic HTML

- One logical `h1` per page; sequential heading levels after remediation.
- Landmarks: `header`, named `nav` (`aria-label="Primary"`), `main` (stable `id`), `footer`.
- `article` used for self-contained feature and card units.
- Lists used for real content (About page).
- Form: every control has a visible associated `<label>`; `required` + `aria-required`; `autocomplete` tokens; instructions via `aria-describedby`.
- Current page: visual class + `aria-current="page"`.
- Informative images have descriptive `alt`; decorative images not used.

## CSS Architecture & Responsive Layout

- `@layer` cascade with clear token → component progression.
- Design tokens for color, type, spacing, focus.
- Mobile-first, intrinsic grids, Flexbox where appropriate.
- Content reflows cleanly at narrow widths and 200% zoom.

## Media & Typography

- System font stack only (performance and CLS decision documented in CSS and HTML comments).
- Image dimensions + `aspect-ratio` for layout stability.
- Lazy loading on below-the-fold images; eager on hero.
- Full asset provenance recorded in source comments.

## Accessibility

- Skip link on every page.
- Visible focus indicators.
- Keyboard-operable controls; no traps.
- Reduced-motion and higher-contrast preference support.
- Form accessibility attributes complete for a static build.
- Detailed audit and remediation log: `docs/ACCESSIBILITY-REPORT.md`.

## Discoverability

- Unique, descriptive `<title>` on every page.
- `lang="en"`.
- Meaningful link text.
- Logical internal linking via persistent navigation and in-content CTAs.
- Semantic structure aids machine readability.

## File Organization

```
gameboy-capstone/
├── index.html, about.html, database.html, contact.html
├── style.css
├── assets/          (product photographs)
├── docs/            (this evidence package)
└── README.md
```
