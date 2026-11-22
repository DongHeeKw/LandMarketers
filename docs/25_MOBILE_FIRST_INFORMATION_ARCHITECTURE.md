# Mobile-first Information Architecture & Independent App Boundary (v1.0)

> Status: product architecture specification. The attached visual mockups are **desktop concept references**, not literal requirements to cram every panel into a mobile screen.

## 0. Product identity
**LandMarketers is its own independent application, brand, GitHub repository, frontend, navigation, release pipeline, domain deployment, data contract and user journey.** Do not merge routes, databases, authentication sessions, product analytics or UI branding with the other two products simply because they have a common author. A reusable package may be copied or versioned only if a real shared requirement is demonstrated and its compatibility is tested.

3D 토지 탐험은 넓고 아름답게 보여주되, 필지→공식 데이터→규제→검토 리포트라는 순차 흐름. 토지 지도 위에 실거래·규제·개발 예상 수익을 동시에 겹쳐 놓지 않는다.

## 1. Decision architecture
Choose progressively: one primary task per mobile screen; reveal details only when requested. Do not render the desktop dashboard at 40% width. "Progressive disclosure" means routes/states, not hidden content that is inaccessible on mobile. A map is not a substitute for an accessible information list.

## 2. Page-by-page journey
| Stage | Page | Mobile primary content | Proposed route |
|---|---|---|---|
| 01 | 세계관·진입 | 지형 3D hero, '토지 탐색 시작'. 데모/시각화 경고. 모바일 저사양 2D fallback. | `/` |
| 02 | 지역 선택 | 주소·지번 검색 또는 지도 이동. 지역/필지 식별 가능성과 데이터 제공 범위 안내. | `/explore` |
| 03 | 필지 탐색 | 3D/2D 전환, 지적도와 필지 선택. 선택된 필지 ID는 두 모드에서 동일. | `/parcels` |
| 04 | 필지 개요 | 면적·지목·공식 지도 정보, 자료 시점 및 경계 정밀도. 거래 가격을 정확한 필지에 억지로 붙이지 않는다. | `/parcels/[id]` |
| 05 | 규제·이용 검토 | 용도지역, 중첩 규제, 법적 확인사항 및 모호한 결과 표시. 법적 허가 승인 아님. | `/parcels/[id]/rules` |
| 06 | 거래 비교 | 지역·용도/면적 등 유사 범위의 실거래 집계, 표본·결측 표시. | `/market` |
| 07 | 리포트 | 공식 서류 확인 체크리스트, 데이터 출처·갱신일·미검증 사항 모음. | `/reports/[id]` |

홈은 3D 지형+검색 CTA. 3D 탐색에서는 필지 선택 정보만 간단히 표시; 상세 정보/규제/비교 리포트를 전용 페이지로 분리. 기존 예시 이미지의 3개 분석 패널은 데스크톱 상세 화면 전용.

## 3. Three distinct responsive compositions
| Viewport guidance | Composition | Navigation | Data visibility |
|---|---|---|---|
| Mobile <= 599 CSS px | Single-column, 1 primary CTA, stacked wizard, separate detail route | Bottom nav; native back / persistent route params | 1 main metric group, progressive expansion; full-screen or sheet filters |
| Compact tablet 600–1023 px | Two panes when usable; otherwise mobile stack | Sidebar or tabs | Selected item + one detail panel |
| Desktop >= 1024 px | 2–3 column explorer/detail/analysis workspace | Sidebar or top nav | Rich summary panels, but still grouped by task |
These widths are initial design tokens, not a hard breakpoint to force layout on all devices. Also respond to container width, zoom and touch/hover capabilities. Portrait tablet may use mobile behavior.

## 4. Route-state contract
- Refresh and deep-link must preserve region/category/search/filter/selected item via safe URL query params or persistent session state.
- Browser back returns to the exact previous step with prior selections retained, not back to home.
- No invalid ID silently redirects to an unrelated listing. Offer explicit recovery.
- Loading/empty/error/stale/permission-denied states have unique screens and tests.
- Shareable pages contain server-rendered explanatory content for SEO, not solely WebGL canvas.
- Auth gates only for private personalized features; public analysis stays browsable without signup.

## 5. Design reference migration
- Images in `assets/` or `docs/` should be cataloged as `desktop-concept`, `mobile-flow`, `tablet-split-view`, `3d-scene-reference`.
- Existing beautiful desktop mockups define palette, atmosphere, card treatment, typography, material, and visual hierarchy. Their multiple panels must be mapped into **separate mobile routes**.
- UI copyright/assets: only use images actually present in repo or licensed content, never treat generated demo numbers as real data.
- Mobile illustration must be planned for each key stage independently. Day/night modes change atmospheric lighting, not data truth or navigation structure.

## 6. Agent implementation sequence and TDD
1. Write route-state tests for stage progression, back navigation, and preservation of query params.
2. Implement mobile component skeletons and loading/empty/error states; Playwright viewport screenshots.
3. Add tablet split layout and desktop workspace **without duplicate business logic**.
4. Link domain layer through typed view models. Business rules are independent of CSS or Three.js.
5. Add 3D as an enhancement where applicable with tested 2D fallback and WebGL disabled scenario.
6. Add accessibility tests for keyboard, screen readers, focus order, reduced motion, dynamic zoom up to 200%.
7. Visual regression at widths 375, 430, 768, 1024, 1440 CSS px; use curated stable fixtures.
8. Regression: switching viewport must not lose user-selected state; DOM and selected 3D feature ID match.

### Acceptance scenarios
- Starting on a 375px phone, the user can perform the full journey without horizontal scrolling and without needing dashboard knowledge.
- The user can exit/re-enter each step and retrieve prior selection through route state.
- Critical factual data and source links are readable with no WebGL.
- Desktop supports simultaneous panels but each panel is purposeful, not obligatory.
- No product routes or names from the other two apps appear in this app's main navigation.
- Analytics measure task completion and useful return visits, not time wasted in multi-panel complexity.

## 7. Navigation rules
Mobile bottom nav: 토지 찾기 / 비교 / 저장 / 가이드. 필지 선택 시 바텀시트 간략 정보, '상세 보기'를 눌러 전용 페이지 이동.

## 8. Business safety / correctness
실거래 API의 불완전한 지번을 임의의 특정 필지 가격으로 확정하지 않는다. 위성영상으로 유휴 상태 확정 금지. 부동산 중개·수수료·소유주 연락 매칭은 법적 검토 전 제외.

## 9. Engineering ownership
No technical approval required from the founder. Agent supplies tests, screenshots, performance reports, architecture rationale and teachable file-reading order. Founder reviews the **experience** and business direction; CI and source data checks verify implementation correctness. Do not claim a user preview or WebGL test passed before running it.

## 10. Work packages
- UX-IA-001: independent routing / page inventory / route graph / breadcrumb specification
- UX-IA-002: mobile shell and navigation + Playwright back/forward tests
- UX-IA-003: each screen one goal: search/select/detail/report component suite
- UX-IA-004: tablet split-view
- UX-IA-005: desktop concept decomposition
- UX-IA-006: 3D adaptive rendering + fallback where applicable
- UX-IA-007: responsive + accessibility regression + screenshots
Each PR contains a task-focused demo, test-first evidence, and learning guide.
