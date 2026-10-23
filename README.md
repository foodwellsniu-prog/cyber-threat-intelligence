# SENTINEL — Cyber Threat Intelligence Dashboard

A responsive, dark-themed cyber threat intelligence dashboard prototype built as a static website.

## Current status

- Premium dark dashboard with responsive layout.
- Interactive global map, sample event feed, country table, severity labels, and event-category chart.
- UTC clock and simple navigation/search.
- GitHub Actions workflow for publishing to GitHub Pages.
- **Demo mode only:** event counts, map routes, locations, and risk labels are illustrative samples. They are not verified live attacks and must not be treated as confirmed attribution to a country.

## Publish with GitHub Pages

The repository includes `.github/workflows/deploy-pages.yml`, which deploys the root of the `main` branch when pushed.

One-time setup required by GitHub:

1. Open **Settings → Pages** in this repository: https://github.com/foodwellsniu-prog/cyber-threat-intelligence/settings/pages
2. Under **Build and deployment → Source**, choose **GitHub Actions**.
3. Open the **Actions** tab and select the **Deploy SENTINEL to GitHub Pages** workflow to monitor deployment. A push to `main` or manual workflow run triggers deployment.
4. Once the workflow succeeds, the published URL should be: https://foodwellsniu-prog.github.io/cyber-threat-intelligence/

If GitHub asks you to approve or enable Actions, follow the repository's on-screen prompt. The website may take a few minutes to become available after the first successful run.

## Public threat-intelligence feed

The dashboard now displays records from the official [CISA Known Exploited Vulnerabilities (KEV) Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog). This catalog lists vulnerabilities that CISA has identified as exploited in the wild; it is **not** a live feed of attacks against this website, your bank, or any specific organization.

- A GitHub Actions workflow downloads and validates the public CISA JSON feed every six hours, and can also be run manually from the **Actions** tab using **Refresh public threat intelligence**.
- The newest 250 catalog entries are published to `data/kev.json`; the dashboard shows the catalog count, release date, and recent additions.
- The refresh workflow deploys the updated static site to GitHub Pages.
- If the first feed refresh has not run successfully yet, the live catalog panel will show a waiting/error message instead of treating an empty file as zero threats.
- The map routes, country counts, risk labels, and category chart remain illustrative demo data. They must not be interpreted as confirmed attacks, attacker nationality, or real-time telemetry.
- CISA KEV entries are vulnerability intelligence. Review vendor advisories and your own asset inventory before deciding whether an item affects your environment.

If the feed does not populate, open **Actions → Refresh public threat intelligence**, run it, and inspect the job logs. The workflow requires GitHub Actions to be enabled and Pages to be configured for GitHub Actions.

## Run locally

Open `index.html` in a modern browser. The map uses Leaflet and OpenStreetMap tiles loaded from public CDNs, so an internet connection is needed for the map library and tiles.

## Connecting real threat intelligence

Before presenting this dashboard as live, connect a legitimate data provider and document its coverage, update interval, and limitations. Recommended integration pattern:

1. A backend or serverless function retrieves provider data securely.
2. Store API keys in server-side environment secrets; never put private API keys in browser JavaScript or commit them to Git.
3. Normalize events into a documented schema, such as timestamp, indicator type, source observation, destination observation (if provided), severity, provider, and confidence.
4. Update the UI from the backend endpoint and show the last successful update time and provider status.
5. Do not infer an attacker's nationality from IP geolocation or a map route. A location may describe an observed IP or hosting endpoint, not the person or group responsible.
6. Follow provider terms, rate limits, privacy requirements, and data licensing.

Public threat feeds often describe indicators (such as malicious URLs or IP reputation) rather than verified source-to-destination attack paths. Only show routes if the selected source actually provides that relationship. Never label illustrative or inferred data as live.

## Technology

- HTML, CSS, vanilla JavaScript
- Leaflet for interactive mapping
- OpenStreetMap tiles and attribution
- GitHub Actions / GitHub Pages for deployment

## License

No license has been added yet. Add a license before redistributing or accepting external contributions.
