---
component: Drawer · Breadcrumb
category: Navigation
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L6118-L6182
---

# Drawer · Breadcrumb

> Drawer는 **주메뉴 전체**를 담는 측면 패널. Breadcrumb은 현재 위치를 알려주는 **경로**. 둘 다 계층이 깊은 앱에서 빛을 발합니다.

## Drawer

### 언제 사용하나

- 주요 네비게이션을 **숨겨두고 싶을 때** (Tab Bar에 담기에 너무 많을 때)
- 워크스페이스 선택, 사용자 프로필, 설정 등 **부가 진입점**
- 데스크톱 대시보드의 사이드바

### 구조

```
┌────────────────────────┐
│ [DH]  Designer DH       │
│       Pro Plan          │
├────────────────────────┤
│ WORKSPACE               │
│ [▦] 대시보드        (3)  │
│ [▣] 프로젝트       (12)  │
│ [👥] 팀원                │
├────────────────────────┤
│ PREFERENCES             │
│ [⚙] 설정                │
└────────────────────────┘
```

- 상단: 사용자 프로필 블록 (아바타 + 이름 + 부가 정보)
- 그룹: `UPPERCASE` 라벨 + 항목 리스트
- 각 항목: 아이콘 + 텍스트 + 우측 count (선택)

### 상호작용

- 모바일: 좌측 엣지 스와이프 또는 햄버거 버튼으로 열기
- 데스크톱: 고정 사이드바 또는 토글

### 토큰

```
--cm-drawer-surface      → var(--sm-surface-default)
--cm-drawer-item-bg-hover → var(--sm-background-muted)
--cm-drawer-item-bg-active→ var(--sm-interactive-brand-subtle)
--cm-drawer-item-content-active → var(--sm-content-brand)
--cm-drawer-group-label  → var(--sm-content-tertiary)
--cm-drawer-width        : 272px
```

## Breadcrumb

### 언제 사용하나

- 여러 단계 깊이의 페이지
- 사용자가 **어디에 있는지 · 어디로 돌아갈 수 있는지** 보여줘야 할 때

### 구조

```
홈 ▸ 프로젝트 ▸ 디자인시스템 v0.3 ▸ UX Writing Guide
 ↑     ↑              ↑                    ↑
 링크  링크           링크              현재(링크 아님)
```

- 구분자: `▸` 또는 `/`
- 마지막(현재) 항목은 **링크가 아닌 일반 텍스트** — `content-primary`, bold
- 중간 항목은 클릭 가능한 링크 — `content-secondary`

## 접근성

### Drawer
- `role="navigation"` + `aria-label="주 네비게이션"`.
- 열려 있으면 `aria-expanded="true"`, 모달형인 경우 포커스 트랩.
- ESC 키로 닫기.

### Breadcrumb
- `<nav aria-label="경로">` 감싸기.
- `<ol>` 사용 (순서가 의미 있음).
- 현재 페이지에 `aria-current="page"`.

## 모션

- Drawer 등장: 좌측에서 슬라이드 in — `--motion-slow` + `--ease-emphasized`
- Drawer 닫힘: `--motion-base` + `--ease-accelerate`
