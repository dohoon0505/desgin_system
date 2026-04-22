# Changelog

Semantic Versioning을 따릅니다. 과거는 지워지지 않고 아래에 **누적됩니다**.

---

## v0.3.2 — 2026-04-22 · UIUX-DH Icon Package v1 + Nav/Header refinement

### Added
- **UIUX-DH Icon Package v1** — SVG 심볼 스프라이트 기반 통합 아이콘 패키지 (40+ 심볼).
  - Navigation 쌍(outline + fill): `i-home` · `i-calendar` · `i-diary` · `i-cart` · `i-user`
  - Action: `i-arrow-left/right` · `i-chevron-{left,right,up,down}` · `i-close` · `i-check` · `i-plus` · `i-minus` · `i-more-h/v` · `i-menu`
  - Common: `i-search` · `i-bell` · `i-heart(-fill)` · `i-star(-fill)` · `i-settings` · `i-edit` · `i-trash` · `i-share` · `i-filter` · `i-link` · `i-eye(-off)` · `i-mail` · `i-clock` · `i-map-pin` · `i-camera` · `i-image`
  - Status: `i-info` · `i-alert` · `i-check-circle` · `i-x-circle`
  - 공통 규약: 24×24 viewBox · 1.7 stroke · round linecap/linejoin · currentColor
- **Icon CSS utilities** — `svg.ico` 베이스 + `ico-sm/md/lg/xl` 크기 변형 · 기존 `<span class="ico">` (사이드바/탭바 이모지 슬롯)과 충돌 없이 공존.

### Changed
- **Tab Bar 섹션 재설계** — 5탭(디데이·다이어리·홈·스토어·마이페이지) 기준 5가지 활성 상태 매트릭스. 비활성은 outline, 활성은 `-fill` 변형으로 브랜드 컬러 적용.
- **Top App Bar 섹션 재설계** — 5가지 변형 제공: (1) Center+back+more, (2) Left+back+more, (3) Left+back+다음, (4) Left+close, (5) Left+다음. Large title은 별도 최상위 변형.
- **Asset · Icon 섹션 전면 교체** — 아이콘 패키지 전체 쇼케이스(총 40+ 심볼)로 개편. 이모지 사용 금지 원칙 명시.
- **모바일 데모 아이콘 교체** — 커뮤니티·배달·스토어·To-do 등의 탭바/헤더 아이콘을 이모지에서 SVG로 치환.
- **CSS: `text-btn` / `text-btn-brand` 추가** — Top App Bar의 "다음" 같은 텍스트 액션 전용 버튼 스타일.

### Docs
- `components/tab-bar.md` v0.3.2 갱신 — 5탭 표준 + outline/fill 쌍 네이밍 규칙.
- `components/top-app-bar.md` v0.3.2 갱신 — 5가지 변형 + 선택 기준 + UX Writing 가이드.
- `components/asset-icon.md` v0.3.2 전면 재작성 — 아이콘 패키지 카테고리 표 + 확장 가이드.

---

## v0.3.1 — 2026-04-22 · Vanilla JS Architecture + SPA + Demos

### Changed
- **저장소 구조 재편** — 단일 HTML 파일(8,375줄)을 바닐라 JS 구조로 분리.
  - `index.html` (3,680줄) · `assets/css/main.css` (4,311줄) · `assets/js/main.js` (382줄)
  - 기존 단일 파일은 `Single HTML/UIUX-DH-design-system.html`에 자기완결 배포본으로 보존.
- **CLAUDE.md 3단계 작업 원칙 추가** — 수정 시 ① 운영 진본, ② Single HTML, ③ AI 문서(md)를 반드시 함께 갱신.
- **README.md 업데이트** — 새 실행 방법(`index.html` 열기) + 폴더 구조 반영.

### Added
- **SPA 라우팅** — 해시 기반 라우터. 카테고리 클릭 시 하위 항목 카드 그리드 동적 생성, 항목 클릭 시 단일 컴포넌트만 렌더.
- **실제 사용 데모 9종** — Splash · 로그인 · 회원가입 · 커뮤니티 · 배달 · 스토어 · 요금제 · 달력 · To-do List (375×812 모바일 뷰포트).
- **왼쪽 고정 사이드바** — 모든 카테고리가 펼쳐지는 네비게이션 + 모바일 햄버거 토글 + 활성 섹션 자동 하이라이트.

---

## v0.3.0 — 2026-04-22 · Overlays, Navigation, States & UX Writing

### Added
- Overlay 컴포넌트 — Dialog, Bottom Sheet, Popover · Tooltip
- Navigation 컴포넌트 — Top App Bar, Tab Bar, Drawer, Breadcrumb
- State 컴포넌트 — Skeleton Loader, Empty State
- Density 컴포넌트 — Data Table, Accordion · Tree
- UX Writing 7원칙 + 컴포넌트별 라이팅 규칙 + 3종 에러 메시지 템플릿
- Semantic 토큰 확장 — `--sm-background-overlay`, `--sm-surface-*`
- Elevation — `--elevation-5` (모달·시트 전용 최상위 레이어)

### Changed
- **그라데이션 정책 재정의** — 두-색 그라데이션 원칙적 금지, 솔리드 컬러를 기본으로. 진행률·브랜드 모멘트 등 목적이 분명한 경우만 허용.
- Avatar — 솔리드 컬러 변형(`.av-solid`) 추가. 그라데이션 기반 `.avatar`는 레거시로 유지.

---

## v0.2.0 — 2026-04-21 · Component Library

### Added
- 13종 컴포넌트 — Asset & Icon, Badge, Bar Chart, Border & Divider, Button, Chip, Text Field, Avatar, Checkbox · Radio · Toggle, List Item, Alert · Toast, Progress · Slider, Tabs · Segment, Card
- 아이콘 세트 — 24px 그리드, 1.5px stroke, round linecap/linejoin 기본값
- 일러스트 스타일 — 컬러 필 기반, 다크 모드에서 톤 유지
- Button 변형 7종 — primary / tonal / secondary / outline / ghost / dark / danger
- Button 크기 5단계 (sm/md/base/lg/xl), pill/icon/fab 변형
- Status subtle 토큰 — `--sm-status-success-subtle`, `--sm-status-error-subtle`, `--sm-status-info-subtle`
- Chart 타입 — vertical / horizontal / stacked bar
- Field 타입 — default / affix / amount / search

---

## v0.1.0 — 2026-04-21 · Foundations · Initial release

### Added
- **3계층 토큰 아키텍처** — Primitive / Semantic / Component
- Light / Dark 테마 시맨틱 매핑
- 브랜드 컬러 — Indigo 스케일(11단계) 및 Amber Signal
- Pretendard Variable 기반 9단계 타이포 토큰 — display / heading / body / label / caption / overline
- 4px 베이스 사이즈 토큰 (size-50 ~ size-1200)
- Radius 8단계 (none/xs/sm/md/lg/xl/2xl/full)
- Elevation 5단계 (0~4), 다크 모드 대응 그림자
- Motion 토큰 — 5단계 duration, 4종 easing curves
- Button·Input 컴포넌트 토큰 예시
- 네이밍 컨벤션 — `p-` / `sm-` / `cm-` prefix, 축약어 금지, 의미 기반 명명
- 여섯 가지 디자인 원칙 정의

---

## v0.4.0 — Planned · 2026 Q2

### Planned
- Figma Variables ↔ CSS 변수 자동 동기화 플러그인
- WCAG 2.2 AA 대비 자동 검증
- 반응형 레이아웃 가이드 — Breakpoint · Grid · Density
- AGENTS.md 기반 AI 코드 생성 가이드라인

---

## v1.0.0 — Target · 2026 Q4

### Goals
- 모든 프로덕션 화면이 시스템 토큰만으로 구성
- Storybook 기반 컴포넌트 문서화
- React + Vue 듀얼 패키지 제공
- Deprecation 프로세스 문서화 (2 버전 notice, migration codemod 제공)
