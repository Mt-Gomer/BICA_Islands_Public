# BICA Islands Public Search (demo)

A public-facing version of the BICA island search tool. Same client-side search page as the internal tool, but with **no owner names, descriptions, or folder structure** — just TP number and coordinates per pin.

No server-side code, no database, no build step. Runs entirely in the browser.

## Repo layout

```
site/
  bica-island-owner-search.html   the search page
  BICA_TP_Search.kml              sanitized pin data (TP number + coordinates only)
```

## Data sanitization

`site/BICA_TP_Search.kml` is derived from the internal dataset with:
- All owner names, descriptions, and extended data fields removed
- All folder/grouping structure removed (flat list of placemarks)
- Only pins with a `TP####`-style name kept — a handful of non-TP entries (waypoints, street addresses) were dropped since they don't fit that format and some were individually identifying

This repo is intended to be **public**. Do not add owner names, addresses, or other personally identifying data back into `BICA_TP_Search.kml` here — that data belongs only in the private internal repo.

## Running locally

```
cd site
python3 -m http.server 8000
```

Then open http://localhost:8000/bica-island-owner-search.html.

## Status

Text and UI are still being adapted for public use (this currently reuses the internal tool's wording/branding as a starting point).
