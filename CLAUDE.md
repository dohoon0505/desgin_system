# CLAUDE.md — AI 에이전트 작업 가이드

이 문서는 Claude/Copilot 등 AI 도구가 이 저장소를 다룰 때 읽어야 하는 문맥 요약입니다.

## 저장소의 정체

- **이름**: UIUX-DH · Unified Design System
- **형태**: 모바일 중심 디자인시스템의 단일 진실의 출처 (Single Source of Truth)
- **현재 버전**: v0.3.0 (2026.04.22)
- **범위**: Foundations(토큰/원칙) + Policy(그라데이션) + UX Writing(7원칙) + Components(24종)

## 파일 구조의 의도

1. **원본 HTML**: `UIUX-DH-design-system.html`
   - 시각 쇼케이스. 실제 CSS 토큰과 컴포넌트 프리뷰가 모두 인라인으로 렌더링됩니다.
   - 절대 삭제·변경하지 마세요. 질의가 있으면 이 파일을 먼저 확인해 근거를 찾습니다.

2. **`docs/`**: 개념/정책/원칙 (사람 가독용 마크다운)
   - `00-overview.md`: 디자인시스템이란 · 4가지 구성요소
   - `01-principles.md`: 6가지 설계 원칙
   - `02-token-architecture.md`: 3-tier 토큰 (Primitive → Semantic → Component)
   - `03-naming-conventions.md`: 이름 붙이기 · 금지 케이스 표
   - `04-gradient-policy.md`: 그라데이션 정책 (v0.3에서 재정의됨)
   - `05-ux-writing.md`: 문구 원칙 + 컴포넌트별 라이팅 규칙 + 에러 템플릿

3. **`tokens/`**: 기계 판독용 JSON. **값의 정본입니다.**
   - 같은 토큰 이름이 `semantic.light.json`과 `semantic.dark.json`에서 서로 다른 원시값을 참조합니다.
   - 코드에서 사용하는 CSS 변수와 1:1 매칭됩니다.

4. **`foundations/`**: 시각 기초에 대한 가이드 (읽는 문서)
   - color, typography, spacing, radius, elevation, motion

5. **`components/`**: 각 컴포넌트 1파일
   - 파일명은 `kebab-case`입니다.
   - 모든 컴포넌트 문서는 동일한 섹션 구조를 사용합니다 (아래 참조).

## 컴포넌트 문서 템플릿

모든 `components/*.md`는 다음 순서를 따릅니다:

```
# {Component Name}

> 한 줄 요약.

## 언제 사용하나 (Use when)
## 언제 쓰지 않나 (Don't use when)
## 변형 (Variants)
## 상태 (States)
## 토큰 (Component Tokens)
## 접근성 (Accessibility)
## UX Writing 규칙 (있는 경우)
## 원본 HTML 참조 (줄 번호)
```

## AI가 지켜야 할 규칙

### 해야 할 것
- **토큰 이름으로 말합니다.** `#4F46E5`가 아니라 `--sm-interactive-brand-default` 또는 `--p-indigo-500`.
- **같은 이름이 Light/Dark에서 다른 값이라는 사실을 이해합니다.** 시맨틱 토큰을 언급할 때 양쪽 값을 의식합니다.
- **변경은 `CHANGELOG.md`에 기록합니다.** 삭제가 아니라 누적.
- **새 컴포넌트는 자체 파일**을 가집니다. 기존 파일에 여러 컴포넌트를 섞지 않습니다.
- **원본 HTML의 줄 번호**를 참조할 때는 분할 문서에 명시합니다.

### 하지 말 것
- 색을 Hex 값으로 부르기 (`#0B0D12`) → `content-primary`
- 'Btn', 'Nav' 같은 **축약어 사용** (`CTA/URL/SVG/FAQ` 등 업계 관례만 허용)
- `style="color: #333"` 같은 **하드코딩**
- **다크 모드만을 위한 별도 토큰 이름** 만들기 (같은 이름·다른 값)
- v0.3 이후의 **두-색 그라데이션** (정책 위반, `docs/04-gradient-policy.md` 참조)

## 토큰 네이밍 패턴

```
// Primitive (Tier 1)
--p-<category>-<scale>
ex) --p-indigo-500, --p-neutral-0

// Semantic (Tier 2)
--sm-<role>-<variant>
ex) --sm-background-default, --sm-content-primary

// Component (Tier 3)
--cm-<component>-<part>-<state>
ex) --cm-button-primary-bg, --cm-input-border-focus
```

## 변경 워크플로

사용자가 "컴포넌트 추가" / "토큰 수정" / "원칙 갱신"을 요청할 때:

1. **영향 범위를 확인**합니다 — `tokens/`, `docs/`, `components/` 중 어디가 바뀌는지.
2. **원본 HTML은 변경하지 않습니다.** 질문만 있으면 참조용으로 읽습니다. (사용자가 HTML 자체를 업데이트해달라고 명시한 경우 예외)
3. 토큰 JSON을 먼저 변경하고, 그것을 참조하는 마크다운을 동기화합니다.
4. `CHANGELOG.md`에 항목을 추가합니다 (Semantic Versioning 준수).
5. `git commit` → `git push` 로 마무리합니다. 커밋 메시지는 영향 범위와 이유를 적습니다.

## 자주 하는 참조

| 찾는 것 | 보는 곳 |
| --- | --- |
| 컬러 원시값 | [tokens/primitives.json](tokens/primitives.json) |
| 라이트 테마 매핑 | [tokens/semantic.light.json](tokens/semantic.light.json) |
| 다크 테마 매핑 | [tokens/semantic.dark.json](tokens/semantic.dark.json) |
| 타이포그래피 스케일 | [tokens/typography.json](tokens/typography.json) |
| 사이즈 토큰 | [tokens/sizing.json](tokens/sizing.json) |
| 컴포넌트 상세 | [components/README.md](components/README.md) |
| 원칙 6개 | [docs/01-principles.md](docs/01-principles.md) |
| UX 라이팅 | [docs/05-ux-writing.md](docs/05-ux-writing.md) |
