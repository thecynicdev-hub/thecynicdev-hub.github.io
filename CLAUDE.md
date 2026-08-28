# CLAUDE.md — The Cynic Dev hub site

Context for any AI session working in this repo. Read this first, then the
`CLAUDE.md` inside whichever app folder you're touching.

## What this is

A **static GitHub Pages site** that acts as an application portfolio / hub for
"The Cynic Dev". The front page (`/index.html`) lists the apps; each app lives
in its own folder with a set of child pages (product page, pricing, and legal
pages — privacy, terms, refunds — plus, in future, guides / how-tos / FAQs).

- **Live URL:** https://thecynicdev-hub.github.io/
- **Repo / remote:** `thecynicdev-hub/ContextShiftExtension` (branch `main`)
- **Hosting:** GitHub Pages, served from repo root. `.nojekyll` is present —
  Jekyll is disabled, so files are served exactly as committed.
- **No build system.** No npm, no bundler, no framework. Plain HTML.
- **All CSS is inline** in a `<style>` block per page. There is no shared
  stylesheet (GitHub Pages + no build = no partials). Consistency is by
  convention, not by tooling — keep the tokens below identical across pages.
- **Deploy** = push to `main`. There is no preview environment.

## Repo layout

```text
/                          hub root
  index.html               front page — lists the apps
  CLAUDE.md                 this file
  robots.txt               sitemap ref + hides not-yet-public app dirs
  sitemap.xml              hand-maintained; update lastmod + add new URLs
  site.webmanifest         PWA manifest (name "The Cynic Dev")
  .nojekyll                keep — disables Jekyll on Pages
  favicon*.png/.ico, apple-touch-icon.png, icon-192/512.png, og-image.png
  docs/                    reference material for humans/AI, not part of the site
    page-template.html     skeleton to copy when adding a new child page

  contextshift/            App 1 — browser extension (LIVE)
    CLAUDE.md              app-specific facts, URLs, constraints
    index.html  pricing.html  privacy.html  terms.html  refund.html
    og-image.png

  cynical-portfolio-analyser/   App 2 — web app (NOT public yet)
    CLAUDE.md
    index.html  pricing.html  privacy.html  terms.html  refund.html
```

## Brand / identity

- **Public persona:** "The Cynic Dev". Use this everywhere by default —
  nav brand, footers (`© 2026 The Cynic Dev`), copy, signatures (`— The Cynic Dev`).
- **Legal name:** "Bruno Santos" appears **only** in legal pages, and only where
  a real legal entity must be named:
  - ContextShift legal pages: *"Bruno Santos, trading as ContextShift"*
  - Cynical Portfolio Analyser legal pages: *"Bruno Santos, trading as The Cynic Dev"*
  - Also in ContextShift `terms.html` §8: *"Bruno Santos shall not be liable…"*
  - Do **not** introduce "Bruno Santos" anywhere else (marketing pages, hub,
    footers, meta tags).
- **Contact email:** `thecynicdev@gmail.com` (used in footers and legal contact sections).
- **Tone:** honest, understated, anti-hype. "Small tools. No nonsense." One
  developer, no VC, no growth hacking, no telemetry, one-time purchases.

## Shared external services

| Purpose            | Value |
|--------------------|-------|
| Payment processor  | **Lemon Squeezy** (Merchant of Record — handles VAT, receipts, refunds). Replaced Paddle in June 2026. |
| Feedback form      | Tally — `https://tally.so/r/QKOYll` (currently shared by both apps; TODO: separate form for CPA) |
| Search verification| `<meta name="google-site-verification" content="fDKRy_6iUIQHcXLl_mdvj8TjRnGf0gMFZbxDpu5YqKE"/>` — keep on indexable pages |

Do **not** invent product URLs (store listings, app URLs, checkout links). If a
real URL isn't known, use the documented placeholder token from the app's
`CLAUDE.md` and leave a `<!-- TODO -->` comment. Wait for the user to supply real URLs.

## Design tokens (keep identical across every page)

```text
Background        #0a0a0a
Card / panel bg   #111108
Border            #1e2028
Text (primary)    #f0ece4
Text (muted)      #706050
Text (legal body) #907060
Text (dim)        #504840   / #3a3028 for the "← The Cynic Dev" back-link
Accent (gold)     #c8a96e   hover #dfc080
"Live" green      #22c55e   (with 22/33 alpha suffixes for bg/border)
theme-color meta  #0a0a0a
```

- **Font stack:** `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`
- **Mono accents** (eyebrows, footers, `.meta`): `"DM Mono", monospace` /
  `"DM Mono", "Courier New", monospace`. (Not loaded as a web font — it just
  falls back to the system monospace. Don't add a Google Fonts link.)
- **Layout widths:** hub `main` = 860px; product page = 760px; legal pages = 720px.
- **Radius:** cards 10–12px, buttons 6–8px.
- **Reset:** every page starts with
  `*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }`

## Per-page `<head>` conventions

Every indexable page includes, in this order:
1. `<meta charset>`, google-site-verification, viewport
2. `<title>` — pattern: `Product — Short descriptor` or `Product Thing — …`
3. Favicon block (absolute `/` paths): `favicon.ico`, `favicon-32.png`,
   `favicon-16.png`, `apple-touch-icon.png`, `site.webmanifest`, `theme-color`
4. `<meta name="description">` (≤ ~160 chars)
5. `<link rel="canonical">` — absolute `https://thecynicdev-hub.github.io/...`
6. Open Graph (`og:type/url/title/description/image`) + Twitter card tags.
   OG image: hub uses `/og-image.png`; each app uses `/<app>/og-image.png`.
7. JSON-LD where it applies (see `contextshift/index.html`: `BreadcrumbList`,
   `SoftwareApplication`, `FAQPage`). Keep JSON-LD FAQ entries in sync with the
   visible `<details class="faq-item">` list on the page.

## Navigation & linking rules

- Within an app folder, link with **relative** paths (`pricing.html`).
- Link to the hub with `/`. Cross-app links use `/contextshift/…` etc.
- App nav has a small back-link: `<a href="/" style="font-size:12px;color:#3a3028;">← The Cynic Dev</a>`
- App footer pattern:
  `© 2026 <Product> · The Cynic Dev · <page links> · Feedback`
- Every legal page carries `<p class="meta">Last updated: <Month Year></p>` and a
  `.change-log` table (`Date | Change`, newest row first) — add a new row on every
  substantive edit, bump "Last updated", and don't rewrite history.

## When adding a NEW child page (guide / how-to / FAQ / etc.)

1. Copy `docs/page-template.html` into the app folder.
2. Fill in title/description/canonical/OG for the new URL.
3. Reuse the exact design tokens and nav/footer from the app's existing pages.
4. Add the page to `sitemap.xml` (loc + `lastmod` = today + sensible `changefreq`/`priority`).
5. Add a nav link on sibling pages if it's a primary page.
6. Keep it inside the app folder — the hub only lists apps, not their sub-pages.

## When adding a NEW app

1. New folder `/<app-slug>/` with `index.html` + `pricing.html` +
   `privacy.html` + `terms.html` + `refund.html` + `CLAUDE.md` + `og-image.png`.
2. Add a product card to `/index.html` (`tag-live` or `tag-soon`).
3. If not public yet: `Disallow: /<app-slug>/` in `robots.txt`, and
   `<meta name="robots" content="noindex, nofollow"/>` on its pages. Remove both
   when it launches, and add its public URLs to `sitemap.xml`.
4. Create `/<app-slug>/CLAUDE.md` documenting its URLs, pricing, and placeholders.

## Known TODOs / placeholders (2026)

- **ContextShift:** Edge Add-ons URL not yet approved — links use `href="#"` +
  "coming soon". Firefox and Chrome store URLs are real (see `contextshift/CLAUDE.md`).
- **Cynical Portfolio Analyser:** app not public. `PRODUCTION_URL` placeholder in
  `cynical-portfolio-analyser/pricing.html`. Whole folder hidden via `robots.txt`.
  `index.html` meta-refreshes to `/`. Needs its own Tally feedback form.

## Verifying changes

No test suite. To sanity-check: open the changed `.html` files in a browser
(or the `run` skill), confirm nav/footer links resolve, and that light/dark
rendering still matches the tokens. Check `sitemap.xml` and `robots.txt` after
adding or removing pages.
