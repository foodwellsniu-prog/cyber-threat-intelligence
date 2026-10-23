# SENTINEL — Cyber Threat Intelligence Dashboard

A responsive, dark-themed cyber threat intelligence dashboard prototype built as a static website.

## Current status

- Premium dashboard UI with responsive layout.
- Interactive global map, sample event feed, country table, severity labels, and event-category charts.
- UTC clock and simple navigation/search.
- **Demo mode only:** map routes, event counts, locations, and risk labels are synthetic illustrative examples. They are not live attack telemetry and must not be interpreted as confirmed attribution to a country.

## Run locally

Open `index.html` in a modern browser. The map uses Leaflet and OpenStreetMap tiles loaded from public CDNs, so an internet connection is required for the map tiles and library.

## Publish with GitHub Pages

1. Open the repository's **Settings**.
2. Choose **Pages** in the sidebar.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select branch `main` and folder `/(root)`, then save.
5. Wait for GitHub Pages to publish the site; the Pages screen will show its URL.

## Connecting real threat intelligence

Before presenting this dashboard as live, connect a legitimate data provider and document the provider, update interval, coverage, and limitations. Recommended integration pattern:

1. A small backend or serverless function retrieves provider data securely.
2. Store API keys in server-side environment secrets; never put private API keys in browser JavaScript or commit them to Git.
3. Normalize events into a documented schema, for example: timestamp, indicator type, source observation, destination observation (if provided), severity, provider, and confidence.
4. Update the UI from the backend endpoint and show the last successful update time and provider status.
5. Do not infer an attacker's nationality from an IP geolocation or a map route. A location can describe an observed IP or hosting endpoint, not necessarily the person or group responsible.
6. Follow the provider's terms, rate limits, privacy requirements, and data licensing.

Public threat feeds often describe specific indicators (such as malicious URLs or IP reputation) rather than verified source-to-destination attack paths. Only show routes if the chosen source actually provides that relationship. Do not label illustrative or inferred data as live.

## Technology

- HTML, CSS, vanilla JavaScript
- Leaflet for interactive mapping
- OpenStreetMap tiles and attribution

## License

No license has been added yet. Add a license before redistributing or accepting external contributions.
