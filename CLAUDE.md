# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Overview

Personal portfolio website for Atakan Onay (Computer Engineer). It is a **single static
`index.html`** file — there is no build step, framework, package manager, or backend.
Styling is done with Tailwind CSS (via CDN) and icons via Font Awesome (CDN). The site is
deployed as a static page (custom domain `atakanonay.dev`).

## Structure

Everything lives in `index.html`:

- **`<head>`** — meta/OG tags, Google Fonts, Tailwind CDN + inline `tailwind.config`, and a
  `<style>` block with custom animations (`blink`, `fade-in`, `project-card`, `glassmorphism`).
- **`<body>`** — sections in order: Navbar, Hero, About (`#about`), Experience (`#experience`),
  Projects (`#projects`), Contact (`#contact`), Footer.
- **`<script>`** at the bottom — the i18n `translations` object, language toggle, mobile menu,
  and the `IntersectionObserver` fade-in animation.

Other files: `assets/` holds the CV PDFs (linked from the navbar "CV İndir / Download CV" button).

## Internationalization (TR / EN)

The site is bilingual (Turkish default, English optional) and this is the most important thing
to get right when editing content:

- Any translatable element has a **`data-i18n="<key>"`** attribute. Its visible text is the
  Turkish default (the page loads with `setLanguage('tr')`).
- The **`translations`** object in the bottom `<script>` has a `tr` and an `en` map. **Every
  `data-i18n` key must exist in BOTH maps.** `setLanguage()` sets `el.innerHTML` from the map,
  so some values intentionally contain HTML (e.g. icon markup, `<br>`, `<span>`).
- When adding/editing content, update **three places consistently**: the HTML element's
  `data-i18n` attribute + default TR text, the `tr` map entry, and the `en` map entry.

### Project cards

Projects live in the `#projects` grid. Each card is keyed `projectN-title`, `projectN-desc`,
`projectN-demo` (or `-play`), and `projectN-code`. **Card key numbers match their visual order**
(project1 = first card). When reordering, keep the numbering aligned with position so it stays
predictable. To add a card: copy an existing card block, bump N, and add the matching `tr`/`en`
keys. Watch for copy-paste key mistakes (e.g. a mismatched `projectN-demo` key silently breaks
that button in one language).

## Local preview

No build. Open `index.html` directly, or serve it (the browser extension can't load `file://`):

```
python -m http.server 8765
# then visit http://localhost:8765/index.html
```

## Conventions

- Keep it a single self-contained `index.html`; don't introduce a build tool or framework.
- Use Tailwind utility classes inline, matching the existing slate/sky color scheme.
- Preserve the TR-default / EN-toggle i18n pattern for all user-facing text.
