---
component: Skeleton Loader
canonical: "skeleton-loader.schema.json"
category: States
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L6197-L6235
---

# Skeleton Loader

> 로딩 중에 "텅 빈 화면"이 아니라 **"곧 채워질 그림자"**를 보여줍니다. 사용자는 기다리는 동안에도 맥락을 유지합니다.

## 언제 사용하나

- 네트워크 로딩 중 (**500ms 이상 지연**이 예상될 때)
- 리스트·카드 초기 로드
- 페이지 진입 직후의 비어 있는 구조

## 언제 쓰지 않나

- 로딩이 **300ms 미만**일 것으로 예상 → 즉시 콘텐츠
- 정확한 진행률을 보여야 함 → [Progress](progress-slider.md)
- 사용자의 명시적 액션 대기 → Spinner / 작은 로더

## 핵심 규칙

**Skeleton은 실제 콘텐츠의 구조를 따라야 합니다.**

카드가 3줄 텍스트라면 스켈레톤도 3줄. 실제보다 복잡하거나 단순하면 **레이아웃이 튑니다**.

## 구조 예시

```
┌──────────────────────────┐
│ ⬤  ▭▭▭▭▭▭▭              │   ← circle 아바타 + 제목 라인
│    ▭▭▭▭                  │   ← 메타 라인
│                          │
│ ▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭    │   ← 본문 1
│ ▭▭▭▭▭▭▭▭▭▭▭▭▭        │   ← 본문 2
│ ▭▭▭▭▭▭▭▭▭            │   ← 본문 3
└──────────────────────────┘
```

- 원형: `circle` (아바타 자리)
- 직사각형: 라인 높이에 맞춤 (텍스트는 10~16px, 제목은 14~18px)
- 큰 사각: 이미지 자리 (`radius-md`)

## 토큰

```
--cm-skeleton-bg      → var(--sm-background-muted)
--cm-skeleton-shimmer → linear-gradient(
                          90deg,
                          transparent,
                          var(--sm-background-default) 50%,
                          transparent
                        )
--cm-skeleton-radius  → var(--radius-sm)
```

## 모션

쉬머(shimmer) 애니메이션 — 좌→우 이동 그라데이션. **예외적으로 허용되는 장식 애니메이션** (로딩 상태 표시가 목적이므로).

- 주기: 1.5s
- 무한 반복 (`animation-iteration-count: infinite`)
- `prefers-reduced-motion: reduce`에서는 정적 회색으로 표시

## 접근성

- `role="status"` + `aria-busy="true"`.
- 스크린리더에는 "콘텐츠를 불러오고 있어요" 같은 `aria-label`.
- 로딩 완료 시 skeleton 제거 후 실제 콘텐츠로 교체 → `aria-busy="false"`.
