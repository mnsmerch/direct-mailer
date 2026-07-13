# Paint Pals — Direct Mailer Estimate Form

A self-contained, multi-step lead form embed for direct-mailer landing pages,
styled to match the `quote.thepaintpals.com` landers (Poppins, brand green
`#2F7740`, hero photo with white form card, Google reviews badge).

## Usage

Copy the entire contents of `paint-pals-direct-mailer-form.html` into a
**Custom HTML** block (or section) on the WordPress page. The block is fully
scoped under `#paint-pals-estimate-form`, full-bleed, and responsive — no
theme changes needed.

## Flow

1. **ZIP check** — gate against the Colorado service-area list (ZIP → city)
2. **Service type** — exterior / interior / cabinet / other
3. **Name** (requires first + last)
4. **Email** (validated)
5. **Phone** (10+ digits) → submit
6. **Thank you** — with `tel:9705999614` CALL NOW button (direct-mailer tracking number)

## Mobile sticky bar

On screens ≤900px a fixed bottom bar shows two buttons:
- **Get Quote** (black) — scrolls to the form and focuses the current step's input
- **Call Now** (green) — dials `970-670-8887`

## Live Google review count

The "4.9 | 329 Google Reviews" badge can update itself. In the script config
at the top, set `GOOGLE_PLACE_ID` and `GOOGLE_PLACES_API_KEY` (a key with only
"Places API (New)" enabled, restricted to your website domain). The badge then
fetches the live rating/count and caches it in localStorage for 24 hours.
Left blank, the hardcoded numbers are used.

## Lead delivery

- Posts to the LeadConnector webhook as `FormData`, with a JSON `no-cors`
  fallback and a hidden-form fallback if both fetches fail.
- Captures UTM/click-ID attribution (`utm_*`, `gclid`, `fbclid`,
  `taboolaclickid`, etc.) plus landing URL and referrer once per page load
  and includes it in the payload.
- Fires the Taboola `lead` conversion (safe no-op when `_tfa` isn't present).
- Payload `source` field: `Paint Pals Direct Mailer Form`.
