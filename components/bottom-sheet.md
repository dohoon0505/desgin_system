---
component: Bottom Sheet
canonical: "bottom-sheet.schema.json"
category: Overlays
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5902-L5958
---

# Bottom Sheet

> 모바일에서 가장 **자연스러운 오버레이**. 아래에서 올라오고, 엄지로 닫기 편합니다. Dialog보다 가볍고, Drawer보다 맥락적입니다.

## 언제 사용하나

- **선택지 제공** — 정렬 방식, 공유 옵션
- **맥락적 폼** — 필터 설정, 빠른 댓글
- **모바일 주요 액션** — Dialog의 모바일 대체

## 언제 쓰지 않나

- 강제 결정 확인 → [Dialog](dialog.md)
- 긴 콘텐츠 → 별도 페이지
- 데스크톱 전용 UI → [Popover](popover-tooltip.md)

## 구조

```
┌──────────────────┐
│                  │
│   (배경 화면)      │
│                  │
├─── (스크림) ──────┤
│ ──               │ ← handle (드래그로 닫기 가능)
│ 정렬 방식         │ ← title
│ ● 최근 수정한 순  │
│   만든 순서대로   │
│   이름 순         │
│   즐겨찾기 먼저   │
│                  │
│   [적용하기]      │
└──────────────────┘
```

- 상단 **핸들** (작은 수평 바): 드래그 가능함을 알림
- 상단 모서리만 `radius-2xl` (28px), 하단 모서리는 각짐

## 상호작용

- **아래로 드래그** → 닫힘
- **배경(스크림) 탭** → 닫힘
- **내용 스크롤** → 시트만 스크롤 (배경 고정)
- 다단계 높이 지원 가능: peek / full

## 토큰

```
--cm-sheet-surface → var(--sm-surface-default)
--cm-sheet-handle  → var(--sm-border-default)
--cm-sheet-overlay → rgba(0, 0, 0, 0.5)
--cm-sheet-radius  → var(--radius-2xl)   /* 28px */
```

## 접근성

- `role="dialog"` + `aria-modal="true"`.
- 제목과 연결: `aria-labelledby`.
- ESC 키로 닫기.
- 핸들은 스크린리더 사용자도 닫기 가능해야 하므로 **별도 close button** 제공 권장.
- 배경 스크롤 잠금 + 포커스 트랩.

## 모션

- 등장: `--motion-slow` (320ms) + `--ease-emphasized`
- 닫힘: `--motion-base` (200ms) + `--ease-accelerate`
