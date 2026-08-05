# Project card images — drop-in, auto-upgrade

Every project card renders a **code-generated brand tile** (monogram + domain-tinted
gradient + console grid). Nothing is broken or blank if this folder stays empty.

To upgrade a card to a real screenshot, just save a file here with the matching
name. The page picks it up automatically on the next reload — no HTML editing.

| Save this file           | Upgrades the card for              |
| ------------------------ | ---------------------------------- |
| `dts.jpg`                | US Healthcare Claim Submission — DTS |
| `deven.jpg`              | Deven Software (M&A SaaS)          |
| `upay.jpg`               | UPay (fintech)                     |
| `roboket.jpg`            | Roboket (CRM)                      |
| `aarong.jpg`             | Aarong (e-commerce)                |
| `gateway.jpg`            | Gateway to Access                  |
| `wta.jpg`                | World Tax Analyzer                 |
| `tpa.jpg`                | Transfer Pricing Analyzer          |
| `erp.jpg`                | ERP System — NYK Advance           |

## How it works

Each tile contains `<img class="tile-shot" src="assets/projects/<name>.jpg"
onerror="this.remove()">`. If the file is missing the browser fires `onerror`, the
`<img>` removes itself, and the generated tile underneath shows through.

**The cost:** each missing file is one 404 request — so an empty folder means 9 extra
requests per page load and 9 harmless 404 lines in devtools. Visitors never see them
and nothing is blocked (they're parallel and `loading="lazy"`), but it isn't free.
If you decide a given card will never have a real screenshot, delete its
`<img class="tile-shot" ...>` line in `index-v2.html` and that request disappears.

## Specs

- **Aspect ratio:** 16:9. The tile crops with `object-fit: cover`, so keep the
  interesting part near the centre.
- **Size:** 800×450 is plenty. Anything over ~150 KB is wasted bytes — the cards
  are at most ~380 px wide on screen.
- **Format:** `.jpg`. To use `.webp` or `.png` instead, change the extension in the
  `src` for that card in `index-v2.html`.

## Before you add anything — two checks

1. **No internal client systems.** Do not screenshot Veradigm / Mercury IT claim
   tooling, or any screen that shows member, claim or PHI data. That is the one
   thing on this page that could cause a real problem. `dts.jpg` is listed above
   for completeness, but leaving it as a generated tile is the safer call.
2. **Third-party logos and UI belong to their owners.** UPay, Aarong, Devensoft and
   Roboket marks are their trademarks. Public marketing-page screenshots are normal
   portfolio practice, but the generated tiles carry zero risk — which is why they
   are the default.
