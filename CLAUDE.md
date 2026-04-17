# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Static site for [hedgehoglet.dev](https://hedgehoglet.dev), hosted on GitHub Pages. No build step: changes to `index.html` and `404.html` deploy automatically on push to `main`.

## Files

- `index.html` - main landing page
- `404.html` - custom 404 with 10-second auto-redirect to `hedgehoglet.dev`
- `CNAME` - sets the custom domain to `hedgehoglet.dev`
- `robots.txt` - crawl rules

## Style approach

Both files use **vanilla CSS** (inline `<style>` block, no build, no CDN dependencies). Keep it dependency-free unless there's a strong reason.

## Code style

- No `/* --- Section --- */` or `/* === Section === */` dashed/decorated section divider comments in CSS
- No em dashes (`—`) in copy: use `·` as a separator in titles/footers, `:` or `.` mid-sentence

## Key details

- Logo: `assets/logo.png` - hedgehog illustration, transparent background, no text. Original full-brand assets (with text) are in `hedgehoglet-assets-main/logo/`
- Live projects to link: [mojipaper.hedgehoglet.dev](https://mojipaper.hedgehoglet.dev) and [sandbox.hedgehoglet.dev](https://sandbox.hedgehoglet.dev)
- Blog lives at [blog.hedgehoglet.dev](https://blog.hedgehoglet.dev) (hosted on Medium)
- Japanese name "ヘッジホグレット" is part of the brand identity and should be preserved in the hero
