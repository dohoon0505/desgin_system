---
component: Chip
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5145-L5255
---

# Chip

> 가볍고 빠른 선택 단위. 필터 · 카테고리 · 태그 · 선택 상태. 버튼보다 작고, 뱃지보다 상호작용이 많습니다.

## 언제 사용하나

- 필터 (여러 개 동시 선택 가능)
- 카테고리 선택 (단일 / 다중)
- 적용된 조건을 표시 (제거 가능)
- 상태 표시 with dot
- 사람 멘션 (아바타 포함)

## 언제 쓰지 않나

- 주요 액션 → [Button](button.md)
- 순수 정보 표시만 → [Badge](badge.md)

## 변형

### Filter · category

기본 칩. 선택 시 브랜드 tonal 배경, 테두리 강조.

### Tonal · soft emphasis

배경이 brand subtle, 선택 시 더 진함. 카테고리 시각 그룹에 적합.

### Removable · filter chip

`X` 아이콘 탭 시 즉시 제거. 적용된 조건을 한눈에 보여줍니다.

### Dot · status indicator

- 초록 — 온라인
- 호박 — 자리비움
- 빨강 — 방해금지
- 그레이 — 오프라인

### Avatar chip · mention

이니셜 2자 아바타 + 이름. 팀 멘션·협업자 표시.

## 크기

- `chip-sm` — Small
- `chip` (default) — Medium
- `chip-lg` — Large

## 토큰

```
--cm-chip-bg           → var(--sm-background-muted)
--cm-chip-bg-selected  → var(--sm-interactive-brand-subtle)
--cm-chip-border       → var(--sm-border-subtle)
--cm-chip-content      → var(--sm-content-secondary)
--cm-chip-content-sel  → var(--sm-content-brand)
```

## 접근성

- 선택 상태는 `aria-pressed="true"`.
- 제거 버튼은 별도 focus-target, `aria-label="제거"` 포함.
- 도트만으로 상태를 구분하지 않고 텍스트 병용 ("온라인" 등).
