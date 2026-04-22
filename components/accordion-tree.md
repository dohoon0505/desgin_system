---
component: Accordion · Tree
canonical: "accordion-tree.schema.json"
category: Density
since: 0.3.0
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L6378-L6479
---

# Accordion · Tree

> 긴 콘텐츠는 접어둡니다. **Accordion은 FAQ·폼 섹션**, **Tree는 폴더 구조·계층적 데이터**.

## Accordion

### 언제 사용하나

- **FAQ**, 긴 설명의 그룹
- 폼의 섹션 접기 (선택 단계 펼치기)
- 긴 리스트의 그룹 요약

### 구조

```
┌───────────────────────────────┐
│ UIUX-DH는 어떤 디자인시스템인가요?  ▼│  ← open
├───────────────────────────────┤
│ 토큰 · 규칙 · 컴포넌트 · 운영      │
│ 프로세스가 하나로 묶인...         │
├───────────────────────────────┤
│ 라이트 모드와 다크 모드는?     ▶ │  ← closed
├───────────────────────────────┤
│ 컴포넌트 토큰은 시맨틱과 어떻게?▶ │
└───────────────────────────────┘
```

- 열린 항목의 trigger: `content-primary` + chevron ▼
- 닫힌 항목: `content-secondary` + chevron ▶

### 정책: 단일 열기 vs 다중 열기

**별도 결정 사항**입니다. 화면 컨텍스트에 따라:

- **단일 열기** (한 번에 하나만): FAQ, 고정된 폼 플로우
- **다중 열기** (여러 개 동시): 필터 그룹, 설정 섹션

한 화면 안에서는 하나의 정책만 사용합니다.

## Tree

### 언제 사용하나

- 파일/폴더 구조
- 계층적 카테고리
- 조직도·메뉴

### 구조

```
▼ 📁 design-system
   ▼ 📁 tokens
      📄 primitive.json
    ◉ 📄 semantic.json    ← 선택됨
      📄 component.json
   ▶ 📁 components
      📄 README.md
```

- `▶` / `▼` chevron
- 들여쓰기 + 폴더/파일 아이콘
- 선택 행: `interactive-brand-subtle` 배경

## 토큰

```
/* Accordion */
--cm-accordion-trigger-content → var(--sm-content-primary)
--cm-accordion-body-content    → var(--sm-content-secondary)
--cm-accordion-border          → var(--sm-border-subtle)

/* Tree */
--cm-tree-node-bg-hover   → var(--sm-background-muted)
--cm-tree-node-bg-selected→ var(--sm-interactive-brand-subtle)
--cm-tree-indent          : 20px
```

## 접근성

### Accordion
- 각 trigger는 `<button aria-expanded="true/false" aria-controls="body-id">`.
- Body 영역은 `id` + `role="region"` + `aria-labelledby` 로 trigger와 연결.
- 키보드: Enter/Space로 토글. Tab으로 trigger 이동.

### Tree
- `role="tree"` + 각 노드 `role="treeitem"`.
- 펼침 상태 `aria-expanded="true/false"`.
- 선택: `aria-selected="true"`.
- 방향키 이동: ↑/↓ 형제, →/← 펼치기/접기.

## 모션

- 펼침: `--motion-base` (200ms) + `--ease-standard`
- 높이 애니메이션: `max-height` + overflow hidden, 또는 FLIP 기법
- `prefers-reduced-motion` 시 즉시 전환
