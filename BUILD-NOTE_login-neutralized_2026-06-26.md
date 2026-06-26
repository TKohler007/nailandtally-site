# Build note — "Log In" tab neutralized (pre-publish)

**Date:** 2026-06-26
**By:** Jack (Dev)
**Where:** `Builds/legal-site/` (the staged public site)
**Status:** Staged only — NOT published.

## Why
We're about to publish the site, but the web app at `app.nailandtally.com` isn't
deployed yet (Vercel deploy blocked on Thomas's network). The header on every page had
a **"Log In"** button pointing at that address — publishing as-is would have shipped a
**dead link on every page**. This neutralizes it.

## What changed
- The **"Log In"** button in the header is now a **non-clickable** "**Log in — coming
  soon**" element. It still looks like part of the header (same outline style, slightly
  dimmed), but it can't be clicked and goes nowhere — so no dead link.
- This was the same kind of "coming soon" treatment we used for the Privacy/Terms links.
- The green **"Request beta access"** button is **untouched** — still the active button.
- Fixed it on **all 6 pages** that share the header:
  - Home (`index.html`)
  - About (`about/`)
  - Journal (`journal/`)
  - Journal post — "Why I'm building this" (`journal/why-im-building-this/`)
  - Changelog (`changelog/`)
  - Roadmap (`roadmap/`)
- One small styling rule added to the shared `assets/site.css` for the dimmed,
  non-clickable look.

## Nothing else touched
No other text, links, layout, or content changed. Only the Log In button.

## How to turn the real Log In link back on (once the web app is live)
This is written into the code so it's obvious later:
- In **each page's header**, there's a clearly marked comment ("LOG IN — NEUTRALIZED…
  TO RE-ENABLE…") right above the button. Follow it: swap the `<span>` back to a normal
  link (`<a>`) pointing at `https://app.nailandtally.com` with the label "Log In".
- The same re-enable instructions are also noted in `assets/site.css` next to the style.

## Needs QA
Quick visual check by Chuck before publish: confirm the header on all 6 pages shows
"Log in — coming soon" as non-clickable, and "Request beta access" still works.
