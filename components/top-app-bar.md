---
component: Top App Bar
canonical: "top-app-bar.schema.json"
category: Navigation
since: 0.3.0
version: 0.3.2
sourceHtml: index.html#appbar
---

# Top App Bar

> 화면의 제목과 주요 액션이 모이는 곳. **뒤로가기는 항상 왼쪽 첫 번째, 닫기·다음 같은 주요 액션은 오른쪽 마지막.** 5가지 변형이 있습니다.

## 5가지 변형

### 1. Center title · back + more

```
┌────────────────────────────────┐
│ [←]         헤더 타이틀      [⋯] │
└────────────────────────────────┘
```

- 아이콘: `i-arrow-left` (뒤로), `i-more-h` (더보기)
- 제목: **중앙 정렬** · `heading-sm` · 700
- **서브 화면의 기본형** — 제목을 명확히 강조하고 보조 액션은 아이콘으로

### 2. Left title · back + more

```
┌────────────────────────────────┐
│ [←] 헤더 타이틀              [⋯] │
└────────────────────────────────┘
```

- 좌측 정렬 제목. **상세 화면의 표준형** (제품 상세·아티클 등)

### 3. Left title · back + text action

```
┌────────────────────────────────┐
│ [←] 헤더 타이틀             다음 │
└────────────────────────────────┘
```

- 오른쪽은 `text-btn text-btn-brand` — `--sm-content-brand` + 700
- **멀티 스텝 플로우**(회원가입·주문 등)에서 "다음" 단계 유도

### 4. Left title · close (no back)

```
┌────────────────────────────────┐
│ 헤더 타이틀                   [×]│
└────────────────────────────────┘
```

- 왼쪽에 뒤로가기 없음 · 오른쪽은 `i-close`
- **모달형 화면**(전체 화면 다이얼로그)에서 닫기가 주된 탈출구

### 5. Left title · text action (no back)

```
┌────────────────────────────────┐
│ 헤더 타이틀                다음 │
└────────────────────────────────┘
```

- 왼쪽에 뒤로가기 없음 · 오른쪽은 "다음" 브랜드 텍스트 버튼
- **모달형 화면에서 완료/다음을 강조** — 취소는 뒤로가기가 아닌 닫기(✕)로 제공할 때

### 6. Large title · home level (예외 · 최상위 화면)

```
┌────────────────────────────────┐
│                      [🔔] [👤]  │
│                                │
│ 홈                              │
└────────────────────────────────┘
```

- 최상위 화면에서 사용
- 큰 타이틀(`heading-lg` ~ `display-sm`)
- 스크롤 시 타이틀이 작아지며 상단 고정

## 변형 선택 기준

| 화면 맥락 | 권장 변형 |
| --- | --- |
| 상세 페이지 (아티클·프로필) | **2. Left + back + more** |
| 서브 화면에서 제목 강조 | **1. Center + back + more** |
| 멀티 스텝 플로우(회원가입·결제) | **3. Left + back + 다음** |
| 전체 화면 모달(설정·약관) | **4. Left + 닫기(×)** |
| 모달에서 저장/완료 강조 | **5. Left + 다음** |
| 탭 바 최상위 홈 화면 | **6. Large title** |

## 레이아웃 규칙

- 높이: 표준 **56px** · Large **120~160px**
- 좌우 패딩: `--size-400` (16px)
- 아이콘 버튼 영역: **44×44px** (터치 타겟)
- SVG 아이콘 자체 크기: **24×24** (패키지 기본)
- 텍스트 버튼 패딩: 8px 12px · radius `--radius-sm`

## 토큰

```
--cm-appbar-bg             → var(--sm-background-default)
--cm-appbar-border         → var(--sm-border-subtle)   /* 스크롤 시 표시 */
--cm-appbar-title          → var(--sm-content-primary)
--cm-appbar-icon           → var(--sm-content-primary)
--cm-appbar-action         → var(--sm-content-brand)    /* 텍스트 액션 */
--cm-appbar-action-hover   → var(--sm-interactive-brand-subtle)
--cm-appbar-height         : 56px
--cm-appbar-height-lg      : 120px
```

## 접근성

- `role="banner"` 또는 `<header>` 요소 사용.
- 모든 icon button은 `aria-label` 필수 ("뒤로", "닫기", "더 보기" 등).
- 텍스트 액션("다음")은 일반 버튼으로 충분 (하지만 의미가 모호하면 `aria-label="다음 단계로"` 추가).
- 뒤로가기는 하드웨어/제스처 백과 **동일 동작**을 하도록.
- **금지**: 중앙 정렬 제목에서 좌우 아이콘 개수가 다를 때 — 제목이 한쪽으로 쏠림.

## UX Writing · "다음" 버튼

텍스트 액션은 **결과를 담는 동사**. 단순 "확인/OK" 대신:

| ❌ | ✅ |
| --- | --- |
| 확인 | 다음 · 저장 · 완료 · 신청 |
| OK | 결제하기 · 가입하기 |

## 스크롤 동작

- 기본: `position: sticky` + `backdrop-filter: blur(12px)`
- Large title: 스크롤에 따라 축소 — `--motion-base` + `--ease-standard`
- 경계선(`border-bottom`)은 스크롤이 있을 때만 표시 (top 상태에서는 투명)
