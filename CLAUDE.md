# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A static one-page personal brand website for Cristel Rodríguez (personal growth, spirituality, trading mindset, and digital marketing/AI mentorship). Pure HTML/CSS/JS — no build step, no package manager, no framework.

## Files

- [index.html](index.html) — single-page site, all sections (Hero, Sobre Mí, Pilares, Academia, Contacto, Footer)
- [style.css](style.css) — all styling, theme variables defined as CSS custom properties in `:root`
- [script.js](script.js) — vanilla JS, all behavior wired up inside a single `DOMContentLoaded` listener
- `img/` — photos used across the site
- `_docs/` — private source documents (brand docs, CV); excluded from git via `.gitignore`, do not reference these paths from the site

## Running locally

No build/install required. Open `index.html` directly in a browser, or serve the directory with any static file server (e.g. `python -m http.server`) to test from `localhost`.

## Architecture notes

- **Theming**: colors, gradients, fonts, and transitions are centralized as CSS custom properties in `:root` in [style.css](style.css). Adjust the palette there rather than hardcoding colors in component rules.
- **Section styling pattern**: `section:nth-of-type(even)` automatically gets the alternate background color (`--bg-section-alt`) — adding/removing/reordering `<section>` elements changes which sections get this styling.
- **Pillars tabs**: the "Mis Pilares" section is a tabbed interface — each `.pillar-tab-btn` has a `data-pillar` attribute matching the `id` of a `.pillar-pane`. JS in `script.js` toggles `.active` on both in sync. When adding a new pillar, add both the tab button and its corresponding pane with matching id/data-pillar.
- **Scroll-driven behavior** (all in `script.js`, no external libs):
  - Navbar gets `.scrolled` class past 50px scroll.
  - Active nav link is highlighted based on which `<section>` is currently in view.
  - `.reveal` elements fade/slide in when scrolled into view (add this class to animate new content blocks).
- **Lightbox**: gallery images (`.gallery-item` > `.gallery-img`) open in a `#lightbox` modal on click; only wired up if `#lightbox`/`#lightbox-img`/`#lightbox-close` exist in the DOM (currently no gallery section is present in `index.html`, but the CSS/JS support it).
- **Contact form**: submission is simulated client-side only (no backend) — shows an alert and resets the form after a timeout.
- **IDs**: most interactive/clickable elements have explicit `id` attributes (e.g. `btn-hero-start`, `nav-link-pilares`) — preserve these when editing markup since they may be referenced for analytics or future JS.
