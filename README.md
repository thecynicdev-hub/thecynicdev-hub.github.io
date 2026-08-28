# thecynicdev-hub.github.io

Static GitHub Pages site — an application portfolio / hub for **The Cynic Dev**.
The front page lists the apps; each app has its own folder with a product page,
pricing, and legal pages (privacy / terms / refunds), plus room for guides and
FAQs.

- **Live:** https://thecynicdev-hub.github.io/
- **Stack:** plain HTML, inline CSS per page, no build system. `.nojekyll` is set.
- **Deploy:** push to `main`.

## Apps

| Folder | App | Status |
|--------|-----|--------|
| `contextshift/` | ContextShift — browser workspace manager (extension) | Live (Chrome, Firefox; Edge pending) |
| `cynical-portfolio-analyser/` | Cynical Portfolio Analyser — AI portfolio critic (web app) | Not public yet |

## Working on this repo

Read **`CLAUDE.md`** (repo root) for conventions — design tokens, `<head>`
structure, brand rules — then the `CLAUDE.md` inside the app folder you're
editing. Copy `docs/page-template.html` when adding a new child page.
