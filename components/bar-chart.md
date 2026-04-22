---
component: Bar Chart
canonical: "bar-chart.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L4901-L4986
---

# Bar Chart

> 데이터는 주인공입니다. 차트 자체는 최소화하고, **값과 위계**가 두드러지게 합니다.

## 세 가지 기본형

### Vertical · time series

시간에 따른 변화. 강조하고 싶은 값(예: 이번 달)은 브랜드 컬러로 높입니다.

```
                ▉
            ▉   ▉
        ▉   ▉   ▉
    ▉   ▉   ▉   ▉   ▉
▉   ▉   ▉   ▉   ▉   ▉   ▉
Jan Feb Mar Apr May Jun Jul
```

- 과거: `interactive-brand-subtle`
- 현재/강조: `interactive-brand-default`

### Horizontal · ranking

카테고리 간 비교. **값이 큰 순서로 정렬**해 상위 항목이 먼저 보이게 합니다.

```
식비  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓   ₩482K
교통  ▓▓▓▓▓▓▓▓▓           ₩318K
쇼핑  ▓▓▓▓▓▓▓             ₩221K
문화  ▓▓▓▓▓               ₩142K
의료  ▓▓▓                 ₩67K
```

### Stacked · composition

전체를 구성하는 부분의 비율. **한 줄에 담아** 여백을 아낍니다.

```
예산 배분 · 이번 달              ₩1,230,000
┌─────────┬─────┬────┬─────┐
│식비 42% │교통 │쇼핑│기타 │
└─────────┴─────┴────┴─────┘
```

세그먼트 컬러는 같은 `indigo` 스케일에서 500 → 200으로 단계적 사용 (같은 색상군, 명도만 다름).

## 토큰

```
--cm-chart-bar-default → var(--sm-interactive-brand-subtle)
--cm-chart-bar-active  → var(--sm-interactive-brand-default)
--cm-chart-axis        → var(--sm-content-tertiary)
--cm-chart-grid        → var(--sm-border-subtle)
```

## 접근성

- 차트는 SVG + `<title>` / `<desc>`로 스크린리더 설명.
- 데이터 테이블 `<table>`을 **대체 시각 표현**으로 함께 제공.
- 색만으로 범례를 구분하지 않음 — 라벨·패턴 병용.
- motion 애니메이션은 `prefers-reduced-motion` 존중.

## 스타일 원칙

- 격자선 최소화 (또는 제거)
- 축은 필요한 최소 정보만 (첫/끝 값만 표시 등)
- 숫자는 항상 `font-variant-numeric: tabular-nums` (자릿수 정렬)
