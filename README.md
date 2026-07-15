# BICA Islands Public Search (demo)

A public-facing version of the BICA island search tool. Same client-side search page as the internal tool, but with **no owner names, descriptions, or folder structure** — just TP number and coordinates per pin.

No server-side code, no database, no build step. Runs entirely in the browser.

## Live site

Hosted via GitHub Pages: https://mt-gomer.github.io/BICA_Islands_Public/site/BICA_Islands_Public.html

## Repo layout

```
site/
  BICA_Islands_Public.html   the search page
  BICA_Islands_Public.kml    sanitized pin data (TP number + coordinates only)
```

## Data sanitization

`site/BICA_Islands_Public.kml` is derived from the internal dataset with:
- All owner names, descriptions, and extended data fields removed
- All folder/grouping structure removed (flat list of placemarks)
- Only pins with a `TP####`-style name kept — a handful of non-TP entries (waypoints, street addresses) were dropped since they don't fit that format and some were individually identifying
- Any suffix beyond the bare `TP####` (e.g. `(N)`, `(Lot 3)`, `- Island Lodge`) stripped; pins that shared a TP number after stripping were merged into one, using the average of their coordinates

This repo is intended to be **public**. Do not add owner names, addresses, or other personally identifying data back into `BICA_Islands_Public.kml` here — that data belongs only in the private internal repo.

## Deployment

Served automatically by GitHub Pages from the `main` branch (site root, `/`). Any push to `main` that touches `site/` redeploys the live site above within a minute or two — no build step or manual publish required.

## Running locally

```
cd site
python3 -m http.server 8000
```

Then open http://localhost:8000/BICA_Islands_Public.html.

## Status

Text and UI are still being adapted for public use (this currently reuses the internal tool's wording/branding as a starting point).
