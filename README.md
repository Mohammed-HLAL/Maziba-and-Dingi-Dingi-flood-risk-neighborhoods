# Maziba-and-Dingi-Dingi-flood-risk-neighborhoods
Application developed by Mohammed Hlal
# Hydrolens — Kinshasa Flood Risk Atlas

Interactive web platform for visualizing flood risk in **Maziba** & **Dingi-Dingi** quartiers (Matete & Kinsenso, Kinshasa, DRC), built directly from your shapefiles.

## How to run — just double-click

1. Unzip the folder.
2. **Double-click `index.html`.** It opens in your browser. That's it.

No server, no installation, no command line. Internet is needed once for the basemap tiles and the Leaflet library (loaded from CDN).

## What you see

Three main thematic layers, mirroring the three reference images you shared:

1. **Flood risk zones** — hatched polygons (Low / Medium / High), like image 2.
2. **Building vulnerability** — building footprints colored by expected water height, like image 3.
3. **Drainage density** — heat-map of streets and drainage channels, like image 1.

Plus quartier boundaries, a scenario filter, four basemap options, and key indicators (building count, area, % at high risk, network length).

## File structure

```
platform/
├── index.html              ← double-click this
└── data_js/                ← shapefile data, embedded as JS variables
    ├── flood_data.js          (3 zones — High / Medium / Low)
    ├── buildings_data.js      (4,035 building footprints)
    ├── drainage_data.js       (8,000 drainage points sampled from 129,545)
    └── quartiers_data.js      (Maziba & Dingi-Dingi boundaries)
```

The original shapefiles were converted to GeoJSON (EPSG:4326), then wrapped as JS so the app works directly from `file://` without needing a web server. Geometries were simplified to keep the bundle around 3.5 MB without losing visual fidelity.

## Stack

- **Leaflet 1.9** — mapping
- **Leaflet.heat 0.2** — drainage heat-map
- **Carto + OSM + Esri** — basemap tiles
- **Vanilla JS** — no build step

## Customization tips

- Colors are CSS variables at the top of `<style>`. Change `--risk-high`, `--vuln-1..4`, etc.
- The drainage density heat-map gradient is in `buildDrainageLayer()`.
- To change the initial zoom, edit `CENTER` and `zoom` in the map setup section.
- To replace data: convert your new shapefile to GeoJSON, then wrap it like:
  `window.MY_DATA = { ...GeoJSON... };`
  save as a `.js` file in `data_js/`, and add a `<script>` tag in `index.html`.
