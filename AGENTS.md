# Agent Instructions for NOLA — French Quarter Neighborhood Explorer

This file contains instructions for AI coding agents working in this repository.

## Project Overview

NOLA is a **mobile-friendly, data-driven static neighborhood explorer** for GitHub Pages.
It is a single-file application built with plain HTML, CSS, and JavaScript — no framework,
no build step, no npm, no Node.js required.

- **Live site:** served from `index.html` at the repository root (deploy via GitHub Pages)
- **Map library:** [Leaflet](https://leafletjs.com/) loaded from CDN
- **No dependencies to install**

## Repository Structure

```
index.html        Complete single-file application (HTML + CSS + JS + inline JSON data)
images/           Place photo assets here (optional — placeholders shown if absent)
images/README.md  Expected filenames and image-size guidance
README.md         Project overview and deployment instructions
AGENTS.md         This file
```

## Key Sections Inside `index.html`

Use the following search strings to navigate the file quickly:

| Search string            | What you'll find                                  |
|--------------------------|---------------------------------------------------|
| `CSS CUSTOM PROPERTIES`  | Colour palette variables (`--color-*`, etc.)      |
| `BEGIN DATA`             | Start of the swappable `NEIGHBORHOOD_DATA` JSON   |
| `END DATA`               | End of the inline JSON data block                 |
| `FUTURE: EXTERNAL DATA`  | Instructions for moving data to a separate file   |
| `loadData()`             | JS function that parses the inline JSON           |
| `init()`                 | Application bootstrap function                   |

## Data Schema

All neighbourhood content is stored in a `<script id="neighborhood-data" type="application/json">`
block between the `BEGIN DATA` and `END DATA` comments. The top-level keys are:

- **`area`** — page/map metadata (`id`, `title`, `subtitle`, `intro`, `center`, `zoom`)
- **`places`** — array of location objects (see full field list in the `BEGIN DATA` comment)
- **`routes`** — array of walking routes referencing ordered `place.id` values
- **`categories`** — optional override of the auto-derived category filter chips

Edit **only** this JSON block to deploy the template for a new neighbourhood; no JavaScript
changes are needed.

## Making Changes

### Modifying content (places, routes, categories)
1. Open `index.html` and search for `BEGIN DATA`.
2. Edit the JSON object between the `<script id="neighborhood-data">` tags.
3. Validate that the JSON is well-formed before committing (use a linter or browser console).

### Changing the colour palette
1. Search for `CSS CUSTOM PROPERTIES` in `index.html`.
2. Edit the CSS custom properties in the `:root` block (e.g. `--color-accent`).

### Adding images
1. Place image files (JPEG or WebP, 800–1200 px wide) in the `images/` folder.
2. Update the `src` field of the relevant `place.images` entry to `"images/your-file.jpg"`.
3. Missing images fail gracefully — the page shows a placeholder automatically.

### Moving data to an external JSON file
See the `FUTURE: EXTERNAL DATA` comment at the bottom of `index.html` for the two-line
change required in `loadData()` to `fetch()` a separate file instead.

## Linting, Building, and Testing

There is **no build step** and **no automated test suite**.

To validate changes:
1. **JSON validity** — paste the data block into [jsonlint.com](https://jsonlint.com/) or run:
   ```bash
   node -e "const fs=require('fs'); const h=fs.readFileSync('index.html','utf8'); \
     const m=h.match(/<script id=\"neighborhood-data\"[^>]*>([\s\S]*?)<\/script>/); \
     JSON.parse(m[1]); console.log('JSON valid');"
   ```
2. **Browser smoke test** — open `index.html` directly in a browser (or serve it with
   `python3 -m http.server 8080`) and verify:
   - The map loads and markers appear
   - Clicking a marker opens the correct place card
   - Category filter chips work
   - Walking routes fit the map view
   - Images or placeholders render correctly on mobile viewport widths

## Deployment

Enable GitHub Pages in **Settings → Pages → Deploy from branch (main / root)**.
The site is served directly from `index.html` at the repository root — no build step needed.

## Conventions

- Keep all application code inside the single `index.html` file.
- Do not introduce a package manager, bundler, or framework.
- Prefer vanilla JS and standard Web APIs; avoid adding CDN dependencies beyond Leaflet.
- Comment any non-obvious logic using the existing block-comment style (`/* === … === */`).
- Keep the data JSON block self-contained and human-readable; use 2-space indentation.
- Do not commit image files larger than ~300 KB; optimise images before adding them.
