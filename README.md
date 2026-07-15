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

## Opt-in submissions

Each pin card has an "Opt-In Owner Info or Correction" button that opens an
in-page form (name, corrected GPS coordinates, notes, required contact email,
and a required consent checkbox). Submissions POST directly to
[Formspree](https://formspree.io) from the browser — there's still no server
or database in this repo.

**Submissions never touch the live KML automatically.** They land in your
Formspree inbox/dashboard for manual review, and you decide what (if anything)
to merge into `BICA_Islands_Public.kml`. This matters because anyone can type
any name into the form — without a review step, someone could impersonate an
owner or vandalize a pin's data.

Setup:
1. Formspree endpoint is already wired up: `https://formspree.io/f/mojgjdoq` (set as `FORMSPREE_ENDPOINT` in `site/BICA_Islands_Public.html`).
2. No CORS/domain config is required — Formspree accepts cross-origin AJAX (`fetch`) JSON submissions by default. Optionally, lock the form down to this site only via **Restrict to Domain**, under the **Project's** Settings tab (one level above the individual form) — set it to `mt-gomer.github.io`. Unauthorized-domain submissions get routed to the spam inbox instead of being rejected.
3. On this form's **Settings** tab, under **Spam Protection**, turn on **Formshield** (ML-based spam filtering). **CAPTCHA** is optional if you want an extra layer on top.

## Running locally

```
cd site
python3 -m http.server 8000
```

Then open http://localhost:8000/BICA_Islands_Public.html.

## Status

Text and UI are still being adapted for public use (this currently reuses the internal tool's wording/branding as a starting point).
