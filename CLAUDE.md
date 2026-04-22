# CLAUDE.md — AI 에이전트 작업 가이드

이 문서는 Claude/Copilot 등 AI 도구가 이 저장소를 다룰 때 읽어야 하는 문맥 요약입니다.

## 저장소의 정체

- **이름**: UIUX-DH · Unified Design System
- **형태**: 모바일 중심 디자인시스템의 단일 진실의 출처 (Single Source of Truth)
- **현재 버전**: v0.3.0 (2026.04.22)
- **범위**: Foundations(토큰/원칙) + Policy(그라데이션) + UX Writing(7원칙) + Components(24종) + 실제 사용 데모(9종)

---

## ⚠️ 가장 중요 · 3단계 작업 원칙

**디자인시스템을 수정할 때 다음 3가지 작업을 반드시 함께 수행합니다.**

### 1. 기본 — `index.html` + 바닐라 JS 구조 수정

실제 운영·렌더링되는 진본입니다. 아래 세 파일 중 영향 범위에 맞는 것을 수정합니다.

| 파일 | 수정 대상 |
| --- | --- |
| `index.html` | HTML 구조 · 컴포넌트 마크업 · 섹션 추가/삭제 |
| `assets/css/main.css` | CSS 토큰 · 컴포넌트 스타일 · 레이아웃 · 반응형 |
| `assets/js/main.js` | 라우터 · 사이드바 · 테마 전환 · 상호작용 로직 |

### 2. 반영 — `Single HTML/UIUX-DH-design-system.html` 동기화

`Single HTML/` 폴더의 단일 파일은 **외부 배포/백업/AI가 통째로 읽을 때를 위한 자기완결 버전**입니다.

1번에서 수정한 내용을 이 파일에도 **인라인으로 반영**합니다 (`<style>` 안에 CSS, `<script>` 안에 JS).

### 3. 문서 — 각 폴더 내 `md` 파일 업데이트

**AI가 이해할 수 있도록 구조화된 문서**를 함께 갱신합니다.

| 수정 유형 | 업데이트 대상 문서 |
| --- | --- |
| 토큰 값 변경 | `tokens/*.json` (값의 정본) + 관련 `foundations/*.md` |
| 컴포넌트 변경 | `components/<name>.md` (프런트매터 버전 갱신) |
| 원칙/정책 갱신 | `docs/0x-*.md` |
| 새 릴리스 | `CHANGELOG.md` 항목 추가 (Semantic Versioning) |

> **이 3단계 모두를 건너뛰지 마세요.** 하나라도 누락되면 시스템의 일관성이 깨집니다.
> 예: `index.html`만 고치면 Single HTML 버전이 outdated 되고, AI 문서가 outdated 되면 다음 Claude 세션이 잘못된 근거로 작업합니다.

---

## 파일 구조

```
UIUX-DH · Unified Design System/
├── index.html                       ← 운영 진본 (바닐라 HTML)
├── assets/
│   ├── css/main.css                 ← 운영 진본 (전체 스타일)
│   └── js/main.js                   ← 운영 진본 (라우터·상호작용)
│
├── Single HTML/
│   └── UIUX-DH-design-system.html   ← 자기완결 단일 파일 (배포·백업용)
│
├── docs/                             ← 개념/정책/원칙 (사람 가독용 md)
│   ├── 00-overview.md
│   ├── 01-principles.md
│   ├── 02-token-architecture.md
│   ├── 03-naming-conventions.md
│   ├── 04-gradient-policy.md
│   └── 05-ux-writing.md
│
├── tokens/                           ← 기계 판독용 JSON (값의 정본)
│   ├── primitives.json
│   ├── semantic.light.json
│   ├── semantic.dark.json
│   ├── typography.json
│   ├── sizing.json
│   ├── radius.json
│   ├── elevation.json
│   ├── motion.json
│   └── z-index.json
│
├── foundations/                      ← 시각 기초 가이드
│   ├── color.md
│   ├── typography.md
│   ├── spacing.md
│   ├── radius.md
│   ├── elevation.md
│   └── motion.md
│
├── components/                       ← 컴포넌트 1개당 1파일 (kebab-case)
│   ├── README.md
│   └── <component-name>.md ...       (24종)
│
├── CLAUDE.md                         ← AI 에이전트 가이드 (이 문서)
├── README.md                         ← 사람 진입점
└── CHANGELOG.md                      ← 누적 릴리스 기록
```

### 파일 역할 요약

| 구분 | 경로 | 역할 |
| --- | --- | --- |
| **운영 진본** | `index.html` · `assets/css/main.css` · `assets/js/main.js` | 브라우저에서 실제 렌더링. 기능 수정은 여기부터. |
| **배포본** | `Single HTML/UIUX-DH-design-system.html` | 외부 공유·백업용 자기완결 단일 파일. 1번 수정 후 동기화. |
| **AI 문서** | `docs/` · `tokens/` · `foundations/` · `components/` | AI가 구조로 이해. 수정 내용을 반드시 반영. |

---

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
```

---

## AI가 지켜야 할 규칙

### 해야 할 것
- **토큰 이름으로 말합니다.** `#4F46E5`가 아니라 `--sm-interactive-brand-default` 또는 `--p-indigo-500`.
- **같은 이름이 Light/Dark에서 다른 값이라는 사실을 이해합니다.** 시맨틱 토큰을 언급할 때 양쪽 값을 의식합니다.
- **변경은 `CHANGELOG.md`에 기록합니다.** 삭제가 아니라 누적.
- **새 컴포넌트는 자체 파일**을 가집니다. 기존 파일에 여러 컴포넌트를 섞지 않습니다.
- **3단계 워크플로 준수** — `index.html` → `Single HTML/` → `*.md` 동시 업데이트.

### 하지 말 것
- 색을 Hex 값으로 부르기 (`#0B0D12`) → `content-primary`
- 'Btn', 'Nav' 같은 **축약어 사용** (`CTA/URL/SVG/FAQ` 등 업계 관례만 허용)
- `style="color: #333"` 같은 **하드코딩**
- **다크 모드만을 위한 별도 토큰 이름** 만들기 (같은 이름·다른 값)
- v0.3 이후의 **두-색 그라데이션** (정책 위반, `docs/04-gradient-policy.md` 참조)
- **`Single HTML/` 파일만 단독 수정** → `index.html`과 불일치를 남깁니다.

---

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

---

## 변경 워크플로 상세 예시

### 예시 A — 컴포넌트의 색상 변경

요청: "버튼 primary 색상을 조금 더 진하게"

1. `tokens/primitives.json` — 새 인디고 값이 필요하면 추가
2. `tokens/semantic.light.json` / `semantic.dark.json` — `interactive-brand-default` 매핑 검토
3. `assets/css/main.css` — `--p-indigo-500` 변수 값 수정
4. `index.html` — 시각적으로 변화 확인 (보통 마크업 변경 없음)
5. `Single HTML/UIUX-DH-design-system.html` — 인라인 `<style>` 내부의 `--p-indigo-500` 갱신
6. `components/button.md` — 토큰 섹션 최신화
7. `CHANGELOG.md` — "Changed: primary 버튼 기본 색상 더 진하게 (--p-indigo-500: #4F46E5 → ...)"
8. `git commit` + `push`

### 예시 B — 새 컴포넌트 추가

요청: "Tag 컴포넌트 추가 (Chip과 유사하지만 상호작용 없음)"

1. `index.html` — 새 섹션 마크업 추가 (`<section class="component-section" id="tag">`)
2. `assets/css/main.css` — `.tag` 관련 스타일 추가
3. `assets/js/main.js` — 사이드바 목록과 CATEGORIES 객체에 `tag` 등록
4. `Single HTML/UIUX-DH-design-system.html` — 위 1·2·3 인라인 반영
5. `components/tag.md` — 신규 문서 (템플릿 준수)
6. `components/README.md` — 컴포넌트 인덱스에 추가
7. `CHANGELOG.md` — "Added: Tag component (information display, no interaction)"
8. `git commit` + `push`

---

## 자주 하는 참조

| 찾는 것 | 보는 곳 |
| --- | --- |
| 운영 진본 HTML | [index.html](index.html) |
| 운영 진본 CSS | [assets/css/main.css](assets/css/main.css) |
| 운영 진본 JS | [assets/js/main.js](assets/js/main.js) |
| 배포용 단일 파일 | [Single HTML/UIUX-DH-design-system.html](Single%20HTML/UIUX-DH-design-system.html) |
| 컬러 원시값 | [tokens/primitives.json](tokens/primitives.json) |
| 라이트 테마 매핑 | [tokens/semantic.light.json](tokens/semantic.light.json) |
| 다크 테마 매핑 | [tokens/semantic.dark.json](tokens/semantic.dark.json) |
| 타이포그래피 스케일 | [tokens/typography.json](tokens/typography.json) |
| 사이즈 토큰 | [tokens/sizing.json](tokens/sizing.json) |
| 컴포넌트 상세 | [components/README.md](components/README.md) |
| 원칙 6개 | [docs/01-principles.md](docs/01-principles.md) |
| UX 라이팅 | [docs/05-ux-writing.md](docs/05-ux-writing.md) |
