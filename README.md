# NXT LOOKUP

A privacy-first phone-number lookup and consent-based location finder.

## Current features
- Responsive dark neon dashboard.
- Basic phone-number format validation and common country calling-code hints.
- Honest owner-name status: identity remains unavailable until a lawful, authorized provider is connected.
- Device geolocation only after the browser asks the user for permission.
- Open the user's own coordinates on OpenStreetMap.
- No fake owner names, no fabricated carrier/region results, and no claim that a phone number reveals live GPS.

## Run locally
Open `index.html` in a modern browser. For geolocation, browsers generally require HTTPS or localhost. You can use GitHub Pages (Settings → Pages → deploy from your main branch/root) to serve the static page over HTTPS.

## Official owner identity integration
This project intentionally does **not** scrape private subscriber records or claim access to telecom databases. Before enabling owner-name lookup:
1. Obtain written authorization and API documentation from a provider legally permitted to disclose the relevant data for your use case.
2. Add a server-side endpoint (never place API secrets in browser JavaScript).
3. Require the provider's documented authorization, purpose limitation, rate limits, audit logging, and retention rules.
4. Return only fields that the provider is permitted to disclose. Use statuses such as `verified`, `unverified`, and `unavailable`; include provider/source and timestamp.
5. Never treat a caller-ID label as proof of legal subscriber identity. Do not expose private subscriber details without a valid lawful basis and authorization.

Suggested future response shape:
```json
{
  "status": "unavailable",
  "displayName": null,
  "source": null,
  "verifiedAt": null,
  "message": "No authorized identity data is available for this number."
}
```

The browser currently uses a safe local-only placeholder and does not make a request to a nonexistent identity API.

## Important limits
- Country calling codes do not reliably identify a caller's current location or mobile carrier.
- Device location belongs to the device/browser user who grants permission; it does not locate a phone by its number.
- Sanchar Saathi is an official Indian telecom-safety service, not a general public reverse-phone-owner API. Use official services according to their intended eligibility and access rules.
