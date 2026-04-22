---
component: Tabs · Segment
canonical: "tabs-segment.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5701-L5738
---

# Tabs · Segment

> 두 컴포넌트는 **역할이 다릅니다.**

| | Tabs | Segment |
| --- | --- | --- |
| 용도 | 서로 다른 콘텐츠 전환 | 같은 데이터의 다른 시각 |
| 개수 | 2~5개 권장 | 2~4개 권장 |
| 시각 | 인라인 언더라인 | 그룹된 pill |
| 예시 | "개요 / 활동 / 설정" | "일간 / 주간 / 월간" |

## Tabs · content section

동일한 레벨의 서로 다른 콘텐츠 영역을 전환. 하단에 컨텐츠가 렌더링됩니다.

```
┌─────────────────────────────┐
│ 개요   활동   설정   보관함    │
│ ────                          │
├─────────────────────────────┤
│ (선택된 탭의 콘텐츠)           │
└─────────────────────────────┘
```

- 활성 탭: 하단 2px 브랜드 라인 + `content-primary` 색
- 비활성: `content-secondary` 색, 라인 없음

## Segment · view switcher

**같은 데이터**의 다른 보기. 차트 viewing 단위, 정렬 방식 등.

```
┌───────────────────────────┐
│ [일간] 주간  월간  연간     │
└───────────────────────────┘
```

- 배경은 `background-muted` (pill 그룹)
- 활성 segment: `background-default` + `elevation-1` (떠 있는 느낌)

## 토큰

```
/* Tabs */
--cm-tabs-content-default → var(--sm-content-secondary)
--cm-tabs-content-active  → var(--sm-content-primary)
--cm-tabs-line-active     → var(--sm-interactive-brand-default)

/* Segment */
--cm-segment-bg         → var(--sm-background-muted)
--cm-segment-item-bg-active → var(--sm-background-default)
--cm-segment-content-active → var(--sm-content-primary)
```

## 접근성

- Tabs: `role="tablist"` + 각 탭 `role="tab"` + 콘텐츠 `role="tabpanel"`, 화살표 키로 이동.
- Segment: `role="radiogroup"` (단일 선택이므로) + 각 segment `role="radio"`.
- 활성 상태는 `aria-selected="true"` 또는 `aria-checked="true"`.
