---
component: Top App Bar
category: Navigation
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L6006-L6059
---

# Top App Bar

> 화면의 제목과 주요 액션이 모이는 곳. **뒤로가기는 항상 왼쪽 첫 번째, 주요 액션은 오른쪽 마지막.**

## 변형

### Standard · with back

```
┌────────────────────────────────┐
│ [‹ 뒤로]   설정        [🔍 검색]  │
└────────────────────────────────┘
```

- 좌: 뒤로가기 icon button
- 중앙: 화면 타이틀 (기본은 좌측 정렬)
- 우: 주요 icon action(s)

### Centered · modal-like

```
┌────────────────────────────────┐
│ [× 닫기]   계좌 추가     [? 도움]│
└────────────────────────────────┘
```

모달성 플로우(계좌 추가·폼 작성). 제목이 중앙 정렬, 좌측은 닫기(×).

### Large title · home level

```
┌────────────────────────────────┐
│                    [알림][프로필]│
│                                │
│ 홈                              │
└────────────────────────────────┘
```

- 최상위 화면에서 사용
- 큰 타이틀(`display-sm` ~ `heading-lg`)
- 스크롤 시 타이틀이 작아지며 상단 고정

## 레이아웃 규칙

- 높이: 표준 56px, Large 120~160px
- 좌우 패딩: `--size-400` (16px)
- icon button 크기: 44×44 터치 영역

## 토큰

```
--cm-appbar-bg       → var(--sm-background-default)
--cm-appbar-border   → var(--sm-border-subtle)  /* 스크롤 시 표시 */
--cm-appbar-title    → var(--sm-content-primary)
--cm-appbar-icon     → var(--sm-content-primary)
--cm-appbar-height   : 56px
--cm-appbar-height-lg: 120px
```

## 접근성

- `role="banner"` 또는 `<header>` 요소 사용.
- 모든 icon button은 `aria-label` 필수 ("뒤로", "검색", "닫기", "프로필" 등).
- 뒤로가기는 하드웨어/제스처 백과 **동일 동작**을 하도록.

## 스크롤 동작

- 기본: `position: sticky` + `backdrop-filter: blur(12px)`
- Large title: 스크롤에 따라 축소 — `--motion-base` + `--ease-standard`
- 경계선(`border-bottom`)은 스크롤이 있을 때만 표시 (top 상태에서는 투명)
