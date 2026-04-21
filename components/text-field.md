---
component: Text Field
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5260-L5349
---

# Text Field

> 입력은 앱에서 가장 위험한 순간입니다. 레이블은 항상 필드 위, 도움말은 항상 아래, 에러는 즉시. 포커스 링은 시각적으로 분명해야 합니다.

## 언제 사용하나

- 단일 행 텍스트 입력
- 이메일, 비밀번호, 전화번호, 금액, URL 등 형식화된 입력
- 검색 (pill 변형)

## 언제 쓰지 않나

- 여러 줄 입력 → Textarea (별도)
- 선택지가 한정된 입력 → [Radio](checkbox-radio-toggle.md) · Select

## 변형

### Default

```
┌─────────────┐
│ Label *     │
│ ┌─────────┐ │
│ │ input   │ │
│ └─────────┘ │
│ helper text │
└─────────────┘
```

- `field-label` 필드 위
- `field-input` 입력
- `field-help` 필드 아래 (도움말 또는 에러)
- `req` — 빨간 별표 `*` (필수 표시, 단어 아님)
- `opt` — "(선택)" 텍스트

### Affix · prefix & suffix

단위·도메인 같은 고정 요소는 필드 **내부에** 배치해 입력 폭을 아낍니다.

- `https://` prefix + URL 입력
- 숫자 입력 + `원` suffix

### Amount · large numeric

금액 입력은 화면 전체를 차지할 수 있습니다. 타이포그래피 자체가 UI가 됩니다.

### Search · pill

`radius-full` + 돋보기 아이콘. 리스트 상단 상단 고정 검색.

## 상태

- **Rest**: `border-default`
- **Focus**: `border-focus` + 4px `interactive-brand-subtle` glow
- **Error**: `border-error` + 에러 아이콘 + 아래 도움말에 에러 내용
- **Disabled**: opacity 낮춤, 커서 not-allowed

## 토큰

```
--cm-input-bg          → var(--sm-background-default)
--cm-input-border      → var(--sm-border-default)
--cm-input-border-focus → var(--sm-border-focus)
--cm-input-border-error → var(--sm-status-error)
--cm-input-content     → var(--sm-content-primary)
--cm-input-placeholder → var(--sm-content-tertiary)
```

## 접근성

- `<label>`은 `for`로 `<input id>`와 연결.
- 에러 메시지는 `aria-describedby`로 input과 연결.
- 필수 필드는 `aria-required="true"`.
- 자동완성에 맞는 `autocomplete` 속성 지정 (`email`, `tel`, `current-password` 등).

## UX Writing

| ❌ | ✅ |
| --- | --- |
| (필수) | `*` (빨간 별표) |
| 올바른 이메일을 입력해주세요 | `'@' 기호가 빠진 것 같아요` |

정확히 무엇이 문제인지 짚어줍니다. 자세히: [../docs/05-ux-writing.md](../docs/05-ux-writing.md).
