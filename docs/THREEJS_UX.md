# Three.js Land Explorer — LandMarketers

## Goal
An instantly intriguing 3D terrain map that leads to **understandable public records**, not a simulated guarantee of land value. User can disable 3D and access all facts in 2D/list.

## First impression
Low-poly terrain overview with highlighted zones, farm/forest/river visual landmarks, smooth zoom to selected area. Conspicuous '시각화 참고용' notice. First CTA '지역 또는 필지 찾기'.

## Scene graph
`LandScene > DEMTerrainTiles > ParcelOutlines > ZoningPolygons > RoadOverlays > HighlightedSelection > InfoPanel`.
Do not rebuild geometry each frame; tile by viewport, instancing as appropriate, LOD by zoom, textured topography if rights permit. Do not overlay parcel polygons without CRS transform and boundary accuracy validation.

## User journey
Search region → terrain view → select parcel or zone → 2D data panel (지목/면적/용도지역/시점) → '무엇을 확인해야 하나?' → export checklist and official reference URLs.

## Engineering
Next.js client dynamic import Canvas using R3F/Three; MapLibre base map 2D. Terrain tile generator on Ubuntu batch if source licenses allow derivative products. Keep 3D geometry files from public client if not licensed. No scraping unlicensed imagery. Adaptive DPR, frustum culling, LOD and tile cache.

## Fallback
WebGL unavailable or low-bandwidth: static 2D map and accessible sortable parcel table. Reduced-motion and keyboard/click touch. No data claim exists only as color in 3D scene.

## Visual QA
Compare selected feature ID between 2D/3D; rendered boundary against authorized GIS reference; off-by-one CRS errors, terrain altitude exaggeration label. Memory cleanup verified; map interaction without JS unaffected for SEO summaries.

## Engagement
Explore scenarios, compare two plots, bookmark regions, update checks and export verification checklist. No pressure to buy property, no fear-driven 'last chance' prompts.
