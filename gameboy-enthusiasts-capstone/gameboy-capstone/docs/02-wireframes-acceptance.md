# 2. Responsive Strategy, Annotations & Acceptance Criteria

## Breakpoint / Layout Strategy (Mobile-first)

| Range | Layout behavior |
|-------|-----------------|
| Base (< ~36rem) | Single column; navigation stacks; cards stack; hero stacks |
| ≥ ~36rem | Navigation becomes horizontal; grids begin multi-column via `auto-fit` / `minmax` |
| Wider viewports | Hero becomes side-by-side grid; card grid expands (2–3+ columns); measure-constrained prose remains readable |

Layout is content-driven rather than a rigid set of named breakpoints. Intrinsic grids (`minmax`, `auto-fit`) and Flexbox handle most reflow.

## Annotated Layout Notes

- **Header**: Dark Game-Boy-green bar; logo left, nav right (or stacked). Current page uses visual class + `aria-current="page"`.
- **Skip link**: First in tab order; off-screen until focused.
- **Hero**: Media + content grid; image has explicit width/height and `loading="eager"`.
- **Feature / Card grids**: CSS Grid with consistent gap; each item is an `article`.
- **Form**: Narrow container; labels above controls; instructions bound to fields.
- **Footer**: Simple copyright bar.

## Acceptance Criteria (Release Checklist)

- [x] All four pages render and function without JavaScript.
- [x] Primary navigation present and consistent; current page indicated visually and programmatically.
- [x] Skip link present on every page and targets `#main-content`.
- [x] Visible focus indicators on interactive elements (`:focus-visible`).
- [x] Semantic landmarks and sequential heading hierarchy.
- [x] Form fields have associated labels, required indication, and autocomplete where appropriate.
- [x] Informative images have descriptive `alt` text and intrinsic dimensions.
- [x] Layout reflows without horizontal body scroll at ~320 CSS px and at 200% zoom.
- [x] No broken internal links.
- [x] Unique, descriptive `<title>` on every page; `lang="en"` present.
- [x] `prefers-reduced-motion` respected; print stylesheet present.
- [x] Asset provenance documented in source comments.
