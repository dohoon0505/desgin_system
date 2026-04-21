# Changelog

Semantic Versioning을 따릅니다. 과거는 지워지지 않고 아래에 **누적됩니다**.

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
