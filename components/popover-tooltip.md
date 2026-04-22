---
component: Popover · Tooltip
canonical: "popover-tooltip.schema.json"
category: Overlays
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5963-L6001
---

# Popover · Tooltip

> Tooltip은 **단순 설명**, Popover는 **상호작용 가능한 미니 화면**. 둘의 경계가 모호해지면 둘 다 신뢰를 잃습니다.

| | Tooltip | Popover |
| --- | --- | --- |
| 수명 | hover/focus 시 잠시 | 명시적으로 닫을 때까지 |
| 내용 | 단문 텍스트 | 제목 + 본문 + 버튼 가능 |
| 상호작용 | 없음 (passive hint) | 있음 (버튼, 입력) |
| Trigger | hover · focus · long-press | click · tap |

## Tooltip · passive hint

hover나 long-press 시 잠시 나타나는 설명. 액션 없음.

```
  ┌─────────────────────────┐
  │ Pro 플랜에서만 쓸 수 있어요│
  └──────┬──────────────────┘
         ▼
     [도움말 ?]
```

- 한 문장, 최대 두 줄
- `background: var(--p-neutral-100)` (Light 테마에서도 딥톤)
- `color: var(--p-neutral-0)`

## Popover · interactive

명시적으로 **열고 닫는** 미니 화면. 링크 공유, 프로필 미리보기, 간단한 폼 등.

```
  ┌──────────────────────┐
  │ 공유 링크 만들기       │
  │                      │
  │ 이 문서를 볼 수 있는   │
  │ 링크를 만들어요...     │
  │                      │
  │   [링크 만들기]        │
  └──────────────────────┘
              ▲
         [공유 버튼]
```

- 배경: `surface-default` + `elevation-3`
- 화살표(arrow) 옵션 — 트리거와 연결을 표시

## 토큰

```
/* Tooltip */
--cm-tooltip-bg      → var(--p-neutral-100)
--cm-tooltip-content → var(--p-neutral-0)
--cm-tooltip-radius  → var(--radius-md)

/* Popover */
--cm-popover-surface → var(--sm-surface-raised)
--cm-popover-border  → var(--sm-border-subtle)
--cm-popover-shadow  → var(--elevation-3)
--cm-popover-radius  → var(--radius-lg)
```

## 접근성

### Tooltip
- `role="tooltip"` + 트리거와 `aria-describedby`로 연결.
- 키보드 포커스 시에도 표시되어야 합니다 (hover 전용 금지).
- `ESC` 키로 닫기.

### Popover
- `role="dialog"` 또는 `role="menu"` (내용에 따라).
- 트리거 `aria-expanded="true/false"` + `aria-controls="popover-id"`.
- 열릴 때 포커스 이동, 닫힐 때 트리거로 복귀.
- 바깥 클릭 또는 `ESC`로 닫기.

## 모션

- Tooltip: `--motion-fast` (120ms) fade + scale(0.95→1).
- Popover: `--motion-base` (200ms) + `--ease-standard`.
