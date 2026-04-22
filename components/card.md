---
component: Card
canonical: "card.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5743-L5821
---

# Card

> 카드는 나머지 모든 컴포넌트를 담는 그릇입니다. **최소한의 장식**으로, 내용이 주인공이 되게 합니다.

## 기본 구조

```
┌──────────────────────────┐
│ Head                     │
│   Title                  │
│   Sub                    │
├──────────────────────────┤
│ Body                     │
│   (숫자, 리스트, 차트 등)  │
├──────────────────────────┤
│ Foot (optional)          │
│   [Action Button]        │
└──────────────────────────┘
```

- 최소: `padding: size-500` (20px)
- 기본 radius: `--radius-lg` (14px)
- 기본 elevation: `--elevation-0` (border로만 경계), hover 시 `elevation-1`

## 변형

### Dashboard 카드 (composition example)

앞서 만든 컴포넌트들이 실제로 어떻게 조합되는지의 예시:

- **지출 카드**: 제목 + badge-success + 큰 숫자 + progress bar
- **팀 카드**: 제목 + avatar-stack + 초대 버튼
- **배송 카드**: 제목 + badge-brand + 단계 체크리스트 + 조회 버튼

## 토큰

```
--cm-card-bg       → var(--sm-surface-default)
--cm-card-border   → var(--sm-border-subtle)
--cm-card-radius   → var(--radius-lg)
--cm-card-shadow   → var(--elevation-0)
--cm-card-shadow-hover → var(--elevation-1)
```

## 결정 가이드

| 상황 | 선택 |
| --- | --- |
| 한 개의 정보 덩어리 | Card |
| 여러 개의 비슷한 행 | [List Item](list-item.md) |
| 강제 결정이 필요 | [Dialog](dialog.md) |
| 잠시 나타나는 메시지 | [Alert · Toast](alert-toast.md) |

## 접근성

- 카드 전체가 클릭 가능하면 `<a>` 또는 `role="button"`, 단일 focus-target.
- 내부에 여러 액션이 있으면 **카드 자체는 non-interactive**로 두고 버튼 각각에 focus.
- 카드의 의미를 제목으로 설명 — `<h3>` 또는 적절한 heading level 사용.
