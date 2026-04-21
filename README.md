# UIUX-DH · Unified Design System

> 토큰부터 문장까지. 모바일 중심의 통합 디자인시스템.
> 현재 버전 **v0.3.0** · 최초 릴리스 2026.04.21 · 최근 업데이트 2026.04.22

## 이 저장소는

기존 단일 HTML 문서 ([`UIUX-DH-design-system.html`](UIUX-DH-design-system.html))를 사람과 AI 모두가 빠르게 탐색할 수 있는 구조로 재구성했습니다. 원본 HTML은 시각적 쇼케이스로 보존되며, 아래의 분할 구조는 편집·추적·AI 참조를 위한 **Single Source of Truth** 입니다.

## 폴더 구조

```
desgin_system/
├── UIUX-DH-design-system.html     ← 시각적 쇼케이스 (원본, 유지)
├── README.md                       ← 이 파일 · 사람용 진입점
├── CLAUDE.md                       ← AI 에이전트용 탐색 가이드
├── CHANGELOG.md                    ← 버전 이력
│
├── docs/                           ← 개념과 정책
│   ├── 00-overview.md              · 디자인시스템이란
│   ├── 01-principles.md            · 여섯 가지 원칙
│   ├── 02-token-architecture.md    · 3-tier 토큰 구조
│   ├── 03-naming-conventions.md    · 네이밍 규칙
│   ├── 04-gradient-policy.md       · 그라데이션 정책
│   └── 05-ux-writing.md            · UX 라이팅 7원칙
│
├── tokens/                         ← 기계 판독용 값 (JSON)
│   ├── primitives.json             · Tier 1 · 원시 컬러 스케일
│   ├── semantic.light.json         · Tier 2 · Light 테마 매핑
│   ├── semantic.dark.json          · Tier 2 · Dark 테마 매핑
│   ├── typography.json             · 폰트·스케일 토큰
│   ├── sizing.json                 · 4px 기반 스페이싱
│   ├── radius.json                 · 모서리 반경
│   ├── elevation.json              · 그림자 레벨
│   ├── motion.json                 · duration + easing
│   └── z-index.json                · 레이어 순서
│
├── foundations/                    ← 시각 기초를 사람이 읽는 형식으로
│   ├── color.md
│   ├── typography.md
│   ├── spacing.md
│   ├── radius.md
│   ├── elevation.md
│   └── motion.md
│
└── components/                     ← 컴포넌트별 사양 (24종)
    ├── README.md                   · 컴포넌트 인덱스
    ├── button.md
    ├── badge.md
    ├── chip.md
    ├── text-field.md
    ├── avatar.md
    ├── checkbox-radio-toggle.md
    ├── list-item.md
    ├── alert-toast.md
    ├── progress-slider.md
    ├── tabs-segment.md
    ├── card.md
    ├── asset-icon.md
    ├── border-divider.md
    ├── bar-chart.md
    ├── dialog.md
    ├── bottom-sheet.md
    ├── popover-tooltip.md
    ├── top-app-bar.md
    ├── tab-bar.md
    ├── drawer-breadcrumb.md
    ├── skeleton-loader.md
    ├── empty-state.md
    ├── data-table.md
    └── accordion-tree.md
```

## 어디서 시작해야 하나요

| 질문 | 바로 가기 |
| --- | --- |
| 디자인시스템이 뭐예요? | [docs/00-overview.md](docs/00-overview.md) |
| 지키는 원칙은? | [docs/01-principles.md](docs/01-principles.md) |
| 토큰은 어떻게 구성되나요? | [docs/02-token-architecture.md](docs/02-token-architecture.md) |
| 이름은 어떻게 붙이나요? | [docs/03-naming-conventions.md](docs/03-naming-conventions.md) |
| 그라데이션 써도 되나요? | [docs/04-gradient-policy.md](docs/04-gradient-policy.md) |
| 화면의 문구는 어떻게? | [docs/05-ux-writing.md](docs/05-ux-writing.md) |
| 실제 컬러 값이 궁금해요 | [tokens/primitives.json](tokens/primitives.json) |
| 컴포넌트 목록이 보고 싶어요 | [components/README.md](components/README.md) |
| 뭐가 바뀌었나요? | [CHANGELOG.md](CHANGELOG.md) |
| 시각 쇼케이스를 보고 싶어요 | [UIUX-DH-design-system.html](UIUX-DH-design-system.html) |

## 이 저장소를 유지하는 방법

1. **원본 HTML은 정본입니다.** 시각 예시가 필요하면 원본에서 먼저 확인합니다.
2. **분할 문서는 살아있습니다.** 의미/정책/토큰이 변경되면 분할 문서와 토큰 JSON을 함께 갱신합니다.
3. **변경은 [CHANGELOG.md](CHANGELOG.md)에 기록합니다.** 과거는 지워지지 않고 누적됩니다.
4. **새 컴포넌트는 자체 파일을 가집니다.** `components/` 아래에 추가합니다.
5. AI 작업 시에는 먼저 [CLAUDE.md](CLAUDE.md)를 읽습니다.

## 라이선스 & 유지

MAINTAINED BY /DH · 2026
