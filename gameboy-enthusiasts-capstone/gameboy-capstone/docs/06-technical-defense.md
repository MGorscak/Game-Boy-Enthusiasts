# 6. Technical Defense

## What I Built

A four-page static website for a fictional Game Boy hardware community. The site uses semantic HTML5 and a single, layered modern CSS stylesheet. Core journeys—understanding the community, browsing hardware variants, and contacting the site—work without JavaScript.

## Why It Fits the Audience and Task

Collectors and newcomers need clear model identification, readable descriptions, and a low-friction way to reach the community. The Database page presents hardware as scannable cards with descriptive images and metadata. The Contact form is fully labelled and instruction-bound. Visual language draws on the classic Game Boy palette while maintaining strong contrast and readability.

## What I Tested

- Semantic structure, landmarks, and heading hierarchy
- Keyboard navigation and skip-link behavior
- Form labelling, required state, autocomplete, and instructions
- Image alternatives and loading attributes
- Reflow at narrow widths and 200% zoom
- Internal link integrity
- Focus visibility, reduced-motion, and contrast preferences
- Detailed accessibility audit documented in `ACCESSIBILITY-REPORT.md`

## What I Fixed

Documented remediation log (high-level):

1. About page had been a duplicate of Database → replaced with correct content, title, and `aria-current`.
2. Missing skip link → added site-wide with stable main target.
3. Navigation lacked a named landmark → wrapped in `<nav aria-label="Primary">`.
4. Current page indicated only visually → added `aria-current="page"`.
5. Contact form missing instructions binding, autocomplete, and explicit required state for AT → added.
6. Home feature headings skipped a level → corrected to sequential `h2`.

## What Remains Limited

- No live form processing or accessible error summary.
- Automated full axe/Lighthouse scores not exported from CI in this environment.
- Live screen-reader pass still recommended before any public release.
- Image assets are educational/community photographs; licensing notes are in source comments.

The delivered site meets the production requirements for semantic HTML, modern CSS architecture, responsive layout, accessibility foundations, and a complete evidence package from planning through release.
