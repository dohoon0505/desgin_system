---
component: Badge
canonical: "badge.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L4829-L4896
---

# Badge

> 작지만 강한 시각 신호. 상태 · 카테고리 · 숫자 알림을 전달합니다. 한 화면에 많이 쓰이면 신호의 가치를 잃습니다.

## 언제 사용하나

- 상태 표시 (진행 중, 완료, 실패)
- 카테고리 태그
- 알림 개수 (9 이상은 `99+`로 상한)
- 신규·Hot·Pro 같은 짧은 강조

## 언제 쓰지 않나

- 상호작용이 필요한 경우 → [Chip](chip.md)
- 긴 설명이 필요한 경우 → [Alert](alert-toast.md)

## 변형

### Status · tonal

배경이 subtle한 페일 톤. 가독성 좋고 주변을 방해하지 않습니다.

- `badge-default` — 중립
- `badge-brand` — 신규·강조
- `badge-success` — 완료
- `badge-warning` — 주의
- `badge-error` — 실패
- `badge-info` — 정보

### Solid · emphasis

꽉 찬 배경. 눈에 더 띕니다.

- `badge-solid-brand` — 브랜드 솔리드
- `badge-solid-dark` — 딥톤 (예: "PRO")
- `badge-outline` — 테두리만 (예: "BETA")

### Notification · numeric & dot

아이콘 버튼에 붙는 우측 상단 표시.

- **숫자 뱃지**: `9` 이상일 때 `99+`로 상한.
- **도트 뱃지**: 정확한 개수가 중요하지 않을 때.

## 토큰

```
--cm-badge-notif-bg  → var(--sm-status-error)
--cm-badge-brand-bg  → var(--sm-interactive-brand-subtle)
--cm-badge-content   → var(--sm-content-brand)
```

## 접근성

- 숫자 뱃지는 `aria-label="<count>개의 새로운 알림"` 같은 설명 포함.
- 색만으로 상태를 구분하지 않습니다 — 아이콘 또는 텍스트와 병용.
