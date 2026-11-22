# LandMarketers

한국의 농지·토지 **실거래 및 규제 정보 탐색**과 활용 가능성 검토를 돕는 지도 서비스. Three.js 3D 지형/필지 탐색을 사용하되 **공식 정보와 시각화 추정치 구분**을 최우선으로 한다.

## 문서
- [제품 요구사항](docs/PRODUCT_REQUIREMENTS.md)
- [토지 데이터 및 법규 로직](docs/DATA_AND_BUSINESS_LOGIC.md)
- [Three.js 지형 UX](docs/THREEJS_UX.md)
- [아키텍처](docs/ARCHITECTURE.md)
- [테스트 및 로드맵](docs/TEST_AND_ROADMAP.md)

## 범위 경계
첫 출시: 거래 내역/용도지역/규제정보/공식 원본 연결, '활용 검토 체크리스트'. 거래 당사자 연결, 중개 수수료, 유휴토지 확정 판정, 투자 수익 보장은 하지 않는다.

## 기술
Next.js + TypeScript + Three.js/R3F + MapLibre + Python ETL + PostGIS. Vercel 테스트와 Ubuntu 데이터 작업 분리.

문서와 가설만 존재하며 현재 제품/법적 적합성 인증을 의미하지 않는다.
