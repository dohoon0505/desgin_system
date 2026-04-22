---
component: Tab Bar
category: Navigation
since: 0.3.0
version: 0.3.2
sourceHtml: index.html#tabbar
---

# Tab Bar

> 앱 전체의 최상위 이동 수단. **3~5개, 항상 같은 위치, 항상 같은 순서.** 비활성은 outline 아이콘, 활성은 fill 아이콘 — UIUX-DH Icon Package의 쌍 구조를 따릅니다.

## 언제 사용하나

- 모바일 앱의 최상위 네비게이션
- 서로 **동등한 우선순위**의 섹션 이동

## 언제 쓰지 않나

- 3개 미만 → 탭이 낭비됨, 버튼으로 해결
- 6개 이상 → 너무 많음. 드로어 또는 탐색 구조 재검토
- 한 섹션 안의 하위 네비게이션 → [Tabs](tabs-segment.md)

## 표준 구조 (5탭 예시)

```
┌────────────────────────────────────────┐
│ 디데이  다이어리   홈    스토어  마이페이지 │
│  [📅]   [☻]     [🏠]   [🛒]    [👤]   │
└────────────────────────────────────────┘
  outline  outline  FILL  outline  outline
                     ^ 활성 (브랜드 컬러)
```

각 아이템의 구성 (always 세로 스택):

1. 아이콘 (24×24) — 비활성 `outline`, 활성 `fill`
2. 라벨 (짧은 명사, 한 단어)

## 활성/비활성 상태

| 상태 | 아이콘 | 텍스트 색 | 아이콘 색 |
| --- | --- | --- | --- |
| **Active** | `#i-<name>-fill` | `--sm-content-brand` · 700 | `--sm-content-brand` |
| **Inactive** | `#i-<name>` (outline) | `--sm-content-tertiary` · 500 | `--sm-content-tertiary` |
| **Pressed** | — | opacity 0.6, 80ms | — |

**한 번에 하나만 활성** — 5개 중 1개만 `-fill` 변형을 사용합니다.

## 아이콘 네이밍 (UIUX-DH Icon Package v1)

디데이 → `i-calendar` / `i-calendar-fill`
다이어리 → `i-diary` / `i-diary-fill`
홈 → `i-home` / `i-home-fill`
스토어 → `i-cart` / `i-cart-fill`
마이페이지 → `i-user` / `i-user-fill`

이모지 사용은 **금지**입니다. 반드시 아이콘 패키지의 심볼 사용.

## 강조된 가운데 탭 (FAB 스타일 · 예외)

```
┌─────────────────────────────────┐
│  홈    검색   [+]   알림  프로필   │
│                                  │
└─────────────────────────────────┘
                ^
         원형 FAB, 브랜드 컬러
```

"새로 만들기" 같은 강한 액션을 중앙에 강조. 5탭 중 1개 자리를 FAB로 치환.

## 규칙

- **항상 같은 위치**: 화면 하단 고정 (safe-area-bottom 존중)
- **항상 같은 순서**: 사용자가 근육 기억으로 이동
- **한 번에 하나만 활성**
- iOS/Android 모두 Safe Area inset 적용
- **라벨은 항상 표시** — 아이콘만 사용 금지

## 토큰

```
--cm-tabbar-bg              → var(--sm-background-default)
--cm-tabbar-border          → var(--sm-border-subtle)
--cm-tabbar-height          : 56px (+ safe-area-inset-bottom)
--cm-tabbar-content         → var(--sm-content-tertiary)
--cm-tabbar-content-active  → var(--sm-content-brand)
```

## 접근성

- `role="tablist"` + 각 항목 `role="tab"` + 해당 화면 `role="tabpanel"`.
- 활성 항목 `aria-selected="true"` 또는 `aria-current="page"`.
- 각 아이콘 버튼에 텍스트 라벨 포함 (아이콘만으로 의미 전달 금지).
- 터치 영역 최소 44×44px.

## UX Writing

라벨은 **짧은 명사**. 동사가 아닙니다.

| ❌ | ✅ |
| --- | --- |
| 홈으로 | 홈 |
| 메시지 보기 | 메시지 |
| 내 정보 관리 | 마이페이지 |
