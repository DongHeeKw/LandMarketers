# Land Data & Legal Logic — LandMarketers

## Official sources
- 토지 매매 실거래 API: https://www.data.go.kr/data/15126466/openapi.do
- 토지이용계획정보 WMS/WFS/속성: https://www.data.go.kr/data/15123973/openapi.do
- 지적도 WMS/WFS: https://www.data.go.kr/data/15057570/openapi.do
- 용도지역지구정보 WMS/WFS: https://www.data.go.kr/data/15123895/openapi.do

Validate exact service contracts, licensing, tile display conditions, API keys, quota, CRS, update lag before launch. Some reported land trades redact parcel identifiers for privacy; don't silently assign precise parcel IDs.

## Entity model
`parcel(parcel_key,polygon,area_sqm,land_category,boundary_version,source_id,observed_at)`
`zoning_overlay(id,geom,zone_code,valid_from,source_id)`
`restriction_rule(rule_id,legal_basis,effective_from,effective_to,applicable_zone,activity,rule_text,verification_state)`
`trade_event(source_event_id,contract_month,region_code,area_sqm,amount,location_precision,source_id)`
`parcel_trade_link(parcel_key,source_event_id,confidence,manual_review)` — confidence < exact => never public exact claim.
`land_scenario(scenario_id,parcel_key,purpose,rule_version,input_assumptions,results)`
`quality_flag(entity_id,category,details,verified_at)`
`data_provenance(entity_id,source_uri,source_date,ingested_at,checksum)`

## GIS logic
Use correct source CRS transformation, ST_Transform / ST_Intersects, GiST; never approximate parcel boundary from screenshot pixels. Overlay is not legal determination. Slivers & boundaries require tolerance policy, geometry validity checks, and official document link.

## Rule evaluation
Return typed outcomes `CONFIRMED_PUBLIC_FACT`, `POTENTIAL_RESTRICTION`, `INSUFFICIENT_DATA`, `REQUIRES_PROFESSIONAL_CHECK`. Avoid 'PERMITTED' as final decision without official verification.
Rules versioned with legal source, effective date, applicable geography, activity. Unknown takes precedence over false certainty; conflicting rules trigger manual review.
Agricultural acquisition/lease, conversion, permits and specialized jurisdictions vary and require official validation. Distinguish informative checklist from professional legal advice.

## Fraud prevention design
Risk checklist: title and registered rights verification through official sources where lawfully accessible; access road/landlocked status; zoning; boundary/area differences; seller-authority documentation; deposit/contract protections; on-site verification. No automatic 'fraud score' for identifiable owners. Avoid collecting sensitive IDs.

## Idle land policy
'유휴' requires authorized official classification or owner-attested listing with timestamp and verification status; satellite bare field ≠ idle property. Separate suspect candidates from verified offers.

## Time series
Contract month vs report date distinction; revisions/withdrawals captured; aggregate only matched scope. Comparable trades require explicit area, type, region and timeframe; coverage and missingness prominent.

## Data quality
Spatial topology, invalid geom, CRS drift, official source staleness, redaction compliance, 1:n join anomalies, legal rule expiry, confidence and provenance audit.
