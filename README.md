# VGCO — Vienna construction activity (pilot)

**What this is.** A static site: a map of the pilot AOI with, for every
labelled place, the official building data, the orthophoto carousel
2014-2025, the EGMS InSAR motion diagram and the geotechnical screening
context; plus a market dashboard of construction activity per district and
year.

**Serve it.** Any static file server, no backend:

    python -m http.server 8000 --directory deploy
    # then open http://localhost:8000/

The orthophoto base map comes from the City of Vienna's own WMTS (live);
the carousels and diagrams are shipped with the bundle.

## What it claims — and what it does not

* The detector is a **three-band Sentinel-2 index-threshold engine**
  (NDVI loss, BSI and NDBI gain; July year-on-year; T = 0.30; two-year
  persistence; a 3-pixel cluster; the unit is the official footprint).
* **Precision**: 83 % of the footprints it flags in Waehring (a district it
  never saw) are real construction; 70 % on the pilot's human labels.
* **Recall**: it fires on about **6 % of the footprints that actually
  changed** in Waehring (90 % CI 3.7-11.5 %). No threshold, cluster floor or
  area floor lifts that above ~17 %: the ceiling is the 10 m pixel, not the
  parameters (AUDIT.md FINDINGS 27-29).
* The market series is therefore a **floor, not a census**. It is never
  summed with the orthophoto series: the satellite sees the ground change,
  the orthophoto sees the structure appear.
* **The pilot AOI covers Hernals almost entirely and only clips six
  neighbouring districts.** Their zeros are a coverage fact, not a market
  finding.
* Not a substitute for a site investigation: the geotechnical block names
  the mechanisms it cannot speak to (no bearing capacity, no settlement
  prediction).

## Data

Sentinel-2 L2A (10 m, July composites 2015-2026), Vienna orthophoto
2014-2025 (10 cm), official FMZK footprints, GEBAEUDEINFOOGD, ADRESSEN,
BAUPERIODEDETAIL, M29BOHR boreholes, BAUSTELLENPKTOGD/LINOGD works, EGMS
Level-3 InSAR (100 m grid, 2020-2024).
