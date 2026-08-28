# CLAUDE.md — Cynical Portfolio Analyser (CPA)

App-specific context. Read the repo-root `CLAUDE.md` first for shared conventions.

## What CPA is

A **web app** (hosted separately on Vercel — not in this repo). A free AI
"portfolio critic" that adapts its analysis to the portfolio type (developer,
designer, photographer, writer, …): blunt feedback, no flattery. Free for
single-page analysis; **$9 one-time Pro** unlocks multi-page audits, code fixes,
and clean shareable reports. Reports are stored permanently by unique URL. No
accounts, no tracking. Portfolio content is sent to third-party AI providers for
analysis.

**Status: NOT PUBLIC.** The app isn't launched. This folder holds only the
legal/marketing shell that the app will link back to.

## Current state of this folder

| File | State |
|------|-------|
| `index.html` | `noindex` + `<meta http-equiv="refresh">` → redirects to `/`. "Not yet available." |
| `pricing.html` | Thin stub — points into the app via `PRODUCTION_URL/pricing`. Lighter `<head>` (no favicon block / no site-verification). |
| `privacy.html` | Full policy — change-log table, "Last updated: June 2026". |
| `terms.html` | Full ToS — 11 numbered sections + change-log table. |
| `refund.html` | 14-day guarantee + change-log table. |

The whole folder is hidden from search via `Disallow: /cynical-portfolio-analyser/`
in `/robots.txt`. It is **not** in `sitemap.xml`.

On the hub (`/index.html`) CPA is shown as a **"Coming soon"** card (`tag-soon`),
not a link.

## Placeholders — do not invent real values

| Token | Meaning | Occurs in |
|-------|---------|-----------|
| `PRODUCTION_URL` | The live Vercel app origin (e.g. `https://…vercel.app` or custom domain) | `pricing.html` (2×, both with `<!-- TODO -->` comments) |
| Tally form | CPA reuses ContextShift's `https://tally.so/r/QKOYll` for now — needs its own form (`<!-- TODO -->` in `pricing.html`) |

## Pricing

- **Free:** single-page portfolio analysis.
- **Pro: $9 one-time:** multi-page audits, code fixes, shareable report pages.
- **14-day refund** via Lemon Squeezy (Merchant of Record).
- Actual pricing UI + checkout live **inside the app**, not on these pages.

## Legal entity

**"Bruno Santos, trading as The Cynic Dev"** — used in `privacy.html`,
`terms.html`, `refund.html` (contact/liability sections only). Note this differs
from ContextShift, which trades as "ContextShift".

## Launch checklist (when the app goes public)

1. Replace all `PRODUCTION_URL` tokens with the real app URL.
2. Give CPA its own Tally feedback form; swap the shared link.
3. Replace `index.html` (redirect stub) with a real product landing page using
   the shared design tokens + nav/footer pattern.
4. Remove `Disallow: /cynical-portfolio-analyser/` from `/robots.txt`.
5. Remove `noindex` metas from CPA pages.
6. Add CPA URLs to `/sitemap.xml`.
7. On the hub, change the CPA card from "Coming soon" to a live link (`tag-live`).
8. Consider adding `noindex` to `privacy/terms/refund` until step 4, OR leave as
   is — they're already dir-blocked in robots.txt. (Known minor inconsistency:
   these three lack the `noindex` meta that `index.html` has.)
