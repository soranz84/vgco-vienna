# Publishing this bundle with GitHub Pages

The bundle is static: no backend, no database, no build step.

## 1. Create the repository

* GitHub → **New repository** → name e.g. `vgco-vienna` → **Public**
  (Pages on a private repo needs a paid plan) → do **not** add a README.

## 2. Push THIS folder only

`deploy/` is the product; the rest of the project (2.7 GB of cached tiles,
labels, workbench pages) must not be pushed.

```bash
cd C:/Users/h873d/Documents/pi/craic/deploy
git init
git add .
git commit -m "VGCO Vienna construction-activity screen (pilot)"
git branch -M main
git remote add origin https://github.com/<your-user>/vgco-vienna.git
git push -u origin main
```

## 3. Turn on Pages

Repo → **Settings → Pages** → *Build and deployment*:
* **Source**: `Deploy from a branch`
* **Branch**: `main` · **folder**: `/ (root)` → **Save**

After ~1 minute the site is at
`https://<your-user>.github.io/vgco-vienna/`
(the map: `.../site_map.html`, the market: `.../market_dashboard.html`).

## 4. Optional

* **Custom domain**: Settings → Pages → *Custom domain* (adds a `CNAME` file).
* **`.nojekyll`**: already present; it stops Jekyll from ignoring files that
  start with an underscore.
* **Size**: the bundle is ~77 MB / ~1,350 files — well inside the 1 GB repo
  and 100 GB/month bandwidth limits, and no single file is near the 100 MB
  hard limit, so **no Git LFS is needed**.
* **Tiles**: the map loads the orthophoto from the City of Vienna's live
  WMTS, so the 2.7 GB local cache is deliberately absent.

## What the page claims (keep this in the README)

* precision 75-83 % on the engine's own detections, measured in three AOIs
  (pilot, Währing, Döbling);
* recall 6-14 % of the changed footprints at the frozen operating point,
  bounded at ~17-22 % by the 2 % population false-positive guarantee;
* the district series is a **floor**, not a census;
* the pilot AOI covers Hernals and clips six neighbouring districts.
