---
component: Data Table
canonical: "data-table.schema.json"
category: Density
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L6316-L6373
---

# Data Table

> 많은 정보를 빠르게 비교할 때. **숫자 컬럼은 오른쪽 정렬 · 탭 고정 폭**, 텍스트 컬럼은 왼쪽 정렬. 정렬 가능한 컬럼은 표시로 알려줍니다.

## 구조

```
┌──────────────┬──────────┬──────┬──────┬───────┐
│ 프로젝트 ▲    │ 담당자    │ 상태  │ 진행률│ 마감  │
├──────────────┼──────────┼──────┼──────┼───────┤
│ Design System│ [DH] DH  │[진행중]│ 72% │ 04.28 │
│ Onboarding   │ [JK] JK  │ [완료]│100% │ 04.20 │
│ Payment v2   │ [SP] SP  │[검토중]│ 45% │ 04.22 │
│ Motion Lib   │ [ML] ML  │ [대기]│  0% │ 05.15 │
└──────────────┴──────────┴──────┴──────┴───────┘
```

## 규칙

- **정렬 가능한 컬럼**은 헤더에 정렬 표시(▲/▼). 현재 정렬 중인 컬럼 강조.
- **텍스트 컬럼**: 왼쪽 정렬.
- **숫자/날짜 컬럼**: 오른쪽 정렬 + `tabular-nums` (자릿수 맞춤 고정폭).
- **상태 컬럼**: 칩 또는 tonal pill로 시각화 (badge와 유사).
- **마감이 임박/지남**: 날짜를 `--sm-status-error` 색 + bold.

## Row 상호작용

- Hover: `--sm-background-muted` 배경
- 전체 행 클릭 가능하면 전체를 focusable 영역으로
- Row actions: 우측 끝에 `⋯` 메뉴 버튼

## 토큰

```
--cm-table-head-bg        → var(--sm-background-subtle)
--cm-table-head-content   → var(--sm-content-secondary)
--cm-table-row-border     → var(--sm-border-subtle)
--cm-table-row-bg-hover   → var(--sm-background-muted)
--cm-table-cell-content   → var(--sm-content-primary)
```

## 밀도 (Density)

| Density | Row height | 사용처 |
| --- | --- | --- |
| Comfortable | 56px | 기본 |
| Compact | 44px | 데이터 집약 화면 (대시보드) |
| Relaxed | 72px | 리딩 우선 |

## 접근성

- `<table>` 시맨틱 요소 사용. `<thead>` / `<tbody>` 구분.
- 정렬 가능 컬럼: `<th aria-sort="ascending | descending | none">`.
- 긴 테이블은 `<caption>`으로 표의 목적 설명.
- 모바일: 좌우 스크롤 허용하되, 첫 컬럼 고정(sticky) 권장.

## 반응형

- 모바일(< 640px): 가로 스크롤 또는 **카드 뷰 전환**
- 컬럼 수가 많으면 우선순위에 따라 일부 컬럼 숨김 허용
