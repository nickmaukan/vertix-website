# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

VERTIX Website — Static landing page for an investment consulting SaaS (Mauri Esp). Single-page HTML/CSS/JS deployed on Vercel.

## Development

```bash
# Open directly in browser
open index.html

# Or serve locally
npx serve .

# Deploy to Vercel
vercel
```

No build step required — pure static HTML with inline CSS and JS.

## Architecture

- `index.html` — Single-page landing (~1000+ lines, inline CSS/JS)
- `.vercel/` — Vercel deployment config
- `DEV_REVISION.md` — Technical audit (HTML/CSS/JS issues, 6.5/10)
- `CRO_REVISION.md` — Conversion optimization notes (5.8/10)
- `QA_REVISION.md` — QA review (6.5/10)
- `RECURSOS_DESIGN.md` — Design spec for a section (HTML/CSS code snippets)

## Key Technical Issues (from DEV_REVISION.md)

Known issues in `index.html`:
- HTML structural problems: orphan `</div>` tags, misplaced content inside `section.faq`
- CSS variables `--surface`, `--text-secondary`, `--primary-dark`, `--secondary` undefined
- Duplicate empty `@keyframes faqFadeIn`
- Google Fonts loads synchronously (blocks render)
- `onclick` inline handlers on plan buttons instead of event delegation

## Section Flow

Hero → Trust Bar → Plans → Recursos (Resources) → Perfiles (Profiles) → FAQ → CTA

## Stack

- HTML5 + CSS3 + Vanilla JS
- Google Fonts (Inter)
- Vercel deploy
- Analytics: Google Analytics, Facebook Pixel, Hotjar
