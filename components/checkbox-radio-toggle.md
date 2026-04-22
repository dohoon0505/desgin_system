---
component: Checkbox · Radio · Toggle
canonical: "checkbox-radio-toggle.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5408-L5481
---

# Checkbox · Radio · Toggle

> 세 컨트롤은 **역할이 다릅니다.** 섞어 쓰면 사용자가 혼란을 느낍니다.

| 컨트롤 | 용도 | 복수 선택 | 즉시 적용 |
| --- | --- | --- | --- |
| Checkbox | 여러 개 중 선택 | ✅ | ❌ (저장 버튼 필요) |
| Radio | 여러 개 중 하나 | ❌ | ❌ |
| Toggle | 설정 켜기/끄기 | — | ✅ (즉시 저장) |

## Checkbox

- 약관 동의, 항목 체크, 필터 다중 선택
- **인디터미네이트 상태** 지원 (부모-자식 트리)

```
☑ 이용약관에 동의합니다
☑ 개인정보 수집에 동의
☐ 마케팅 정보 수신 동의 (선택)
```

## Radio

- 플랜 선택, 옵션 택일
- 같은 `name` 속성 필수 (한 그룹 내 택일)

```
○ 무료 플랜
● Pro 플랜        ← 선택됨
○ Team 플랜
```

## Toggle

- 알림, 다크 모드, 자동 저장 같은 **즉시 적용** 설정
- 탭 즉시 서버 저장·UI 반영. 확인 버튼 없음.

```
알림 받기            ━━●   (on)
다크 모드           ●━━   (off)
자동 저장            ━━●   (on)
```

## 토큰

```
--cm-control-box-bg        → var(--sm-background-default)
--cm-control-box-border    → var(--sm-border-default)
--cm-control-box-bg-on     → var(--sm-interactive-brand-default)
--cm-control-check-content → var(--sm-content-onBrand)

--cm-toggle-track-off → var(--sm-background-muted)
--cm-toggle-track-on  → var(--sm-interactive-brand-default)
--cm-toggle-knob      → var(--sm-background-default)
```

## 접근성

- 각 컨트롤은 `<label>`로 감싸거나 `for` 연결. 라벨 탭으로도 토글되어야 합니다.
- Checkbox `aria-checked` — `true` / `false` / `mixed`.
- Radio group은 `role="radiogroup"` + 방향키 이동.
- Toggle은 즉시 반영되므로 **loading 상태**를 고려 — 네트워크 실패 시 원래 상태로 복원.

## 금지

- Toggle을 **확인 버튼과 함께** 배치 (즉시 적용 원칙 위반)
- Radio를 하나만 두기 (Radio는 **선택지가 2개 이상**)
- Checkbox를 "택일"에 사용
