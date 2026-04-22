---
component: Asset · Icon
canonical: "asset-icon.schema.json"
category: Components
since: 0.2.0
version: 0.3.2
sourceHtml: index.html#asset
---

# Asset · Icon · UIUX-DH Icon Package v1

> 아이콘은 의미 전달의 최소 단위. **SVG 심볼 스프라이트** 기반의 통합 아이콘 패키지. 이모지 사용은 **전면 금지** — 반드시 이 패키지의 심볼을 사용합니다.

## 기본 규약

| 속성 | 값 |
| --- | --- |
| viewBox | `0 0 24 24` (공통) |
| Stroke width | `1.7px` (outline 기본) · `1.8px` (네비게이션 아이콘) · `2px` (chevron/check/plus) |
| Stroke linecap | `round` |
| Stroke linejoin | `round` |
| Color | `currentColor` (부모의 `color`를 상속) |
| Fill (outline) | `none` |
| Fill (filled) | `currentColor` |

## Usage

아이콘은 HTML 상단의 `<svg>` 심볼 스프라이트에서 `<use>`로 참조합니다.

```html
<!-- 기본 24px outline -->
<svg class="ico"><use href="#i-home"/></svg>

<!-- 크기 변형 -->
<svg class="ico ico-sm"><use href="#i-home"/></svg>   <!-- 16px -->
<svg class="ico ico-md"><use href="#i-home"/></svg>   <!-- 20px -->
<svg class="ico ico-lg"><use href="#i-home"/></svg>   <!-- 28px -->
<svg class="ico ico-xl"><use href="#i-home"/></svg>   <!-- 40px -->

<!-- Filled 변형 (Tab Bar 활성 상태 등 강조용) -->
<svg class="ico"><use href="#i-home-fill"/></svg>

<!-- 색상 — 부모의 color를 상속 -->
<span style="color: var(--sm-status-error);">
  <svg class="ico"><use href="#i-heart-fill"/></svg>
</span>
```

## 아이콘 카테고리

### Navigation (Tab Bar) — outline + fill 쌍

탭바 비활성 탭에는 outline, 활성 탭에는 `-fill` 변형을 사용합니다.

| 의미 | outline | filled |
| --- | --- | --- |
| D-day · 달력 | `i-calendar` | `i-calendar-fill` |
| 다이어리 | `i-diary` | `i-diary-fill` |
| 홈 | `i-home` | `i-home-fill` |
| 스토어 · 장바구니 | `i-cart` | `i-cart-fill` |
| 마이페이지 · 사용자 | `i-user` | `i-user-fill` |

### Action · Control

`i-arrow-left` · `i-arrow-right` · `i-chevron-left` · `i-chevron-right` · `i-chevron-down` · `i-chevron-up` · `i-close` · `i-check` · `i-plus` · `i-minus` · `i-more-h` · `i-more-v` · `i-menu`

### Common · 도구 · 커뮤니케이션

`i-search` · `i-bell` · `i-heart` · `i-heart-fill` · `i-star` · `i-star-fill` · `i-settings` · `i-edit` · `i-trash` · `i-share` · `i-filter` · `i-link` · `i-eye` · `i-eye-off` · `i-mail` · `i-clock` · `i-map-pin` · `i-camera` · `i-image`

### Status · 의미 전달

| 이름 | 권장 색 토큰 |
| --- | --- |
| `i-info` | `--sm-status-info` |
| `i-alert` | `--sm-status-warning` |
| `i-check-circle` | `--sm-status-success` |
| `i-x-circle` | `--sm-status-error` |

## Illustration · filled

컬러 필 기반의 장식용 일러스트. 빈 상태, 성공 화면, 온보딩에 제한적으로 사용.

- 컬러는 primitive 스케일을 사용 (브랜드 `indigo-500`, 성공 `green-500` 등)
- 다크 모드에서도 동일한 톤을 유지하도록 디자인 (`currentColor` 미사용 — 의도된 예외)

## 토큰

아이콘은 `currentColor` 원칙이므로 별도의 색 토큰이 없습니다. 크기 토큰만:

```
/* svg.ico */
--cm-icon-size-sm    : 16px  /* .ico-sm */
--cm-icon-size-md    : 20px  /* .ico-md */
--cm-icon-size-base  : 24px  /* .ico · default */
--cm-icon-size-lg    : 28px  /* .ico-lg */
--cm-icon-size-xl    : 40px  /* .ico-xl */

--cm-icon-stroke         : 1.7  /* 기본 outline */
--cm-icon-stroke-nav     : 1.8  /* arrow/menu */
--cm-icon-stroke-chevron : 2    /* chevron/check/plus */
```

## 접근성

- 의미 있는 아이콘: 감싸는 버튼에 `aria-label`이 있어야 합니다.
- 장식 아이콘(텍스트 라벨이 같이 있는 경우): SVG에 `aria-hidden="true"` 권장.
- 터치 타깃은 아이콘 자체가 아닌 **부모 버튼의 44×44px**로 확보.
- 스프라이트 전체는 `aria-hidden="true"`로 감쌉니다 (스크린 리더가 `<defs>`를 읽지 않도록).

## 금지

- **이모지 사용 금지** (예: `🏠`, `🔍`, `🔔`) — 반드시 `<use href="#i-*"/>` 사용
- 아이콘만 있는 버튼을 `aria-label` 없이 사용
- viewBox 밖 경로 (확대하면 잘림)
- 다크 모드에서 보이지 않는 이슈 — `currentColor` 규약 위반
- 인라인 SVG 복붙으로 아이콘 추가 — 반드시 `<symbol>`로 스프라이트에 등록 후 `<use>`

## 확장 가이드

새 아이콘을 추가할 때:

1. `index.html` 상단 `<svg xmlns...>` 스프라이트 안에 `<symbol id="i-<name>" viewBox="0 0 24 24">` 추가
2. Outline 버전은 `fill="none" stroke="currentColor" stroke-width="1.7"`
3. 필요하면 `<symbol id="i-<name>-fill">` 변형 추가 (`<path ... fill="currentColor"/>`)
4. `components/asset-icon.md`의 카테고리 표에 추가
5. `Single HTML/`에 동기화
