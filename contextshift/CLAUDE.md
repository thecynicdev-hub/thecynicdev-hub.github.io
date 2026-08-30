# CLAUDE.md — ContextShift

App-specific context. Read the repo-root `CLAUDE.md` first for shared conventions
(design tokens, head structure, brand rules).

## What ContextShift is

A **browser extension** — "Browser Workspace Manager". Save your open tabs as
named workspaces (backed by the browser's **native tab groups**), switch context
in one click, auto-snapshot every 5 minutes, global tab search, Focus Reminder
with a Pomodoro timer, workspace templates. All data is stored **locally** in the
browser's extension storage — no servers, no accounts. The only network call is
license-key validation against `api.lemonsqueezy.com`.

**Status: LIVE** (Chrome + Firefox). Edge pending.

## Pages in this folder

| File          | Purpose | Notes |
|---------------|---------|-------|
| `index.html`  | Product landing page | Has 3 JSON-LD blocks (BreadcrumbList, SoftwareApplication, FAQPage) + a visible FAQ `<details>` list — keep the two FAQ copies in sync. Has a `<script>` that detects the browser and swaps the primary install button. |
| `pricing.html`| Free vs Pro plans | Same browser-detect script. Real Lemon Squeezy checkout link. |
| `privacy.html`| 13 numbered sections + change-log table | Browser-agnostic language (Chrome/Firefox/Edge). |
| `terms.html`  | 11 numbered sections + change-log table | §1 & §8 name "Bruno Santos". |
| `refund.html` | 14-day money-back guarantee + change-log table | Handled by Lemon Squeezy. |

`Last updated: June 2026` on all three legal pages.

## Real URLs (use verbatim)

| Thing | URL |
|-------|-----|
| Product page | `https://thecynicdev.com/contextshift/` |
| Chrome Web Store | `https://chromewebstore.google.com/detail/contextshift/dlepgpniiieoabehelmapldeojcdnjmb` |
| Firefox Add-ons (AMO) | `https://addons.mozilla.org/en-US/firefox/addon/contextshift/` |
| Edge Add-ons | **NOT approved yet** — links use `href="#"` + `onclick="return false"` + "coming soon" styling. Replace when the user provides the real URL. |
| Pro checkout (Lemon Squeezy) | `https://thecynicdev.lemonsqueezy.com/checkout/buy/12e50d9b-3e05-4dff-a1ce-585d3c7b2fe9` |
| Feedback (Tally) | `https://tally.so/r/QKOYll` |

The install `<script>` maps: chrome → Web Store, firefox → AMO, edge → `#`
(click prevented). Keep that mapping in step with the buttons.

## Pricing

- **Free:** up to 5 workspaces, native tab groups, notes/status, 10 auto-snapshots,
  built-in templates. No account.
- **Pro: $19 one-time** (no subscription): unlimited workspaces, full 30-snapshot
  history, global tab search, Focus Reminder, custom templates + template sharing,
  keyboard-shortcut customisation.
- **14-day refund**, no questions asked, via Lemon Squeezy.

## Product facts to keep consistent

- Works in **Chrome, Edge, and Firefox 139+** (Firefox 139 added the native tab
  group API). Other Chromium browsers: use the Chrome button.
- Global search shortcut: **⌘K / Ctrl+Shift+K** on Chrome & Edge,
  **Ctrl+Shift+F** on Firefox (Ctrl+Shift+K clashes with Firefox DevTools).
- Auto-snapshot: **every 5 minutes**; history depth **10 (Free) / 30 (Pro)**.
- Sync: workspaces sync across devices on the *same* browser via the browser
  account (Google / Mozilla); they do **not** cross browsers — platform limitation.
- Legal entity: **"Bruno Santos, trading as ContextShift"** (privacy §1, terms §1 & §8).

## Editing legal pages

Add a row to the `.change-log` table (newest first), bump `Last updated`, and keep
the language browser-agnostic — these pages are submitted to Chrome / Firefox /
Edge store reviewers.
