---
component: Button
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5063-L5140
---

# Button

> 화면마다 Primary 버튼은 한 개가 원칙. 터치 영역은 최소 44×44px, 라벨은 동사로 시작하며 결과를 담습니다.

## 언제 사용하나

- 사용자가 **한 번에 결정 가능한** 액션을 실행할 때
- 화면에 가장 중요한 행동을 강조할 때 (Primary 1개)

## 언제 쓰지 않나

- 탐색 전용(링크가 맞습니다)
- 토글 설정(Toggle 컨트롤 사용)
- 여러 옵션 중 하나 선택(Radio · Chip)

## 변형 (Variants)

| 이름 | 시각 | 언제 |
| --- | --- | --- |
| `primary` | 솔리드 브랜드 | 화면의 메인 액션. **1개 원칙.** |
| `tonal` | 브랜드 subtle | Primary보다 약한 권장 액션 |
| `secondary` | 중립 솔리드 | 보조 액션 |
| `outline` | 테두리만 | 주의를 덜 끄는 액션 |
| `ghost` | 배경·테두리 없음 | 밀도 높은 목록·AppBar 내부 |
| `dark` | 짙은 배경 | 다크 카드 내부 |
| `danger` | 에러 컬러 | 파괴적 액션 전용. 확인 필수. |

## 크기 (Sizes)

`btn-sm` · `btn-md` · `base` · `btn-lg` · `btn-xl` — 5단계.

## 모양 (Shape)

- 표준 `radius-md`
- `btn-pill` — `radius-full`, 시작하기·CTA 스타일
- `btn-icon` — 정사각 아이콘 버튼 (44×44 이상)
- `btn-fab` — 플로팅 액션 버튼 (원형)

## 상태 (States)

rest · hover · active · focus · disabled · loading.

- Hover: `--sm-interactive-brand-hover`
- Active: `--sm-interactive-brand-active`
- Disabled: opacity 낮춤, pointer-events: none

## 토큰 (Component Tokens)

```
--cm-button-primary-bg        → var(--sm-interactive-brand-default)
--cm-button-primary-bg-hover  → var(--sm-interactive-brand-hover)
--cm-button-primary-bg-active → var(--sm-interactive-brand-active)
--cm-button-primary-content   → var(--sm-content-onBrand)

--cm-button-danger-bg         → var(--sm-status-error)
--cm-button-danger-content    → var(--sm-content-onBrand)
```

전체 참조: [../tokens/semantic.light.json](../tokens/semantic.light.json)

## 접근성 (Accessibility)

- **터치 영역 최소 44×44px.** 시각적으로 작아도 padding으로 확보합니다.
- 모든 icon-only 버튼은 `aria-label` 필수.
- 포커스 링은 `--sm-border-focus` 2px + 4px offset box-shadow.

## UX Writing

라벨은 **결과를 담는 동사**.

| ❌ | ✅ |
| --- | --- |
| 확인 | 저장하기 |
| 완료 | 결제하기 |
| OK | 신청하기 |

자세한 규칙: [../docs/05-ux-writing.md#principle-05--버튼-라벨은-결과를-담는다](../docs/05-ux-writing.md).

## Full-width CTA

화면 하단 고정 버튼은 `btn-full btn-lg`. 모바일에서 가장 자주 쓰이는 형태.
