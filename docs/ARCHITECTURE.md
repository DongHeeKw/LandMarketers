# Architecture — LandMarketers

## Modules
Next.js SSR/SEO app, MapLibre 2D, Three/R3F 3D; Python GIS ETL; PostGIS; rule-engine library with effective-date versioning and official citations. Vercel frontend previews + Ubuntu batch and prebuilt GeoJSON/vector tiles.

## HTTP
`GET /v1/regions`, `GET /v1/parcels?bbox=...`, `GET /v1/parcels/{id}`, `GET /v1/zoning?bbox=...&as_of=...`, `POST /v1/scenarios/check`, `GET /v1/provenance/{entityId}`.
No open-ended SQL, bound bbox/size/zoom. Legal checklist response must expose rule_version, confidence, and not-authoritative statement.

## Storage
Separated raw immutable provider objects, normalized spatial model, published render tiles, rule set & legal review registry. Spatial joins done server-side; no private title registry information stored without rights.

## Security
Only server-side API keys; domain restriction when possible; TLS, auth for saved data, rate limiting, structured request validation, secure backup, admin MFA, source license tracking. No user data sold to advertisers, privacy controls for uploads, avoid raw ownership evidence upload in MVP.

## Performance
Precompute static area-level aggregated tiles, gzip/brotli, spatial RTree/GiST; client streaming tiles; 2D fallback. Keep Vercel edge workloads bounded and not dependent on always-on home PC.

## Regulatory review
Real estate brokerage/commissions and ad disclosures require counsel and licensed entity where applicable. Do not build payment/escrow, offer matching or owner-contact relay until reviewed.
