---
component: Dialog
canonical: "dialog.schema.json"
category: Overlays
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5836-L5897
---

# Dialog

> Dialog는 사용자의 선택을 **강제로 멈추게** 합니다. 결정 없이는 되돌아갈 수 없어야 할 때만 씁니다. 남용하면 신뢰를 잃습니다.

## 언제 사용하나

- **파괴적 액션 확인** — 삭제, 결제, 되돌릴 수 없는 변경
- **저장되지 않은 작업 경고** — 나가기 전 확인
- **시스템 완료 알림** — 송금 성공 같은 중요한 완료

## 언제 쓰지 않나

- 단순 알림 → [Toast](alert-toast.md)
- 모바일의 선택지 제공 → [Bottom Sheet](bottom-sheet.md)
- 정보 열람 → Card 또는 별도 페이지

## 변형

### Confirm · destructive

```
┌───────────────────────────────┐
│ 삭제한 프로젝트는 복구할 수 없어요 │
│                               │
│ '디자인시스템 v0.3' 프로젝트와 포함된│
│ 12개의 파일이 함께 삭제돼요.      │
│                               │
│         [닫기]   [삭제하기]    │
└───────────────────────────────┘
```

- **왼쪽 = 안전한 액션** ("닫기")
- **오른쪽 = 위험한 액션** (`btn-danger` "삭제하기")

### Success · completion

```
┌────────────────────────────┐
│           [✓]               │
│                            │
│  송금을 완료했어요           │
│  김디자이너 님에게 320,000원│
│  을 보냈어요.               │
│                            │
│         [확인]              │
└────────────────────────────┘
```

- 상단 원형 아이콘 (`--sm-status-success` 배경)
- 단일 버튼 full-width

### Warning · attention required

```
┌────────────────────────────┐
│           [!]               │
│                            │
│  저장하지 않고 나갈까요?     │
│  작성한 내용이 사라져요.     │
│                            │
│     [나가기]  [저장하기]    │
└────────────────────────────┘
```

- 상단 원형 아이콘 (`--sm-status-warning` 배경)

## 토큰

```
--cm-dialog-surface  → var(--sm-surface-default)
--cm-dialog-overlay  → rgba(0, 0, 0, 0.5)
--cm-dialog-radius   → var(--radius-xl)
--cm-dialog-shadow   → var(--elevation-4)
--cm-dialog-max-width: 360px
```

## 접근성

- `role="dialog"` + `aria-modal="true"`.
- `aria-labelledby`로 제목과 연결.
- 열릴 때 **첫 focusable 요소**로 포커스 이동, 닫힐 때 **트리거 요소**로 복귀.
- `ESC` 키로 닫기 지원 (단, 데이터 유실 위험이 있으면 확인 후 닫기).
- 배경 스크롤 잠금.

## UX Writing

제목은 **결과나 질문**으로. "주의!" 같은 감탄사로 시작하지 않습니다.

| 컴포넌트 | ❌ | ✅ |
| --- | --- | --- |
| 왼쪽 버튼 | 취소 | 닫기 |
| 오른쪽 버튼 | 확인 · OK | 삭제하기 · 나가기 · 저장하기 |

'취소'는 지금까지 한 작업이 취소될까 봐 사용자가 망설입니다. 자세히: [../docs/05-ux-writing.md](../docs/05-ux-writing.md).
