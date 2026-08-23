# Routed — Website

Plain HTML/CSS/JS, single file (`index.html`), no build step, no dependencies (one Google Fonts link for the display typeface).

## v8 tweak (2026-08-23, same day) — functional quote request form
The "Request a Quote" contact form previously just showed a placeholder `alert()`. It's now wired to submit to [Formspree](https://formspree.io) (free tier: 50 submissions/month, unlimited forms, confirmed AJAX/JSON support — compared against Getform, which rebranded to "Forminit" in Jan 2026 and caps the free tier at 1 form).

- Added `name` attributes to every field (`name`, `company`, `email`, `message`) — required for Formspree (or any form backend) to capture field data.
- Form now has `id="quoteForm"` and `action="https://formspree.io/f/YOUR_FORM_ID"` — **`YOUR_FORM_ID` is a placeholder that must be replaced with your real Formspree endpoint before this goes live** (see walkthrough below).
- Added a hidden honeypot field (`_gotcha`) — a lightweight, invisible spam trap Formspree recognizes automatically; real visitors never see or fill it.
- Submission now happens via `fetch()` (AJAX) instead of a page reload/redirect — keeps the same in-page, no-jarring-navigation feel as the rest of the site.
- Added an inline success/error status message styled to match the dark contact section (same checkmark icon language used in the value strip), with the submit button showing a "Sending…" state and re-enabling itself afterward.
- If the placeholder `YOUR_FORM_ID` hasn't been replaced yet, submitting shows a friendly inline warning instead of silently failing — so this is safe to deploy as-is and finish connecting whenever the endpoint is ready.

## v7 tweak (2026-08-23, same day) — final headline
User asked for 5 fresh headline hooks (separate from the earlier 4). Picked: **"Never wonder where your parts are again."** — leads with the customer's pain point rather than announcing a feature. Subhead unchanged (still complements it without repeating wording).

## v6 tweak (2026-08-23, same day) — new headline (superseded by v7)
User asked for headline alternatives to "Store-to-store parts delivery, run like clockwork" that communicate what Routed does AND how it's different, while staying short/peppy. Offered 4 directions; user picked the punchiest one. New hero H1: **"Fixed routes. Live tracking. Zero guesswork."** Subhead was also rewritten to avoid repeating "fixed routes"/"tracked" from the new headline — now reads "Contracted, store-to-store parts delivery for Georgia retail chains — proof on every drop, and pricing built around accuracy," which adds who it's for (Georgia retail chains) and two more differentiators (proof of delivery, accuracy-based pricing) instead of restating the headline.

## v5 tweak (2026-08-23, same day) — copy refinements
- Hero value-strip: swapped "Contract-locked, predictable pricing" for "Performance-based contracts, built around accuracy" — better represents that differentiator (the pricing-stability angle is still covered separately in the Capabilities differentiator grid, so nothing was lost).
- "The Solution" paragraph in the Problem/Solution section now weaves in more of the core value props in flowing prose (live tracking, proof of delivery, performance-based/accuracy pricing, dedicated vehicle, AI-optimized scheduling) instead of just naming live tracking and proof of delivery — gives visitors a fuller picture of the value prop earlier on the page, before they reach the dedicated Capabilities section.

## v4 iteration (2026-08-23, same day) — page restructure, real design-system cleanup, generic store names
Feedback on v3: showing NAPA/AutoZone by name implied Routed serves two direct competitors, which reads oddly — replaced with a generic "Auto Shop #___" naming scheme everywhere (map labels, dashboard PO list, proof-of-delivery sample data). Bigger feedback: the map shouldn't be the first thing a visitor sees (not enough context yet), and the Problem/Solution and capability "cards" looked like PowerPoint/generic-SaaS-template boxes with hard-to-read text, not real Apple-caliber design.

**Root cause of the "PowerPoint" look**: bordered boxes + colored circular icon badges + a heading + a paragraph, repeated identically several times, is the single most common generic marketing-template pattern — it's what nearly every no-design-effort SaaS site defaults to. Real Apple marketing pages almost never box small pieces of text like that; they rely on generous whitespace, strong typographic hierarchy, and hairline dividers instead of borders/shadows around every block of copy.

**Fixes:**
- **Typography simplified**: Fraunces (the display serif) is now used in exactly one place — the logo — matching the brand mark the user supplied. Every heading everywhere else (including the hero H1) is now bold system sans-serif. This directly fixes the "somewhat difficult to read" complaint too: the serif's optical-size-144 cut is designed for large display use, and was being used at small card-heading sizes where its fine details hurt legibility.
- **Removed card/box chrome from all text-only content**: Problem/Solution, the "About" section, and the four differentiator items (Performance-based contracts, AI-structured routing, Contract-locked pricing, Consistent vehicles) no longer sit in bordered/shadowed boxes with colored icon badges. Problem/Solution and About now use a plain two-column "editorial" layout with a single hairline divider between columns — no borders, no backgrounds. The differentiator grid uses plain (unboxed) icons with generous whitespace instead of colored-square icon badges.
- **Kept card treatment only for genuinely functional UI**: the live-tracking dashboard (map + status panel) and the proof-of-delivery search tool still sit in a card, because they represent actual app screens, not decorative text blocks — that distinction is what separates "legitimate product UI" from "PowerPoint SmartArt."
- **Removed the Mon–Fri vehicle-icon row entirely** per feedback that it wasn't a good visual — "Consistent vehicles" is now text-only, matching the restraint of the rest of the page.
- **Reordered the page** so the live-tracking demo is no longer the first thing after the hero: Hero (text + a plain, unboxed 3-item value strip) → Problem/Solution → How It Works → Live Tracking demo (now with its own heading and framing copy for context) → Capabilities (proof-of-delivery demo + differentiator grid) → About → Contact. This gives visitors the "why this matters" context before showing the product demo, instead of leading with an unexplained map.
- **Generic store names**: all "NAPA Auto Parts" / "AutoZone" references replaced with "Auto Shop #114 / #118 / #402 / #409" across the map, the dashboard PO list, and the proof-of-delivery sample data — avoids implying Routed serves two named, competing retail chains simultaneously.

## v3 iteration (2026-08-23, same day) — logo fix, tighter copy, dashboard-style tracking demo
Follow-up feedback on v2: logo's pin sat too high and the serif wasn't rendering with the intended rounded/soft look; hero's "Marietta, GA · Electric-First..." eyebrow line felt unnecessary; page needed to read faster overall (Apple-style efficiency); tracking demo should keep improving; vehicle roster shouldn't be listed at all (no vehicles owned yet — the Cybertruck/Model Y/Model 3/diesel-truck breakdown was removed entirely, not just relabeled) since the real value prop is *consistency*, not a specific fleet lineup; the "Box Truck" was actually meant to be a Chevy Silverado diesel truck, but per the same feedback specific vehicles aren't named on the site at all now.

Changes:
- **Logo font fix**: the Google Fonts request now pins two specific static instances of Fraunces by axis values (`ital,opsz,SOFT,wght,WONK`) instead of a variable range — the earlier version requested a range that didn't actually include the SOFT axis in the served font, so the "soft/rounded" styling silently had no effect and Fraunces rendered in its default (non-rounded) form. Now explicitly requests SOFT=100 for the 900-weight logo instance and SOFT=0 for the 600-weight headline instance, so the intended rounded wordmark should render correctly in a real browser with internet access (the sandboxed test browser here has no external network access, so its screenshots fall back to a generic serif — that's a test-environment limitation, not how it'll look for real visitors).
- **Logo position fix**: pin now bottom-aligned with the wordmark's baseline (`align-items:flex-end`) instead of top-aligned — it no longer floats above the text.
- Removed the hero eyebrow line entirely.
- Tightened copy throughout (shorter subheads, one-line step descriptions, less padding) — page is noticeably shorter/faster to scan.
- Tracking demo redesigned as a two-panel "dashboard" — map on the left, a live-style status panel on the right (route name, next-stop ETA, on-vehicle PO list) — reads much more like a real app screenshot than a plain map.
- Removed all specific vehicle names/models from the site (no more Cybertruck/Model Y/Model 3/Box Truck roster) — the "Consistent vehicles" capability card now focuses purely on the value prop (same dedicated vehicle every run, so stores always know what will fit) with a simple Mon–Fri "same vehicle, every day" icon row instead of a fleet list. This avoids publicly committing to a vehicle lineup that isn't finalized/owned yet.

## v2 redesign (2026-08-23)
- New brand: wordmark logo built from the "Fraunces" serif (Google Font) in the new brand blue `#2563eb`, with a location-pin mark and dashed underline, matching the logo image the user supplied.
- Full visual redesign aimed at a premium, Apple-caliber feel: serif display headlines paired with system-font UI text, a dark hero with a floating "product shot" card, a bento-style capabilities grid, a timeline-style "How It Works," and custom iconography (no stock photos, no icon libraries).
- The live-tracking demo is no longer an abstract straight line — it's a custom vector map illustration (roads, blocks, four store pins) with a car icon animating along a curved route via SVG `animateMotion`, plus a growing "distance traveled" line. This is a hand-drawn illustration, not an embedded Google Maps widget — no API key required, and it renders identically for every visitor. If real Google Maps embedding is ever wanted for Phase 2 (with real vehicle positions), that requires a Google Maps JavaScript API key and billing account — a separate step.
- Removed the standalone "Fleet" section (three vehicle cards) per feedback that it didn't add much value — vehicle-type messaging is now folded into a compact 4-vehicle chip row inside the "Consistent vehicle types" capability card.
- Corrected the "all-electric" claim: the fleet is now described as **electric-first** — three EVs (Cybertruck, Model Y, Model 3) plus one **diesel box truck** for heavy/maximum-capacity routes at launch, each vehicle chip tagged ELECTRIC or DIESEL. The pricing-stability pitch was reworded from "no gas surcharges because EVs" (which wouldn't be true for the diesel truck) to "contract-locked pricing regardless of how a given route is powered" — an honest, and arguably stronger, claim.
- Added a "Performance-based contracts," "AI-structured routing," and a pricing-stability card with a small illustrative sparkline comparison (clearly conceptual, not real performance data — no fabricated stats anywhere on the site).

## What's in this version
- Full marketing site with the new design system described above.
- Two **illustrative demo widgets** using hardcoded sample data — clearly labeled "Sample data — illustrative preview":
  - **Live tracking**: custom map illustration with an animated vehicle + a sample list of POs "on the vehicle."
  - **Proof of delivery**: a searchable sample delivery log (search by PO number or store name).
  These are not connected to any real data — they exist to show prospects what the real dashboard will look like once a route is live.

## Known placeholders to replace before sharing with real prospects
- Contact form (`#contact`) is wired to Formspree but still has a placeholder endpoint (`action="https://formspree.io/f/YOUR_FORM_ID"`) — create a free Formspree account/form and paste your real endpoint URL in (see v8 note above and the walkthrough sent alongside this file).
- Footer email (`hello@routedparts.com`) — swap for the real inbox once set up.
- Founder bio / About section is minimal — fill in once ready.

## Hosting
Already live: GitHub (`corbett90/route-website`) → Vercel (auto-deploys every push) → routedparts.com (DNS via Cloudflare). Replacing `index.html` in the GitHub repo redeploys automatically within about a minute.
