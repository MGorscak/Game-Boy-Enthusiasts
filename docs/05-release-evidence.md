# 5. Release Evidence

## Validation

- HTML reviewed against HTML5 practices: doctype, charset, viewport, `lang`, unique titles, semantic landmarks, form associations.
- CSS uses standard modern features (`@layer`, custom properties, Grid, Flexbox, `:focus-visible`). No vendor-prefix dependency for core layout.
- Core user journeys work with JavaScript disabled.

## Broken-Link Checks

| From | Target | Status |
|------|--------|--------|
| All pages | index.html, about.html, database.html, contact.html | OK |
| Home CTA | database.html | OK |
| About CTA | database.html | OK |
| Nav + logo | All primary pages | OK |
| Form action | `/submit-form-endpoint` (demo; no backend) | Presentational only |

No internal 404s within the package.

## Responsive Regression Checks

Manually reviewed at approximate widths:

- ~320 px (narrow mobile)
- ~375 px (common phone)
- ~768 px (tablet)
- ≥1024 px (desktop)

Observed:

- Navigation stacks / expands appropriately.
- Hero and card grids reflow without horizontal body overflow.
- Form remains usable and readable.
- Focus and skip link remain operable.

## Accessibility Spot Checks

Covered in depth in `docs/ACCESSIBILITY-REPORT.md`. Summary:

- Keyboard order and visible focus: Pass
- Skip link: Pass
- Landmarks + heading hierarchy: Pass (after remediation)
- Form labels / required / instructions / autocomplete: Pass
- Image alternatives: Pass
- Reduced motion & contrast preferences: Pass
- Residual risk: live screen-reader session and full axe/Lighthouse export still recommended before a public production launch

## Performance Diagnostic (Conceptual)

- Single stylesheet; no render-blocking scripts.
- System fonts only → zero font network cost and no font-related CLS.
- Image dimensions + aspect-ratio reduce layout shift.
- Lazy loading on non-hero images.
- Expected strong Performance / Accessibility / Best-Practices scores for a static multipage site of this size when assets are present.

## Compatibility Notes

- Modern evergreen browsers.
- Graceful degradation for older environments that lack `@layer` or `backdrop`-style features (core layout still functions via standard Grid/Flexbox/custom properties).
- No IE11 support claimed.

## Known Limitations

1. Contact form is presentational; no backend or live error-summary / `aria-live` handling.
2. Full automated axe/Lighthouse CI export was not generated in the build environment (structural rules applied manually).
3. Live screen-reader verification (NVDA/VoiceOver) remains a recommended final step.
4. Some image licenses are educational/community use; confirm suitability if the site is published beyond coursework.
5. No sitemap.xml / robots.txt (can be added for production hosting).
6. Dark-mode and forced-colors edge cases should be spot-checked on target devices.
