---
component: Tab Bar
category: Navigation
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L6064-L6113
---

# Tab Bar

> 앱 전체의 최상위 이동 수단. **3~5개, 항상 같은 위치, 항상 같은 순서.**

## 언제 사용하나

- 모바일 앱의 최상위 네비게이션
- 서로 **동등한 우선순위**의 섹션 이동

## 언제 쓰지 않나

- 3개 미만 → 탭이 낭비됨, 버튼으로 해결
- 6개 이상 → 너무 많음. 드로어 또는 탐색 구조 재검토
- 한 섹션 안의 하위 네비게이션 → [Tabs](tabs-segment.md)

## 구조

```
┌────────────────────────────────┐
│  홈    탐색   즐겨찾기  메시지 내정보│
│ [홈]  [🔍]    [♥]    [💬•]  [👤] │
└────────────────────────────────┘
  ^활성                  ^뱃지
```

- 각 아이템: 아이콘 + 라벨 (2줄)
- 활성: 솔리드 아이콘 + `content-primary` + 라벨 굵게
- 비활성: stroke 아이콘 + `content-secondary`
- 뱃지: 아이콘 우상단 도트 또는 숫자

## 강조된 가운데 탭 (FAB 스타일)

```
   ┌─────────────────────────────┐
   │  홈    검색   [+]   알림 프로필│
   │                              │
   └─────────────────────────────┘
                  ^
           원형 FAB, 브랜드 컬러
```

흔한 패턴. "새로 만들기" 같은 강한 액션을 중앙 강조.

## 규칙

- **항상 같은 위치**: 화면 하단 고정 (safe-area-bottom 존중)
- **항상 같은 순서**: 사용자가 근육 기억으로 이동
- **한 번에 하나만 활성**
- iOS/Android 모두 Safe Area inset 적용

## 토큰

```
--cm-tabbar-bg       → var(--sm-background-default)
--cm-tabbar-border   → var(--sm-border-subtle)
--cm-tabbar-height   : 56px
--cm-tabbar-icon-active   → var(--sm-content-primary)
--cm-tabbar-icon-inactive → var(--sm-content-secondary)
```

## 접근성

- `role="tablist"` + 각 항목 `role="tab"` + 해당 화면 `role="tabpanel"`.
- 활성 항목 `aria-selected="true"` 또는 `aria-current="page"`.
- 각 아이콘 버튼에 텍스트 라벨 포함 (아이콘만으로 의미 전달 금지).

## UX Writing

라벨은 **짧은 명사**. 동사가 아닙니다.

| ❌ | ✅ |
| --- | --- |
| 홈으로 | 홈 |
| 메시지 보기 | 메시지 |
