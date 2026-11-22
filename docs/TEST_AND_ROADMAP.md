# Test Plan & Parallel Roadmap — LandMarketers

## Core tests
- Privacy redaction: trades with partial lot numbers never join exact private parcels.
- Geometry: invalid polygons, CRS mismatches, holes, overlap/tolerance, border parcels, missing DEM.
- Regulation: rules with effective dates, conflicts, conflicting zoning, missing permit requirement, missing source, no '허가 가능' definitive output.
- Transactions: corrected trade, area unit conversions, zero samples, missing prices.
- User: mobile 3D->2D switch preserves selected parcel, provenance links, comparison, data staleness.
- Legal: all monetized transaction features OFF, no seller solicitation, no unsolicited private property contact.
- Reliability: API throttling, WMS outage, imagery rights, retry and checksum.

## Evidence/acceptance
G0 source license/CRS documentation + legal info review.
G1 area-level trades correctly aggregated, redacted exact links absent.
G2 3D/2D maps share feature IDs and accessible UI.
G3 rules trace to verifiable source and manual 'unknown' cases.
G4 real user tests of checklist before further expansion.

## Roadmap
S0 docs/source adapters & 1 trial region; S1 trade region aggregates & parcel overlays; S2 terrain demo with mock label; S3 verified rules/checklist; S4 beta feedback & performance.
Scale via coverage and quality, not quantity of clickable parcels.

## Metrics
verified report completion, source-document click, correction rate, location match false positive rate, geospatial response p95, render FPS and data refresh lag.
