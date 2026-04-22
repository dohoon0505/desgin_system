---
component: Alert · Toast
canonical: "alert-toast.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5553-L5619
---

# Alert · Toast

> Alert는 화면에 머무는 메시지, Toast는 잠시 나타났다 사라지는 메시지. **둘은 목적이 다르며 섞어 쓰지 않습니다.**

| | Alert | Toast |
| --- | --- | --- |
| 수명 | 영구적 (사용자가 닫을 때까지) | 약 3초 |
| 위치 | 인라인 (콘텐츠 안) | 화면 하단 floating |
| 사용 | 중요한 상태·경고·정보 | 작업 결과 피드백 |

## Alert

### 4가지 semantic 타입

| Type | Token | 사용 |
| --- | --- | --- |
| `alert-info` | `--sm-status-info` | 업데이트·팁 |
| `alert-success` | `--sm-status-success` | 저장 성공·완료 |
| `alert-warning` | `--sm-status-warning` | 용량 부족·주의 |
| `alert-error` | `--sm-status-error` | 연결 실패·파괴 |

### 구조

```
┌──────────────────────────┐
│ [icon] Title             │
│        Description text  │
└──────────────────────────┘
```

- Title: 한 줄
- Description: 한두 줄 (무엇·왜·어떻게)

## Toast

- **자동 사라짐**: 3초.
- 위치: 화면 하단 중앙, `z-toast` (1100).
- 변형: 기본 / 성공 (체크 아이콘) / 실패 (빨간 도트 + 재시도 액션)

```
┌──────────────────────────┐
│ ● 링크가 복사되었습니다     │
└──────────────────────────┘
```

## 토큰

```
/* Alert */
--cm-alert-bg-info     → color-mix(--sm-status-info 10%, transparent)
--cm-alert-bg-success  → color-mix(--sm-status-success 10%, transparent)
--cm-alert-bg-warning  → color-mix(--sm-status-warning 10%, transparent)
--cm-alert-bg-error    → color-mix(--sm-status-error 10%, transparent)
--cm-alert-content     → var(--sm-status-*)

/* Toast */
--cm-toast-bg      → var(--p-neutral-100)
--cm-toast-content → var(--p-neutral-0)
--cm-toast-radius  → var(--radius-full)
```

## 접근성

- Alert는 `role="alert"` 또는 `role="status"` (중요도에 따라).
- Toast는 `role="status"` + `aria-live="polite"`.
- 파괴적 Alert는 `aria-live="assertive"` — 스크린리더가 즉시 읽음.
- 자동 사라지는 Toast라도 사용자가 **포커스로 접근 가능**해야 하며, 정지 옵션 필요 (WCAG 2.2).

## UX Writing

| ❌ | ✅ |
| --- | --- |
| 성공하였습니다 | 저장했어요 |
| 오류가 발생했어요. 다시 시도해주세요 | 네트워크가 불안정해요. Wi-Fi를 확인해주세요 |

자세히: [../docs/05-ux-writing.md#컴포넌트별-라이팅-규칙](../docs/05-ux-writing.md).
