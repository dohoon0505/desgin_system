---
component: List Item
canonical: "list-item.schema.json"
category: Components
since: 0.2.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L5486-L5548
---

# List Item

> 수직으로 스캔하는 가장 기본적인 정보 단위. 3단 구조를 지킵니다.

## 구조

```
┌────┬────────────────┬──────────┐
│ L  │ Body           │  Trail   │
│    │   Title        │          │
│    │   Meta         │          │
└────┴────────────────┴──────────┘
  ↑         ↑              ↑
 Lead     Body           Trail
(icon,   (title+        (value·
 image)   meta)         chevron)
```

- **Lead**: 아이콘 배지 또는 아바타
- **Body**: 제목 + 보조 정보
- **Trail**: 값(금액, 날짜 등) 또는 chevron(▸)

## 변형

### Standard · avatar/icon + meta + value

가장 일반적인 형태. 계좌 목록, 설정 메뉴, 프로젝트 리스트.

### Key-Value · detail info

주문 정보, 계좌 상세 같은 **정적 정보**. 좌측 키, 우측 값.

```
주문번호       TDS-2026-04-821
주문일시       2026.04.21 14:32
결제수단       신용카드 · 일시불
배송지         서울특별시 강남구
───────────────
총 결제금액    ₩124,800
```

마지막 행(합계)은 강조 (volume-heavy weight + brand color).

## 상호작용

- 클릭 가능한 행: hover 시 `background-muted`, 오른쪽 chevron.
- 드래그 가능: left swipe → 삭제 액션.

## 토큰

```
--cm-list-item-bg       → var(--sm-background-default)
--cm-list-item-bg-hover → var(--sm-background-muted)
--cm-list-item-divider  → var(--sm-border-subtle)
```

## 접근성

- 전체 행이 링크/버튼일 때는 `role="button"` 또는 `<a>` 사용.
- 행마다 의미 있는 라벨 (단순 chevron만 있어도 전체 행이 클릭 타깃).
- 긴 목록에서는 섹션 헤더(`role="heading"`)로 그룹 구분.
