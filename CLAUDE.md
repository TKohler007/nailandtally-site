# Nail & Tally — marketing site: how to change and update this repo

This file is the operating manual for AI sessions (and humans) editing this site.
Read it before touching anything. Last rewritten: July 18, 2026.

## What this repo is

The public marketing site for Nail & Tally (nailandtally.com), a tool & material
inventory tracker for construction, HVAC, plumbing, and carpentry crews.
Static HTML + one shared CSS file. No build step, no framework, no JS.
Deploys via **GitHub Pages** from the `main` branch: a push to `main` IS a deploy.

Do not remove: `CNAME` (custom domain) and `.nojekyll` (disables Jekyll processing).

## Page map

| Path | What it is | Copy rules |
|---|---|---|
| `index.html` | Landing page | Marketing copy — editable, keep the voice (below) |
| `about/` | Founder story | **Thomas's personal words — never rewrite, only restyle** |
| `journal/` + 3 post folders | Build journal | **Thomas's personal words — never rewrite** |
| `roadmap/` | Honest roadmap | Factual claims — Louis/Thomas must clear changes |
| `changelog/` | Shipped features | Factual claims — only list things that actually shipped |
| `privacy/`, `terms/`, `delete-account/` | Legal | **Wording changes need Thomas's explicit OK** (see Legal below) |
| `404.html` | Not-found page | Editable |
| `assets/site.css` | The whole design system | Change tokens, not scattered values |
| `assets/fonts/` | Self-hosted woff2 | Don't re-add Google Fonts `<link>`s |

## The design system (assets/site.css)

Everything is tokenized in `:root`. Change the token, not the fifty usages.

**Type** (self-hosted in `assets/fonts/`, latin subset only):
- Display: `Barlow Condensed` 600/700 — headlines. "Type on the side of a toolbox."
- Text: `Barlow` 400–700 — body/UI.
- Mono: `IBM Plex Mono` 400–600 — counts, dates, labels, eyebrows. The "tally."

**Color tokens** (stay in the navy + forest-green family; neutrals are warm):
- Navy ramp: `--navy-950 #0B1726` · `--navy-900 #122238` (header/hero/dark bands) ·
  `--navy-800 #16304F` · `--navy #1F3A5F` (brand anchor)
- Green: `--green #15512F` (buttons/links on light) · `--green-bright #2E8A52`
  (accents on dark — glare-tested) · `--green-wash #EAF1EA`
- Neutrals: `--paper #F7F5F0` (page bg) · `--paper-2 #EFECE4` (alt bands) ·
  `--line #DFDACE` · `--steel #E9EBEE` (text on navy) · `--ink #20242B`
- Signals: `--red #A93B2A` (missing) · `--amber #8F5A0E` (low stock)

**Shape language** — deliberate, keep it:
- Tight corners: 3px (buttons/inputs), 6px (cards). Not everything rounded.
- Borders over shadows. The ONE shadow (`--shadow-device`) is reserved for the
  phone and browser mockups.
- Section eyebrows: mono uppercase with the tally SVG (4 bars + diagonal 5th
  stroke) before them, numbered spec-sheet style (`01 · WHAT IT DOES`).
- Left-aligned sections. Don't center everything.

**Hard "not AI-made" rules** (from the project brief): no purple/indigo or
rainbow gradients, no glowing blobs, no emoji in headings/buttons/icons, no
lorem ipsum, no identical rounding + shadows on everything, no
cards-over-hero-with-wave-divider template.

## Voice

Plain tradesman's voice. Short sentences. No "unlock synergy," no startup-speak.
Honest to a fault: never imply traction, customers, or features that don't
exist. Every screen mockup with data MUST keep its "Sample data shown" tag.
Pricing is never a number anywhere — always "Pricing — coming soon."
The primary CTA everywhere is **Start a free pilot** →
`mailto:info@nailandtally.com?subject=Free%20pilot%20request`.

The name is "Nail & Tally" (with the ampersand) anywhere a user can see it.
The internal/technical name "loadout" (app ID, URL scheme) never appears on this site.

## Shared header & footer — IMPORTANT

There is **no templating**. The header and footer are duplicated in every HTML
file. If you change them, change them on ALL pages:
`index.html, 404.html, about/, journal/ (+3 posts), roadmap/, changelog/,
privacy/, terms/, delete-account/` — 12 files. Grep to verify:
`grep -rl 'class="btn head"' .` should list all 12.
Subpage nav marks the current section with `aria-current="page"`.
The header CTA has two labels: `.cta-full` (desktop) and `.cta-short` (mobile) — keep both.

## Common tasks

**Add a journal post**
1. Copy an existing post folder, e.g. `journal/its-live/` → `journal/<new-slug>/`.
2. Update `<title>`, meta description, the page-band (post number, title,
   author/date `<time>`), and the article body. Body = Thomas's words, verbatim.
3. Add a `.post-card` to the top of the list in `journal/index.html` (there's a
   how-to comment in that file). Bump the `#N` number.

**Add a changelog entry**
Add a `.log-entry` at the TOP of the `.log` list in `changelog/index.html`.
`<span class="type new">New</span>` or `type improved`. Only ship-ed facts.

**Update the roadmap**
Edit `roadmap/index.html`, and ALWAYS update the "Last revisited" `<time>` stamp
near the top — a stale date reads as an abandoned product.

**Swap in a real dashboard screenshot**
`index.html` has a marked `SWAPPABLE SCREENSHOT SLOT` comment in the
"On the desk" section — instructions are inline there.

**Change a color / font size**
Edit the token in `assets/site.css :root`. Check both light and dark bands
after — several components restyle themselves inside `.band-navy` /
`.band-charcoal` / `.on-dark`.

## Legal pages (privacy, terms, delete-account)

- The wording is legal content. Do not change meaning without Thomas's explicit
  instruction, and flag anything a lawyer should review.
- History: the pre-2026-07 Terms were truncated (Section 18.5 cut mid-sentence,
  19–20 missing). Completed 2026-07-18 at Thomas's direction (18.5 finished;
  18.6 opt-out, 18.7 venue, 19 general, 20 contact added). Drafted by the
  design team, not a lawyer — pending counsel review.
- If wording changes materially, bump the "Last updated" date in the page's
  `.meta` line. Formatting-only changes don't bump the date.
- The legal shell is `.legal-main > .legal-doc` — restyle there, not inline.

## QA checklist before pushing

1. Serve locally: `python3 -m http.server 8000` from the repo root (absolute
   paths like `/assets/site.css` need a server, not `file://`).
2. Check desktop ~1440px and phone ~390px. Watch: header fits on one line on
   mobile; hero H1 breaks cleanly; dark-band text is `--steel`/`--steel-dim`,
   never dim grey on white.
3. Click every nav/footer link. Internal links are root-relative (`/about/`).
4. Legal pages: confirm wording is what Thomas approved.
5. Push to `main` = live. GitHub Pages takes a minute or two to update.

## Related repos / stages (context)

This site is Stage 1 of a larger rebuild. Stage 2 is the web dashboard
(Next.js, `web/` in the main loadout folder), Stage 3 the Expo phone app
(`mobile/`). Reuse this design system there. Backend (`supabase/`) is
off-limits to design work. The full feature checklist lives in
`Nail-and-Tally-Feature-Inventory.md` in the main project folder.
