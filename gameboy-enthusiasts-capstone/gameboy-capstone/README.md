# Game Boy Enthusiasts – Capstone Website

**Production HTML/CSS multipage site** for a fictional community dedicated to Nintendo Game Boy hardware collectors and enthusiasts.

This package is the final submission for the HTML/CSS capstone. It includes the live production pages, organized repository, planning through release evidence, technical defense, and AI disclosure.

## Live / Preview

Open `index.html` in any modern browser. No build step or server is required.

Recommended public hosts: GitHub Pages, Netlify, or Cloudflare Pages (drag-and-drop the folder or connect the repository).

## Site Map

| Page | File | Purpose |
|------|------|---------|
| Home | `index.html` | Hero, value proposition, feature highlights, primary CTA |
| About | `about.html` | Mission, what users will find, educational use notes |
| Database | `database.html` | Card grid of Game Boy family hardware with images + metadata |
| Contact | `contact.html` | Accessible contact form (labels, required, autocomplete, instructions) |

Shared stylesheet: `style.css`  
Assets: `assets/` (product photographs with provenance documented in HTML comments)

## Design Goals

- **Audience**: Collectors, players, and newcomers interested in Game Boy hardware variants.
- **Primary tasks**: Learn about the community, browse hardware variants, identify models, send a message.
- **Constraints**: Core experience works without JavaScript. System fonts only. Strong accessibility focus (WCAG 2.2 AA-oriented).

## Key Technical Features

- Semantic HTML5 landmarks (`header`, `nav` with accessible name, `main`, `footer`)
- Skip link + visible `:focus-visible` ring
- `aria-current="page"` on current navigation item
- Mobile-first responsive layout (CSS Grid + Flexbox)
- CSS `@layer` cascade architecture with design tokens
- System font stack (zero network font cost, no FOIT/FOUT/CLS from fonts)
- `prefers-reduced-motion` and `prefers-contrast: more` support
- Descriptive `alt` text, `width`/`height` + `loading`/`decoding` on images
- Print stylesheet
- Accessible form with associated labels, instructions, `aria-required`, autocomplete

## Evidence Package

All planning, build, and release evidence lives in `docs/`:

1. `01-planning.md` – planning package & content architecture
2. `02-wireframes-acceptance.md` – responsive strategy & acceptance criteria
3. `03-css-architecture.md` – CSS layers, tokens, media/typography
4. `04-build-evidence.md` – Modules 2–6 alignment
5. `05-release-evidence.md` – validation, links, responsive, a11y, performance, limitations
6. `06-technical-defense.md` – concise defense of the work
7. `07-ai-disclosure.md` – AI use, acceptance/rejection, verification
8. `ACCESSIBILITY-REPORT.md` – detailed WCAG-oriented audit & remediation log (from the Accessibility Conformance build)

## Browser Support

Modern evergreen browsers (Chrome, Firefox, Safari, Edge). Uses standard CSS Grid, Flexbox, custom properties, `@layer`, `:focus-visible`. No polyfills required.

## Disclaimer

Fictional community site created for educational purposes. Product photographs are used under their respective licenses for educational/community demonstration; see HTML comments for provenance.
