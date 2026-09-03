# Stonks on Solana

An editorial market board for Solana tokenized-equity pairs, built for Merkle Research.

## What it does

- Displays Solana-only markets with price, 24-hour move, volume, liquidity, and market cap.
- Requests live data from StonkFun's public `platform-pools` endpoint.
- Falls back to `data/market-snapshot.json` when the live endpoint is unavailable.
- Includes search, sorting, automatic refresh, a market detail modal, and visible source status.
- Ships as a dependency-free static site that can deploy directly to GitHub Pages.

## Run locally

Because the app loads JSON with `fetch`, serve the folder over HTTP instead of opening `index.html` directly:

```bash
python3 -m http.server 4173
```

Then open `http://127.0.0.1:4173`.

## Data source

The live adapter requests:

```text
https://www.stonkfun.xyz/api/platform-pools?sort=marketCap&page=1&pageSize=30
```

The UI expects a JSON payload containing a `pools`, `markets`, or `tokens` array. The normalizer accepts common field names and filters for Solana/Raydium-style records. The public source currently does not require an API key. If its endpoint returns an error, the interface keeps working in snapshot mode and labels that state in the header and footer.

## Deploy

The included `.github/workflows/pages.yml` workflow publishes the repository root to GitHub Pages on every push to `main`. In the repository settings, set Pages to use GitHub Actions if it is not selected automatically.

## Structure

```text
index.html                    page structure and accessible controls
styles.css                    grayscale editorial visual system
app.js                        source adapter, rendering, sorting, modal
data/market-snapshot.json     clearly labeled fallback dataset
.github/workflows/pages.yml   GitHub Pages deployment
```

## Notes

StonkFun is the requested primary source. This interface is informational and does not provide investment advice.
