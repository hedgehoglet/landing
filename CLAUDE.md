# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Static site for [hedgehoglet.dev](https://hedgehoglet.dev), hosted on GitHub Pages. No build step: changes to `index.html` and `404.html` deploy automatically on push to `main`.

## Files

- `index.html` — main landing page
- `404.html` — custom 404 with 10-second auto-redirect to `hedgehoglet.dev`
- `assets/style.css` — all styles for `index.html`
- `assets/404.css` — all styles for `404.html`
- `assets/main.js` — scroll reveal `IntersectionObserver` for `index.html`
- `assets/logo.png` — hedgehog illustration, transparent background, no text
- `assets/og.svg` — social card design source; must be exported to `assets/og.png` (1200×630) for OG meta tags to work
- `CNAME` — sets the custom domain to `hedgehoglet.dev`
- `robots.txt` — crawl rules

## Style approach

Both pages use **vanilla CSS in external files** (`assets/style.css`, `assets/404.css`) — no build step, no CDN dependencies. Keep it dependency-free unless there's a strong reason.

## Key details

- Live projects to link: [mojipaper.hedgehoglet.dev](https://mojipaper.hedgehoglet.dev) and [sandbox.hedgehoglet.dev](https://sandbox.hedgehoglet.dev)
- Blog lives at [blog.hedgehoglet.dev](https://blog.hedgehoglet.dev) (hosted on Medium)
- Japanese name "ヘッジホグレット" is part of the brand identity and should be preserved in the hero

## Architecture notes

### Color system
Both pages share the same palette via CSS custom properties on `:root`: `--bg` (`#111111`), `--surface`, `--border`, `--border-hover`, `--text`, `--muted`, `--subtle`, `--accent` (gold `#c89838`), `--accent2` (rose `#c4847a`). Keep both files in sync if changing brand colors.

### Hero visual effects
`.hero` uses `::before` (grain texture via inline SVG `feTurbulence` filter) and `::after` (ambient gold/rose radial gradient orbs) for depth. Both are `position: absolute; inset: 0; pointer-events: none` so they don't interfere with flex layout or child elements.

### Gradient border on hover
`.feature-card:hover` uses the CSS `padding-box`/`border-box` trick: `background: linear-gradient(var(--surface), var(--surface)) padding-box, linear-gradient(...) border-box` with `border-color: transparent` to render a gradient border without extra elements.

### Animated gradient text
`.hero h1 .accent` uses `background-size: 200% auto` with a `gradientShift` keyframe animation to continuously sweep the gold→rose gradient across the text.

### Scroll reveal
Elements with class `reveal` start invisible (`opacity:0; transform:translateY(20px)`) and become visible when an `IntersectionObserver` in `main.js` adds the `visible` class. Use `reveal-delay-1` / `reveal-delay-2` for staggered siblings.

### Project grid
`grid-template-columns: repeat(2, 1fr)`. `li` items use `display: contents` so `.project-card` anchors are the direct grid items. Use `.project-card--wide` (`grid-column: 1 / -1`) to span a card across both columns.

### Safari overflow fix
`overflow-x: hidden` is on `#page-wrap`, not `<body>`, because `position: fixed` (used by `.site-nav`) breaks inside a body with `overflow` set in Safari.

### 404 countdown
A `setInterval` ticking every 1s decrements a counter and redirects to `hedgehoglet.dev/` at zero.
