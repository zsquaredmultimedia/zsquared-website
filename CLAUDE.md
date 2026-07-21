# Z Squared Multimedia — zsquaredproductions.com

Static marketing site for Z Squared Multimedia Productions (Las Vegas broadcast production company, owner Kyle Zuelke). This folder is the deploy source — what's here mirrors what gets uploaded to the live server.

## Structure
- 7 pages: `index.html`, `work.html`, `services.html`, `about.html`, `contact.html`, `locations/las-vegas.html`, `locations/los-angeles.html`
- Single stylesheet: `assets/css/site.css` (referenced as `site.css?v=2` for cache-busting)
- Images: `assets/photos/` (optimized WebP + legacy JPEG originals), logos in `assets/photos/logos/`
- Video: `assets/videos/homepage-hero-720.mp4` (3.2 MB) + `homepage-hero-poster.jpg`; the old 13.5 MB `homepage-hero.mp4` is unreferenced but kept
- `.htaccess`: 301 redirect non-www → www
- Contact form posts to Formspree (`https://formspree.io/f/meenwarb`)
- `site.zip` is a stale pre-optimization backup; `deploy-update.zip` is the latest deploy bundle

## Hosting & deployment
- Host: GoDaddy cPanel (Apache), web root `public_html`
- Behind a **Sucuri firewall** (GoDaddy Website Security). Domain resolves to Sucuri (192.124.249.x), so **FTP via the domain does not work** — deploy through cPanel File Manager: upload a zip to `public_html`, Extract, delete the zip
- **After every deploy, clear the Sucuri cache** (dashboard → Clear Cache), or visitors keep getting stale HTML
- Files must be permission 644 (dirs 755) — the SSD's default 700 breaks the server with 403s. Any deploy zip must be built from 644 copies
- Sucuri is set to High security: non-JS clients get a JavaScript challenge (accepted trade-off; Google/Bing whitelisted)

## Conventions
- Cache-bust strategy: query string `?v=N` on css/logo refs; renamed files for big assets (video)
- New raster images: resize to ≤1920 px, WebP ~q80 (photos) or optimized PNG (logos w/ alpha); target <350 KB
- Below-the-fold `<img>` tags get `loading="lazy"`; nav logos stay eager
- Titles ≤60 chars, meta descriptions ≤160 chars, unique per page
- Every page: self-referencing www canonical, one H1, JSON-LD structured data
- og:image should stay JPEG (1200×630, <300 KB): `assets/photos/IMG_2068-og.jpg`

## State (as of 2026-07-14)
Full audit + remediation completed: homepage ~19.3 MB → ~3.6 MB. All 7 audit actions done and verified live.

Open/optional items:
- Watch Core Web Vitals in Google Search Console (expect improvement over coming weeks)
- HSTS not yet enabled (available in Sucuri "Additional Headers" panel)
- "Transparent pricing" section on homepage shows no actual rates — copy decision pending
- Contact email is Gmail; domain email suggested
- Old original JPEGs still on server, unreferenced (harmless)
