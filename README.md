# NOLA — French Quarter Neighborhood Explorer

A mobile-friendly, data-driven static neighborhood explorer for GitHub Pages.
Built with plain HTML, CSS, and JavaScript — no framework, no build step.

## Live site

**https://lookingsharp.github.io/NOLA/index.html**

Deploy to GitHub Pages by enabling it in **Settings → Pages → Deploy from branch (main / root)**.
The site is served from `index.html` at the repository root.

## Files

| File | Purpose |
|---|---|
| `index.html` | Complete single-file application |
| `images/` | Place photo assets (optional — placeholders shown if absent) |
| `images/README.md` | Expected filenames and image size guidance |

## Customization

All neighborhood content lives inside a single JSON block in `index.html`.
Search for `BEGIN DATA` to find it.

To deploy for a new neighborhood:
1. Copy `index.html`
2. Replace the `neighborhood-data` JSON block with new area/place/route data
3. Add images to the `images/` folder (or skip — placeholders show automatically)
4. Deploy to GitHub Pages

Full schema documentation and a customization guide are embedded as comments
at the bottom of `index.html`.

## Features

- Interactive Leaflet map with OSM tiles
- Place cards with expandable accordion details
- Photo gallery with lightbox
- Category filter chips
- Walking route suggestions with map-fit button
- "Use My Location" with distance to each place
- Google Maps deep links for every place
- URL hash deep-linking to individual places (`#jackson-square`)
- Mobile-first responsive design
- Works in iPhone Safari and modern mobile browsers
- No build step, no npm, no framework
