# Routed — Website

Plain HTML/CSS/JS, single file (`index.html`), no build step, no dependencies.

## What's in this version
- Full marketing site per the design system (Apple-style neutral palette, single blue accent, dark hero/CTA/footer, scroll-reveal animations).
- Two **illustrative demo widgets** using hardcoded sample data — clearly labeled "Sample data — illustrative preview":
  - **Live tracking**: animated route diagram + a sample list of POs "on the vehicle."
  - **Proof of delivery**: a searchable sample delivery log (search by PO number or store name).
  These are not connected to any real data — they exist to show prospects what the real dashboard will look like once a route is live.

## Known placeholders to replace before sharing with real prospects
- Contact form (`#contact`) shows an alert instead of submitting anywhere — wire it to [Formspree](https://formspree.io) or [Getform](https://getform.io) (both have a free tier and need no backend).
- Footer email (`hello@routedparts.com`) — swap for the real inbox once set up.
- Fleet section has no photos yet — real fleet photography will be the single biggest visual upgrade.
- Founder bio / About section is minimal — fill in once ready.

## Hosting
GitHub (source of truth) → Vercel (auto-deploys every push, free tier). See the walkthrough Claude provided in chat, or Vercel's own docs at vercel.com/docs.

Domain: **routedparts.com** (purchased 2026-08-23) — connect it to the Vercel project under Project Settings → Domains once deployed.
