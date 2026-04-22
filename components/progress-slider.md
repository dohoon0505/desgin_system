---
component: Progress · Slider
canonical: "progress-slider.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5624-L5696
---

# Progress · Slider

> 진행 상태는 명확한 시각 메타포가 필요합니다. **연속 진행은 Bar**, **단계적 진행은 Segment**, **값 조정은 Slider**.

## Bar · continuous

0~100% 사이의 연속 진행.

```
업로드 중                    65%
▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░
```

- 기본: `--sm-interactive-brand-default`
- 경고 (80% 이상 등): `--sm-status-warning`
- 완료: `--sm-status-success`

**그라데이션 허용**: 같은 색상군의 명도 변화 (예: `indigo-500 → indigo-300`). 정책: [../docs/04-gradient-policy.md](../docs/04-gradient-policy.md).

## Segment · step

단계가 **정해진 흐름** (퀴즈, 온보딩, 다단계 폼).

```
Step 3 of 5
[■][■][■][ ][ ]
```

- 완료 단계: 브랜드 컬러로 채움
- 현재/미래 단계: 중립 subtle

## Slider · range selector

사용자가 값을 조정.

```
예산                    ₩320,000
●───────────○──────────
₩0                   ₩1,000,000
```

- Thumb: `radius-full`, 그림자 `elevation-2`, 드래그 중 `elevation-3`.
- Track: `size-150` height, filled + unfilled 영역.

## 토큰

```
--cm-progress-track → var(--sm-background-muted)
--cm-progress-fill  → var(--sm-interactive-brand-default)

--cm-slider-thumb    → var(--sm-background-default)
--cm-slider-thumb-ring → var(--sm-interactive-brand-default)
--cm-slider-fill     → var(--sm-interactive-brand-default)
```

## 접근성

- Progress: `role="progressbar"` + `aria-valuenow` / `aria-valuemin` / `aria-valuemax`.
- 상태 변화가 중요하면 `aria-live="polite"`로 스크린리더에 알림.
- Slider: `role="slider"` + 동일 aria-value 속성. 키보드 화살표로 조정 가능.
- 색만으로 경고를 표시하지 않음 — 숫자 텍스트도 함께.
