# README · SPT Public Webroot

> Hand this folder to the agent/site builder. **Everything in this folder is meant for a separate, public-facing static website** — NOT for the private app repo.

## What this is

Minimal static webroot for **SPT - Smart Similar Photo Cleaner** (Windows desktop app). Its job:

1. Satisfy the **Microsoft Store hard requirement**: a public HTTPS Privacy Policy URL.
2. Provide a minimal product landing page (name, tagline, Store link, support contact).
3. Leave room to grow into an SEO/marketing site later (Stage 2 in our roadmap).

## Files

| File | Purpose | Deploy as |
|---|---|---|
| `index.html` | Minimal landing page — product name, tagline, 3 feature cards, Store CTA, footer links | `/` (root) |
| `privacy.html` | Full Privacy Policy page (self-contained, no external deps) | `/privacy.html` (or `/privacy/`) |
| `privacy-policy.md` | Markdown source of the policy — edit here, then regenerate/sync `privacy.html` | — (not deployed) |

## Placeholders — MUST fill before going live

Search and replace in all files:

| Placeholder | Replace with |
|---|---|
| `[MS-STORE-URL]` | SPT's Microsoft Store listing URL (once the listing exists; e.g. `https://apps.microsoft.com/detail/<ProductId>`) |
| `[SUPPORT-EMAIL]` | Your support email (must match the email in the Microsoft Partner Center listing) |
| `[EFFECTIVE-DATE]` | e.g. `October 14, 2026` |
| `[YEAR]` | Current year for the footer |
| `[FEEDBACK-FORM-PROVIDER]` | The feedback-forwarding service used (e.g. `Formspree`) |

## Deployment options (pick one — all free, no backend)

1. **GitHub Pages** — create a NEW public repo (e.g. `spt-site`), push this folder, enable Pages → deploy from `main` / root. URL: `https://<user>.github.io/spt-site/`. (Do NOT publish the private app repo; Pages on private repos needs paid GitHub plan.)
2. **Cloudflare Pages** — connect a Git repo (private is OK) or drag-drop upload. URL: `https://<project>.pages.dev`. Supports custom domains + redirects later.
3. **Netlify Drop** — drag this folder into netlify.com/drop. Fastest 10-minute option; migrate later.

## Rules for the builder

- Keep it **fully static** — no server, no database, no forms that need a backend (the in-app feedback form already handles feedback).
- **English only** — SPT's audience is English-speaking; do not add other languages or non-English UI text.
- **No app code, no user photos** — this site never shows, links to, or references any real user photo data.
- Keep the privacy statements **accurate to the app's actual behavior**:
  - Photos/files/folders/EXIF never leave the device (fully local processing).
  - Diagnostics (Sentry + PostHog) are **anonymous, consent-gated, opt-out any time**, device identified by random local ID only.
  - Purchases are handled by Microsoft; we never see card details.
- Do not change facts in `privacy.html` without also updating `privacy-policy.md` (and vice versa).
- Later (Stage 2): add a real marketing page, SEO meta/canonical, and a sitemap — the current files are a foundation.

## Store listing tie-in

Paste the deployed privacy URL into Partner Center: **App submission → Properties → Privacy policy URL**.
Recommended path shape: `https://<your-domain>/privacy.html`.
