# Presell — The Backyard Bounty (BB-1002 redesign)

Two versions with the same copy, image, CTAs, tracking and legal footer:

- `presell/` — **v1**: keeps the original look (white card, red headline, yellow buttons).
- `presell-v2/` — **v2**: new visual (serif headline with highlighter, framed video, orange CTAs, "Sound familiar?" pain block, dark green footer). Good A/B candidate against v1.

Static page: `index.html` + `assets/`. No build step, no external dependencies.

## Destination
All CTAs (thumbnail + 2 buttons) go to `https://backyardbounty.vercel.app/` — the same route as the original page.
The presell's query string (UTMs, `fbclid`, `gclid`, sub IDs…) is appended to the CTA links on load; keys already present on the destination are not overwritten.

## Events
Sent to `dataLayer`, `gtag` and `fbq` **only if they exist on the page** (the original had no analytics installed):

| Event | When |
|---|---|
| `presell_view` | once on page load |
| `presell_video_click` | click on the thumbnail |
| `presell_primary_cta_click` | "Watch the Free Video Now" |
| `presell_secondary_cta_click` | "Show Me How It Works" |

Navigation is never delayed waiting for analytics.

## Headline A/B test (future)
Live: **Variant A**. Swap only the `<h1>` text to test.

- **A — Curiosity + small space (live):** A Surprising Way to Grow Fresh Food in a Space the Size of a Parking Spot
- **B — Objection + benefit:** No Big Backyard? See This Small-Space Food Growing Method
- **C — Curiosity about the method:** The 'Parking Spot' Growing Method: See How It Works

No winner is assumed — decide by presell CTR (unique clickers / unique visitors) with enough traffic per arm.

## Pending validation
- Copy was not checked against the VSL (destination was not reachable from the build environment). Confirm the video actually shows the "parking spot"-sized space idea.
- Footer links (Home, Disclaimer, Privacy Policy, Contact, Terms) point to the VSL URL, exactly as in the original. Replace them with real legal pages.
