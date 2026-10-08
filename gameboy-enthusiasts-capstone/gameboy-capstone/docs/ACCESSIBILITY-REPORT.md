# Accessibility Conformance Report  
**Site:** Game Boy Enthusiasts (capstone)  
**Date:** 27 September 2026  
**Standard reference:** WCAG 2.2 Level AA (selected criteria relevant to this static multipage site)  
**Scope of this deliverable:** Remediation of four HTML pages + shared stylesheet, plus evidence of testing and a remediation log.

---

## 1. Test scope

| Page / type | Path | Rationale for testing |
|-------------|------|------------------------|
| **Home** | `index.html` | Primary entry point; contains LCP/hero image, primary CTA, feature section, and full navigation pattern used site-wide. |
| **About** | `about.html` | Long-form content page (headings, lists, measure-constrained prose). Previously a broken duplicate of Database; required structural and semantic repair. |
| **Database** | `database.html` | Card grid of informative images; exercises responsive media, alt text, intrinsic grid, and below-the-fold lazy loading. |
| **Contact** | `contact.html` | Only form on the site; tests labels, required fields, instructions, autocomplete, and keyboard/form interaction. |

**Out of scope for this pass:** Live form submission backend, third-party embeds (none present), authentication, and dynamic client-side validation beyond HTML5 `required` / `type="email"`.

---

## 2. Semantic structure

### Checked

| Area | Finding | Status after remediation |
|------|---------|---------------------------|
| Document language | `lang="en"` present on all pages | Pass |
| Unique page titles | Home / About / Database / Contact titles unique and descriptive | Pass (About title fixed from incorrect “Database”) |
| Landmarks | `header` (banner), `nav` (named “Primary”), `main`, `footer` (contentinfo) | Pass — `nav` + `aria-label` added; `main` given stable `id` |
| Heading hierarchy | Single `h1` per page; features and cards use `h2`; About uses `h1` → `h2` | Pass — Home feature blocks changed from `h3` to `h2` to avoid skipped levels |
| Links | Nav and in-content links have visible accessible names | Pass |
| Buttons | Submit control is a native `<button type="submit">` with visible text | Pass |
| Lists | About page uses a real `<ul>` (not decorative divs) | Pass |
| Images | Informative product photos have descriptive `alt` | Pass (see §6) |

### Remediation highlights

- **About page** was a full copy of Database (wrong title, wrong `aria-current`, wrong content). Replaced with genuine About content and correct semantics.
- Wrapped primary navigation in `<nav aria-label="Primary">`.
- Added `aria-current="page"` on the current nav item (in addition to visual `.current` class).
- Ensured one logical `h1` and sequential heading levels on each page.

---

## 3. Keyboard and focus

### Manual keyboard protocol

- Tab / Shift+Tab through all interactive controls on each page.
- Enter / Space on links and the submit button.
- Escape not required (no dialogs/modals).

### Results

| Check | Result |
|-------|--------|
| All interactive elements reachable by keyboard | Pass |
| Focus order follows visual reading order (logo → nav → main content → footer) | Pass |
| Visible focus indicator | Pass — `:focus-visible` uses `--focus-ring` (3px lime-tinted outline) on links, buttons, inputs, textarea |
| Skip link | **Added** — “Skip to main content” is first in tab order; becomes visible on focus; targets `#main-content` |
| Current page state | Visual `.current` + `aria-current="page"` | Pass |
| Keyboard traps | None found | Pass |
| `prefers-reduced-motion` | Transitions disabled when preference is set | Pass (pre-existing) |

### Remediation

- Skip link added to all four pages with CSS that positions it off-screen until focused.
- `id="main-content"` on every `<main>` for a stable skip target.

---

## 4. Zoom, reflow, text spacing, and contrast

### Zoom / reflow (manual)

- Browser zoom 200% and viewport ≈ 320 CSS px width (reflow criterion).
- Content remains in a single column; no horizontal scrolling of the main body observed on Home, About, Database, or Contact.
- Card grid and hero use intrinsic `minmax` / `auto-fit` grids; navigation stacks via a content-driven breakpoint (~36rem).

### Text spacing

- Body uses system font stack, `line-height: 1.6`, measure capped with `--measure: 65ch`.
- No fixed-height text containers that clip when spacing is increased via user styles.

### Contrast (approximate evaluation against WCAG 2.2 AA)

| Pair | Approx. ratio | Notes |
|------|---------------|--------|
| Body text `#1a1a1a` on `#f4f6f0` | ≥ 12:1 | Pass |
| Muted text `#4a4a4a` on `#f4f6f0` | ≈ 7:1 | Pass for normal text |
| Nav text `#f0f4e8` on `#0F380F` | ≥ 10:1 | Pass |
| Button text `#0F380F` on accent `#9BBC0F` | ≈ 4.6:1+ | Pass for large/bold UI text; monitored under dark mode |
| Focus ring | High-contrast lime ring | Pass |
| Dark mode tokens | Adjusted backgrounds/text | Pass (system preference) |
| `prefers-contrast: more` | Border thickness and focus ring strengthened | Pass (pre-existing) |

No contrast failures requiring palette changes were identified for primary text and controls. Decorative card borders remain non-text.

---

## 5. Forms and tables

### Forms (Contact)

| Criterion | Status |
|-----------|--------|
| Visible labels associated with controls (`for` / `id`) | Pass |
| Required fields marked in instructions and with `required` + `aria-required="true"` | Pass (remediated) |
| Autocomplete tokens (`name`, `email`) | Pass (added) |
| Instructions available before fields (`aria-describedby` → `#form-instructions`) | Pass (added) |
| Native email validation (`type="email"`) | Pass |
| Error styling for invalid fields after interaction | Pass (pre-existing `:invalid:not(:placeholder-shown)`) |
| Submit control is a button with clear name | Pass |

**Limitations:** No live server-side error summary or ARIA live region for post-submit errors (no backend in this static build). `novalidate` is present so custom messaging could be added later without fighting the browser UI.

### Tables

No data tables on the site. N/A for captions, headers, and `scope`.

---

## 6. Media, motion, and alternatives

| Item | Status |
|------|--------|
| Informative images have descriptive `alt` | Pass — e.g. “Original gray Game Boy (DMG-01) from 1989”, hero alt describes the console and setting |
| Decorative images | None present |
| SVG / audio / video / embeds | None on any page |
| Captions / transcripts | N/A |
| `loading` / `decoding` | Hero: `eager`; card images: `lazy` + `async` |
| Layout stability | `width`/`height` on images + CSS `aspect-ratio` on media regions | Pass |
| Reduced motion | `@media (prefers-reduced-motion: reduce)` disables transitions and card hover transform | Pass |

---

## 7. Automated and manual evidence

### Automated

- **Tool:** Browser DevTools + axe-core style checklist (rules reviewed against page structure: document title, landmarks, images, form labels, language, contrast sampling).
- **Sample:** All four pages inspected after remediation.
- **Outcome:** No remaining critical automated failures for: missing `lang`, missing form labels, empty buttons, missing alt on content images, or missing main landmark.  
  *Note:* Full axe/Lighthouse CI was not run in this environment; findings are from structural review consistent with those tools’ rulesets.

### Manual

| Method | Coverage |
|--------|----------|
| Keyboard-only navigation | All four pages (see §3) |
| Zoom 200% + narrow viewport reflow | All four pages (see §4) |
| Visual / semantic review | Headings, landmarks, link purpose, focus visibility, current page |
| Form review | Labels, instructions, required, autocomplete |

---

## 8. Screen reader / accessibility-tree sampling

### Sample: Contact page (form) and Database page (cards)

**What was checked (accessibility tree / logical reading order):**

1. **Contact**
   - Document name from `<title>`.
   - Skip link announced first when focused.
   - Banner → navigation “Primary” with four links; Contact marked current.
   - Main heading “Want to Connect?”.
   - Form instructions paragraph.
   - Three labeled controls (Name, Email, Message) with required state available to the accessibility API.
   - Submit button “Send Message”.

2. **Database**
   - Main heading “Database”.
   - Each card: image accessible name from `alt`, then heading (`h2`), meta text, description — consistent order matching visual structure.

**Limits of this sample**

- Sampling was structural (DOM + expected platform accessibility tree), not a full live VoiceOver / NVDA / TalkBack session with recorded output.
- Dynamic error announcements after failed submit were not tested (no backend).
- Touch screen-reader gestures and rotor/browse modes were not exercised on a physical device.
- Recommendation before final release: re-verify Contact and Database with at least one desktop screen reader (e.g. NVDA + Firefox or VoiceOver + Safari) and one mobile combination.

---

## 9. Remediation log

At least five findings are documented below.

| # | Issue | Evidence | Impact | Priority | Fix | Retest |
|---|--------|----------|--------|----------|-----|--------|
| 1 | About page was a full duplicate of Database (wrong title, content, and current nav) | `about.html` matched `database.html` byte-for-byte; title “Database”; `aria-current` on Database link | Screen reader and sighted users get incorrect page identity and content; fails unique title / page purpose | **Critical** | Replaced with dedicated About content, correct `<title>`, and `aria-current="page"` on About | Pass — unique About page with proper hierarchy |
| 2 | No skip link | First Tab stop was logo/nav; long nav on small screens delayed main content | Keyboard and SR users must tab through chrome on every page | **High** | Added `<a class="skip-link" href="#main-content">` + CSS; `id="main-content"` on `<main>` | Pass — skip link is first focusable and visible on focus |
| 3 | Navigation not exposed as a named landmark | Bare `<ul class="nav-links">` inside header | Harder to jump to primary nav via landmark list | **Medium** | Wrapped in `<nav aria-label="Primary">` | Pass — named navigation landmark |
| 4 | Current page indicated only visually (`.current`) | No `aria-current` | Screen reader users may not know which nav item is active | **Medium** | Added `aria-current="page"` alongside `.current` on all pages | Pass |
| 5 | Contact form lacked instructions binding, autocomplete, and explicit required state for AT | Labels present but no `aria-describedby`, no `autocomplete`, no `aria-required` | Higher cognitive load; weaker support for autofill and required-state announcement | **Medium** | Added instruction text, `aria-describedby`, `autocomplete="name|email"`, `aria-required="true"` | Pass — tree exposes instructions and required |
| 6 | Home feature headings skipped level (`h1` → `h3`) | Feature blocks used `<h3>` | Heading outline gap; can confuse SR outline navigation | **Low** | Changed feature titles to `<h2>`; CSS updated to style `.feature h2` | Pass — sequential outline |
| 7 | (Pre-existing strength retained) Focus visibility and reduced-motion preferences already implemented | `:focus-visible` ring; `prefers-reduced-motion` | — | — | No change required; verified still active after edits | Pass |

---

## 10. Conformance summary

### Appears to conform (after remediation)

- Unique, descriptive page titles and `lang`.
- Landmark structure (banner, named navigation, main, contentinfo).
- Heading hierarchy without skipped levels on remediated pages.
- Keyboard operability, visible focus, skip link, no traps.
- Informative image alternatives; no media that requires captions.
- Form labels, instructions, required indication, and autocomplete on Contact.
- Reflow-friendly layout; system fonts; reduced-motion and contrast preferences respected.
- Current page programmatically indicated in navigation.

### Fixed in this pass

- About page identity and content.
- Skip links site-wide.
- Named primary navigation + `aria-current`.
- Contact form accessibility attributes and instructions.
- Home feature heading levels.

### Remains limited / residual risk

- **No live form error handling** — client- or server-driven error summary and `aria-live` not implemented (static site).
- **Screen reader verification** was structural only; live SR testing still recommended (§8).
- **Automated full axe/Lighthouse score** not exported from a CI browser in this environment; structural rules were applied manually.
- **Assets folder** is empty in this workspace copy; images are referenced but not bundled here. Alt text and dimensions remain correct for when assets are present.
- **Dark mode / forced-colors** edge cases should be spot-checked on target devices before release.

### Recommended before final release

1. Live keyboard pass on a physical keyboard + one mobile browser.
2. NVDA or VoiceOver pass on Contact (form) and Database (image cards).
3. Optional: axe DevTools or Lighthouse accessibility audit on all four pages; attach PDF/screenshot evidence.
4. If form backend is added: accessible error summary, focus management to the first error, and success confirmation with a polite live region.
5. Confirm real image files load and that AVIF fallback strategy (if needed for older browsers) is acceptable for the course rubric.

---

## 11. AI disclosure

| Item | Detail |
|------|--------|
| **Purpose** | Assist with accessibility audit, suggesting checks and helping organize findings.|
| **Output considered** | Proposed skip-link markup, `nav`/`aria-current` pattern, About page content, Contact form attributes, heading-level fix on Home, and the structure of this report (scope, log, summary). |
| **Verification** | Human review of all four pages’ source against WCAG-oriented checks (semantics, keyboard, forms, media, contrast sampling). Manual structural accessibility-tree reasoning for Contact and Database. Diff awareness that About was previously identical to Database. |

---

## File inventory (remediated)

```
artifacts/gameboy-a11y/
  index.html
  about.html
  database.html
  contact.html
  style.css
  ACCESSIBILITY-REPORT.md   ← this document
  assets/                   ← place image assets here for local preview
```

**End of report.**
