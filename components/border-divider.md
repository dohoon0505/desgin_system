---
component: Border · Divider
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L4991-L5058
---

# Border · Divider

> 경계는 **정보의 틀**입니다. 네 가지 강도의 경계선과 세 가지 구분선 패턴이 콘텐츠의 계층을 나눕니다.

## Border · 4 intensities

| Token | 강도 | 사용처 |
| --- | --- | --- |
| `--sm-border-subtle` | 가장 약함 | 기본 카드, 분리된 콘텐츠 블록 |
| `--sm-border-default` | 보통 | 입력 필드 rest |
| `--sm-border-strong` | 강함 | 강조 영역, high contrast UI |
| `--sm-border-brand` | 브랜드 | 선택 상태 |
| `--sm-border-focus` | 브랜드 포커스 | 활성 입력 (focus ring) |
| `--sm-status-error` | 에러 | 유효성 실패 입력 |

## Divider · horizontal 패턴

### Default (subtle line)

```
─────────────────────
```

- `height: 1px`
- `background: var(--sm-border-subtle)`

### Strong (섹션 경계)

대화 섹션·그룹 사이.

```
═════════════════════
```

- `background: var(--sm-border-default)`

### Dashed (비고정)

임시 영역, 플레이스홀더.

```
- - - - - - - - - - -
```

### Section (레이블 포함)

```
───── OR ─────
```

좌우 라인 + 중앙 텍스트. 로그인 화면의 "또는" 구분 등에 사용.

## Divider · vertical

수평 리스트의 요소 간 구분.

```
전체 │ 진행 중 │ 완료 │ 보관
```

- `width: 1px`
- `height: 12~16px`
- 색은 `border-subtle`

## 토큰

위의 `--sm-border-*` 시맨틱 토큰을 그대로 사용. 별도 컴포넌트 토큰 없음.

## 접근성

- Divider는 `role="separator"` + (수직인 경우) `aria-orientation="vertical"`.
- 의미 없는 장식 라인은 CSS로만 그리고 DOM에 포함하지 않음.
