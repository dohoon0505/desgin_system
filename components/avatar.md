---
component: Avatar
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5354-L5403
---

# Avatar

> 얼굴이 없는 경우 이니셜 2자, 솔리드 배경. 아바타 색은 이름을 해시해 결정하면 같은 사람이 항상 같은 색을 갖습니다.

## 크기 (5단계)

| Size | px |
| --- | --- |
| `sz-xs` | 24 |
| `sz-sm` | 32 |
| `sz-md` | 40 |
| `sz-lg` | 56 |
| `sz-xl` | 72 |

## 변형

### Solid · `av-solid` (v0.3 권장)

단색 배경 + 이니셜. 이름 해시로 결정적 컬러.

### Legacy · `avatar` (v0.2의 그라데이션)

그라데이션 배경. v0.3에서 **레거시** 로 유지 (신규 사용 비권장). 이유: [../docs/04-gradient-policy.md](../docs/04-gradient-policy.md).

### Status ring · online indicator

아바타 우측 하단 작은 원.

- 초록 — 온라인
- 호박 — 자리비움
- 빨강 — 방해금지
- 그레이 — 오프라인

### Stack · group

협업자·참여자. 최대 4명까지 보여주고 나머지는 `+N` 숫자.

```
(DH)(JK)(SP)(ML)(+12)
```

## 토큰

```
--cm-avatar-bg     → /* 이름 해시로 결정된 --p-* 값 */
--cm-avatar-ring   → var(--sm-background-default)
--cm-avatar-status → var(--sm-status-*)
```

## 이미지 fallback

- 1순위: 사용자 업로드 이미지
- 2순위: 이니셜 2자 + 결정적 배경색
- 3순위: 기본 아이콘 (사용자 사일로)

## 접근성

- `alt` 속성으로 이름 포함 (`alt="Designer DH"`).
- 상태 링은 별도 `aria-label` 또는 sibling 텍스트 필요 ("온라인" 등).
