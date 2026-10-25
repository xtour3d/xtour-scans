# xtour-scans

Xtour 360° tours, served from **https://scans.xtour.com.au** by the `xtour-scans` Cloudflare Worker (static assets, no build step). Every push to `main` deploys automatically.

## How it's laid out

```
scans/
  _redirects              # the bare domain (/) redirects to xtour.com.au
  dynamic-steel-hj/       # -> https://scans.xtour.com.au/dynamic-steel-hj/
    index.html
    xtour-tour.js / .css
    tour.json, tags.json, thumb.jpg, cloud.wasm
    pano/  plan/
  <next-scan>/            # -> https://scans.xtour.com.au/<next-scan>/
```

| Scan | URL |
|---|---|
| Dynamic Steel HJ | https://scans.xtour.com.au/dynamic-steel-hj/ |

## Adding a scan

1. Pick a slug: lowercase, hyphens, no spaces (e.g. `acme-warehouse-l2`). It becomes the URL.
2. Put the exported tour files in `scans/<slug>/`, with `index.html` at the top of that folder.
3. Add a row to the table above and push to `main`.

Each scan folder is self-contained. Files load by relative path, so a scan works at any URL. Limits: each file must be under 25 MiB, and the whole site must stay under 20,000 files (about 480 per scan today).

## Removing a scan

Delete its folder and push. The URL returns 404 after the next deploy.
