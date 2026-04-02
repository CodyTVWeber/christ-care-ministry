# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Project Is

A static HTML/CSS website for Christ Care Ministry (christcareministry.org) — a Christian non-profit delivering food, household supplies, and Christmas gifts across IL, KY, VA, WV, MO, and LA. Two pages: `index.html` (homepage) and `food.html` (food & gifts inventory/requests). Deployed via GitHub Pages using the `CNAME` file.

## Development

No build step. Open HTML files directly in a browser or use any static file server:

```bash
npx serve .
```

There are no dependencies to install, no tests, and no linter configured.

## Image Workflow

All images live in `img/` and must be provided in two formats:
- **Desktop**: `img/ImageName.webp`
- **Mobile**: `img/ImageName-mobile.webp` (resized to 768px wide)

Convert source images with:
```bash
cwebp -q 82 source.jpg -o img/ImageName.webp
cwebp -q 75 -resize 768 0 source.jpg -o img/ImageName-mobile.webp
```

Images are referenced in HTML using `<picture>` elements with a `(max-width: 768px)` media query for the mobile source. Always apply `class="softened-image"` to the `<img>` tag.

## Architecture

- **`styles.css`** — all styles. Tailwind CSS 2.2.19 is loaded from CDN for utility classes; `styles.css` handles custom components (`.hero`, `.mission`, `.services`, `.btn`, `.softened-image`, `.image-grid`, animations).
- **`index.html`** — homepage with hero, about (Rev. Dean Weber), mission pillars, and a 12-image services grid.
- **`food.html`** — food & gifts page with inventory and donation calls-to-action.
- Both pages share identical nav (sticky, glassmorphism, hamburger on mobile) and footer markup — they are duplicated, not templated.

## Key Design Patterns

- **Typography**: `Playfair Display` (headings) + `Inter` (body), loaded from Google Fonts.
- **Color scheme**: Blue (`#2563eb`, `#1e40af`) primary; green (`#16a34a`) for donation CTAs; warm yellow background gradient.
- **Sections**: All `<section>` elements use glassmorphism (`backdrop-filter: blur`), rounded corners, and a shimmer hover animation via `::before`/`::after` pseudo-elements.
- **Animations**: `fadeInUp` on `.fade-in` elements; `pulse` on donation buttons; `rotate` on nav logo.
- **Mobile nav**: Desktop `<ul class="nav-desktop">` is hidden via CSS at ≤768px; a hamburger button toggles `#mobile-menu` via inline `toggleMobileMenu()` JS.
- **Contact**: All donation/inquiry links use `mailto:deanjweber2000@yahoo.com` with pre-filled subject and body parameters.
