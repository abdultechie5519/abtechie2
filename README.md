# AbTechie — GitHub Pages Deployment Guide

AbTechie is currently a **single-file static prototype** (`abtechie.html` — plain HTML/CSS/JS,
no build step, no server). That makes it directly compatible with GitHub Pages as-is.

## Quick deploy (static prototype)

1. Create/use the repository under your account, e.g.
   `https://github.com/abdultechie5519/abtechie`
2. Rename `abtechie.html` to `index.html` and commit it to the repo root
   (or to a `/docs` folder if you prefer that convention).
3. In the repo: **Settings → Pages → Source** → select the branch (e.g. `main`)
   and folder (`/root` or `/docs`).
4. GitHub will publish the site at:
   `https://abdultechie5519.github.io/abtechie/`
5. Because everything (fonts via Google Fonts CDN, inline SVG icons, inline CSS/JS)
   is self-contained or loaded from a public CDN, no additional asset configuration
   or build pipeline is required. There is no client-side router to configure since
   this is a single HTML page with in-page view switching — no 404s on refresh.

## SEO & performance notes already applied

- `<meta name="description">` and Open Graph tags are set for link previews.
- A theme-color meta tag and inline SVG favicon are included (no extra image request).
- All diagrams are inline SVG (no image file requests), keeping the page lightweight.
- Fonts are loaded once via `<link rel="preconnect">` + Google Fonts.

## Moving to a real backend later

This prototype keeps all data (users, approvals, questions, images) in browser
memory only — it resets on every page reload and is not a substitute for real
authentication or storage. When you're ready to go beyond the prototype:

1. Split the app into a proper frontend (React/Next.js + Tailwind, as originally
   scoped) built with a bundler, and deploy the built `dist/` folder to GitHub Pages
   instead of the raw HTML file.
2. Stand up a backend (Node.js/Express) with a real database (PostgreSQL/MongoDB)
   on a free-tier host (Render, Railway, Supabase), since GitHub Pages only serves
   static files and cannot run server code or store data.
3. Point the frontend's API calls at that backend's public URL, and move the admin
   credentials, password hashing, and approval logic entirely server-side.

## Repository suggestion

```
abtechie/
├── index.html          # renamed from abtechie.html
├── README.md
└── (future: /src, /api once split into a real frontend/backend)
```
