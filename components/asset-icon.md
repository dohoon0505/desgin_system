---
component: Asset · Icon
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L4746-L4824
---

# Asset · Icon

> 아이콘은 의미 전달의 최소 단위. **24px 그리드 · 1.5px stroke · 둥근 선 끝**이 기본값.

## Icon · 기본 규약

| 속성 | 값 |
| --- | --- |
| Grid | `24 × 24` |
| Stroke width | `1.5px` |
| Stroke linecap | `round` |
| Stroke linejoin | `round` |
| Color | `currentColor` (부모의 color를 상속) |
| Fill | 기본 `none` |

### 기본 아이콘 세트 (예시)

home · search · bell · heart · message · settings · user · wallet · chevron · check · close · plus

### SVG 템플릿

```html
<svg width="24" height="24" viewBox="0 0 24 24"
     fill="none" stroke="currentColor"
     stroke-width="1.5"
     stroke-linecap="round"
     stroke-linejoin="round">
  <!-- path -->
</svg>
```

## Illustration · filled

컬러 필 기반의 장식용 일러스트. 빈 상태, 성공 화면, 온보딩.

- 컬러는 primitive 스케일을 사용 (브랜드 `indigo-500`, 성공 `green-500` 등)
- 다크 모드에서도 동일한 톤을 유지하도록 디자인 (`currentColor` 미사용)

## 토큰

아이콘은 `currentColor` 원칙이므로 별도의 색 토큰이 없습니다. 크기·스트로크만 상수:

```
--cm-icon-size-sm    : 16px
--cm-icon-size-md    : 20px
--cm-icon-size-base  : 24px
--cm-icon-size-lg    : 32px
--cm-icon-stroke     : 1.5
```

## 접근성

- 의미 있는 아이콘: `<svg role="img"><title>라벨</title></svg>` 또는 감싸는 버튼에 `aria-label`.
- 장식 아이콘: `aria-hidden="true"`, 텍스트 라벨이 동반되어야 함.
- 터치 타깃은 아이콘 자체가 아닌 **부모 버튼의 44×44px**로 확보.

## 금지

- 아이콘만 있는 버튼을 `aria-label` 없이 사용
- stroke width를 `1px` 미만으로 하기 (다크에서 사라짐)
- 다크 모드에서 보이지 않는 이슈 — `currentColor` 규약 위반
