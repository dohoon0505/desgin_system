---
title: 토큰 아키텍처 (3-tier)
section: tokens
version: 0.3.0
sourceHtml: UIUX-DH-design-system.html#L3901-L3970
---

# 02 · 세 개의 층, 의미의 계단

UIUX-DH의 모든 토큰은 세 층으로 구성됩니다. 아래 층은 원시값, 가운데 층은 의미, 위 층은 컴포넌트 전용 맥락. 변경은 위에서 아래로 내려오지 않고, **아래에서 위로 흘러갑니다.**

## Tier 01 · Foundation (Primitive)

> 팔레트의 원재료. UI에 직접 사용하지 않습니다. 디자이너만 접근합니다.

```
--p-indigo-500: #4F46E5;
--p-neutral-0:  #FFFFFF;
--p-neutral-100: #0B0D12;
```

정본: [../tokens/primitives.json](../tokens/primitives.json)

## Tier 02 · Semantic

> 목적을 가진 이름. 테마(Light/Dark)에 따라 다른 원시값을 참조합니다.

```
--sm-background-default
--sm-content-primary
--sm-border-subtle
```

정본:
- [../tokens/semantic.light.json](../tokens/semantic.light.json)
- [../tokens/semantic.dark.json](../tokens/semantic.dark.json)

## Tier 03 · Component

> 특정 컴포넌트 전용. 시맨틱 토큰을 참조하며, 예외를 흡수합니다.

```
--cm-button-primary-bg
--cm-card-surface
--cm-input-border-focus
```

정본: 각 컴포넌트 문서의 `## 토큰` 섹션 (예: [../components/button.md](../components/button.md))

---

## 왜 3-tier인가

예시 — Primary 버튼의 배경이 다크 모드에서 조금 밝아져야 한다면:

- ❌ 시맨틱 토큰 (`--sm-interactive-brand-default`)을 바꾸면 전체 시스템이 흔들립니다.
- ✅ 대신 `--cm-button-primary-bg`라는 **컴포넌트 토큰을 만들고**, 거기서 다른 원시값을 참조하게 합니다.

시스템은 흔들리지 않고, 예외는 정확히 격리됩니다.

## 네이밍 패턴

```
// Primitive
--p-<category>-<scale>
   ex) --p-indigo-500

// Semantic
--sm-<role>-<variant>
   ex) --sm-background-default
   ex) --sm-content-primary

// Component
--cm-<component>-<part>-<state>
   ex) --cm-button-primary-hover
   ex) --cm-input-border-focus
```

자세한 규약은 [03-naming-conventions.md](03-naming-conventions.md).
