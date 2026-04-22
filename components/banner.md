---
component: Banner
category: Components
since: 0.4.6
version: 0.4.6
sourceHtml: UIUX-DH-design-system.html#L2630+
---

# Banner

> 이미지와 텍스트의 **조화로운 조합**으로 프로모션을 전달하는 카드. **두-색 그라데이션으로 채우지 않습니다**(v0.3 그라데이션 정책 준수). 단색 pastel · 다크 · 또는 단일 이미지 배경 + 가독성 오버레이만 허용.

## 언제 사용하나 (Use when)

- 한 화면에 **혜택·이벤트·프로모션**을 강조해야 할 때
- 홈 화면 **히어로**(최상단 큰 배너) 또는 **섹션 배너**(리스트 중간)
- **캐러셀**에 N/전체 형태로 여러 프로모션을 나열할 때
- 파트너·브랜드 **할인 쿠폰**을 이미지와 함께 보여줄 때

## 언제 쓰지 않나 (Don't use when)

- 단순 정보 전달 → `Alert` 또는 `Toast`
- 사용자 결정을 막아야 하는 순간 → `Dialog`
- 메뉴·탐색 용도 → `List Item` 또는 `Card`
- 두-색 그라데이션으로 배경을 채우고 싶을 때 → **금지**. 솔리드 컬러나 이미지를 쓰세요

## 기본 구조

```
┌─────────────────────────────────────────────┐
│ [ribbon] (optional, 좌상단)                  │
│ eyebrow · 악센트(%)                          │
│ Title (headline)              [image/illust] │
│ Subtitle (optional)                          │
│ [CTA] (optional)                             │
│                              [indicator]     │
│                              (우하단 N/전체)  │
└─────────────────────────────────────────────┘
```

## 변형 (Variants)

| Variant | 클래스 | 쓰임새 |
| --- | --- | --- |
| Default | `.banner` | 일반 크기. pastel 배경 + 일러스트 |
| Hero | `.banner.banner-hero` | 홈 최상단 주목 독점 (140×140 이미지) |
| Compact | `.banner.banner-compact` | 리스트 끼움. 76px 최소 높이, 56×56 이미지 |
| Overlay | `.banner.banner-overlay` | 이미지 배경 + 좌측 투명 오버레이 |

## 색상 변형 (Color variants)

솔리드 단색만 사용. 변수 직접 지정 또는 프리셋 중 선택:

| 클래스 | 배경 | 쓰임새 |
| --- | --- | --- |
| *(기본)* | `--sm-interactive-brand-subtle` | 브랜드 프로모션 |
| `.banner-dark` | `#1F2937` | 프리미엄·이벤트 강조 |
| `.banner-warm` | `#FEF3C7` | 세일·가격 혜택 |
| `.banner-cool` | `#DBEAFE` | 멤버스·정보성 |
| `.banner-rose` | `#FCE7F3` | 라이프스타일·F&B |
| `.banner-mint` | `#D1FAE5` | 친환경·헬스 |

커스텀 배경이 필요하면 인라인 `style="background:#..."` 로 오버라이드합니다(단, 단색만).

## 부속 요소 (Sub-parts)

| 클래스 | 역할 |
| --- | --- |
| `.banner-content` | 텍스트 영역 래퍼 |
| `.banner-eyebrow` | 제목 위 작은 라벨. `.banner-accent`로 부분 강조 가능 |
| `.banner-title` | 메인 헤드라인 (22px / hero 26px) |
| `.banner-subtitle` | 보조 문구 (13px / 72% opacity) |
| `.banner-image` | 우측 이미지 슬롯 (기본 112×112) |
| `.banner-cta` | 인라인 CTA 칩 |
| `.banner-ribbon` | 좌상단 대각선 리본 뱃지 |
| `.banner-indicator` | 우하단 "N/전체" 페이지 인디케이터 |

## 토큰 (Component Tokens)

```css
--cm-banner-bg:         var(--sm-interactive-brand-subtle);
--cm-banner-fg:         var(--sm-content-primary);
--cm-banner-accent:     var(--sm-content-brand);
--cm-banner-radius:     var(--radius-lg);
--cm-banner-pad-y:      var(--size-700);
--cm-banner-pad-x:      var(--size-600);
```

각 토큰은 시맨틱 토큰에 매핑되어 Light/Dark 테마를 자동 횡단합니다.

## 그라데이션 정책 (v0.3 준수)

Banner는 **두-색 그라데이션을 사용하지 않습니다**. 허용되는 배경:

1. **솔리드 단색** (시맨틱 또는 Primitive 토큰, pastel 계열 권장)
2. **단일 이미지 배경** (`.banner-overlay`) — 사진·일러스트
3. **가독성 오버레이** (`.banner-overlay::before`) — 이미지 위 텍스트 영역에만 한 방향 투명도 그라데이션 (rgba(0,0,0,0.5) → 0)

→ 브랜드 모멘트 외 장식용 두-색 그라데이션은 금지. 자세한 내용은 [docs/04-gradient-policy.md](../docs/04-gradient-policy.md).

## 접근성 (Accessibility)

- 배너 전체를 클릭 가능하게 할 때 `<a>` 또는 `<button>`으로 감싸거나 `role="button" tabindex="0"` 지정
- `.banner-image`의 장식용 SVG는 `aria-hidden="true"` 권장
- 중요한 정보가 이미지에만 있으면 텍스트로도 제공 (예: 할인율 "5%"는 텍스트에도 포함)
- `.banner-overlay`의 텍스트는 어두운 오버레이 위에서 WCAG AA 명도대비(4.5:1) 확보 필수
- 리본 뱃지(`-35deg` 회전)의 내용은 스크린리더가 읽을 수 있게 `aria-label`로도 제공 권장

## UX Writing 규칙

- **Eyebrow**: 한 줄·짧게. 할인율·기간 등 숫자는 `.banner-accent`로 브랜드 색 강조
- **Title**: 최대 2줄. 해요체 금지(명령·선언조 OK). 숫자는 큰 포인트 (`3,000원 할인부터`)
- **Subtitle**: 조건·기간·한정을 명시 (`#앱 한정`, `4/22~4/24`, `*조건 확인`)
- **CTA**: 동사로 끝나는 6자 이내 (`지금 담기 →`, `쿠폰 받기 →`)
- **Indicator**: `N / 전체` 형식 고정. 클릭 시 전체 목록 이동 암시 (`모두 보기` 병기 가능)

## 사용 데모

실제 `demo-*` 화면 내 Banner 사용처:

- `demo-foodorder` — 쿠폰 배너("4월 NEW 쿠폰팩")
- `demo-shopping` — 히어로 배너("이달의 굿프라이스")
- `demo-booking` — 상황별·주제별 BEST 캐러셀 (3종)
- `demo-banking` — 적금 프로모션 배너
- `demo-mypage` — 포인트 멤버십 배너

수정 시 `window.demoMatrix.byComponent['banner']`로 영향 데모 전수 조회 가능.
