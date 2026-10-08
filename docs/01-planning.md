# 1. Planning Package & Content Architecture

## Project Brief

**Site name:** Game Boy Enthusiasts  
**Type:** Informational multipage community website  
**Approved page scope:**
1. Home – hero, community features, CTA to Database
2. About – mission, what users will find, educational notes
3. Database – grid of hardware variants (informative images + metadata)
4. Contact – accessible contact form

**Out of scope:** Backend form processing, user accounts, e-commerce, JavaScript-dependent core interactions, CMS.

## Audience & Primary Tasks

| Segment | Goals |
|---------|-------|
| Collectors | Identify variants, share knowledge, find model codes/years |
| Newcomers | Understand the Game Boy family and community purpose |
| Enthusiasts | Contact the community, browse special editions |

**Success criteria:** A first-time visitor can answer “What is this site?”, “What models exist?”, and “How do I get in touch?” within two clicks.

## Information Architecture

```
Home
├── About
├── Database  (primary content destination)
└── Contact
```

Global header navigation + consistent footer on every page. Skip link jumps to `#main-content`.

## Content Architecture (page inventory)

### Home
- Skip link
- Header / primary nav (current page marked)
- Hero grid (informative image + H1 + lead + CTA)
- Feature grid (Collectors / Variants / Community) as `article`s
- Footer

### About
- Mission statement
- “What you’ll find” list
- Educational-use note
- CTA to Database

### Database
- Intro paragraph
- Card grid of hardware entries (`article.card`)
  - Each card: image (descriptive `alt`, dimensions, lazy/async), H2 title, meta line, short description

### Contact
- Heading + intro
- Form instructions (bound via `aria-describedby`)
- Name / Email / Message fields (labels, required, autocomplete, aria-required)
- Native submit button

## Asset Provenance (summary)

All images live in `/assets/`. Full source/license notes are embedded as HTML comments on Home and Database pages. System fonts only — no web-font requests.

## Constraints

- HTML + CSS only for core requirements.
- No JavaScript required for navigation, layout, or form presentation.
- Accessibility treated as a first-class requirement (see ACCESSIBILITY-REPORT.md).
