# Product Requirements — LandMarketers (v0.1)

## Vision
'이 토지가 무엇이며 무엇을 확인해야 안전하게 사용할 수 있는가?'를 지형·규제·거래 정보를 결합해 명확하게 보여준다.

## Personas
A 토지/농지 탐색자, B 농업 창업 준비자, C 토지 검토를 반복하는 전문 사용자. 미성년자나 법적으로 계약 제한이 있는 이용자의 거래 절차를 우회시키지 않는다.

## Feature requirements
| ID | Priority | Requirement | Acceptance |
|---|---|---|---|
| L-F001 | P0 | 지역/지목/면적 탐색 | 공개 범위 내 지도·필터 |
| L-F002 | P0 | 공식 토지 실거래 집계 | 계약월/구역/표본수, 상세 필지 매핑 추정 금지 |
| L-F003 | P0 | 용도지역/규제 레이어 | 소스·기준일·범례·공식 링크 |
| L-F004 | P0 | 필지/지형 상세 | 좌표계·경계 정확도·정보 시점 안내 |
| L-F005 | P0 | 데이터 한계 안내 | 일부 지번 비공개, 불확실한 매칭 배제 |
| L-F006 | P1 | 3D 지형 탐색 | 모바일 2D fallback, 시각화 표기 |
| L-F007 | P1 | 이용목적별 체크리스트 | 농업/시설/임대별 필요한 공적 확인 절차 |
| L-F008 | P1 | 신뢰·주의사항 리포트 | 출처, 확인 필요 서류, 누락 정보 |
| L-F009 | P2 | 공식 매물/임대기관 연결 | 파트너·게시권한 및 현황 확인 |
| L-F010 | P2 | 유휴 후보 표시 | 동의된 등록·공식 공개 물건만, 단순 영상으로 확정 불가 |
| L-F011 | P3 | 중개/거래 수수료 | 법적 자격·계약·보수 규정 외부 검토 후 승인 |

## User experience
3D 대한민국 지형 일부→'농지/도로/규제' 레이어→선택→정확도 및 공식 확인 항목→시나리오 체크리스트→공식 출처. 지도는 매력적이되 결과는 자격/인허가 보장을 하지 않는다.

## Business
무료 기본 탐색 → 전문가 검토 워크플로/리포트 가치 실증 후 유료 기능 → 법률 검토된 부가서비스/제휴. 토지 거래 중개 또는 직접 수수료는 시작 범위가 아니다.

## Guardrails
No deterministic '사기 토지' label, no owner identity speculation, no private owner scraping, no '이 땅은 놀고 있다' unsupported claims, no guaranteed development permission, no parcel-level deal price attribution where identifier redacted.

## KPI
verified_land_report_view, official_doc_click, checklist_completion, user-reported correction, return_for_another_parcel, dataset freshness. Keep facts vs hypotheses visually separate.
