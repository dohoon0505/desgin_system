# UIUX-DH · Unified Design System

> 토큰부터 문장까지. 모바일 중심의 통합 디자인시스템.
> 현재 버전 **v0.3.0** · 최초 릴리스 2026.04.21 · 최근 업데이트 2026.04.22

## 실행하기

`index.html`을 브라우저로 열면 바로 실행됩니다. (외부 서버 불필요)

```
open index.html          # macOS
start index.html         # Windows
```

## 저장소는 무엇인가요

사람이 편집하기 쉬운 **바닐라 HTML/CSS/JS 구조**(`index.html` + `assets/`)와 외부 공유용 **단일 파일 배포본**(`Single HTML/`), 그리고 AI·사람이 같이 읽는 **마크다운 문서**를 함께 유지합니다.

## 폴더 구조

```
desgin_system/
├── index.html                       ← 🔸 운영 진본 · 브라우저에서 이 파일을 엶
├── assets/
│   ├── css/main.css                 ← 전체 스타일 (토큰부터 컴포넌트까지)
│   └── js/main.js                   ← 라우터 · 사이드바 · 테마 전환
│
├── Single HTML/
│   └── UIUX-DH-design-system.html   ← 🔹 자기완결 배포본 (CSS/JS 인라인)
│
├── README.md                         ← 이 파일 · 사람용 진입점
├── CLAUDE.md                         ← 🤖 AI 에이전트용 가이드 (3단계 원칙)
├── CHANGELOG.md                      ← 버전 이력 (Semantic Versioning)
│
├── docs/                             ← 개념과 정책
│   ├── 00-overview.md                · 디자인시스템이란
│   ├── 01-principles.md              · 여섯 가지 원칙
│   ├── 02-token-architecture.md      · 3-tier 토큰 구조
│   ├── 03-naming-conventions.md      · 네이밍 규칙
│   ├── 04-gradient-policy.md         · 그라데이션 정책
│   └── 05-ux-writing.md              · UX 라이팅 7원칙
│
├── tokens/                           ← 기계 판독용 값 (JSON, 값의 정본)
│   ├── primitives.json               · Tier 1 · 원시 컬러 스케일
│   ├── semantic.light.json           · Tier 2 · Light 테마 매핑
│   ├── semantic.dark.json            · Tier 2 · Dark 테마 매핑
│   ├── typography.json
│   ├── sizing.json
│   ├── radius.json
│   ├── elevation.json
│   ├── motion.json
│   └── z-index.json
│
├── foundations/                      ← 시각 기초 (읽는 문서)
│   ├── color.md
│   ├── typography.md
│   ├── spacing.md
│   ├── radius.md
│   ├── elevation.md
│   └── motion.md
│
└── components/                       ← 컴포넌트별 사양 (24종)
    ├── README.md                     · 컴포넌트 인덱스
    └── <component-name>.md ...
```

## 세 곳의 "진본"과 역할

| 구분 | 경로 | 언제 참조 |
| --- | --- | --- |
| 🔸 **운영 진본** | `index.html` + `assets/` | 수정 · 새 기능 개발 · 로컬 미리보기 |
| 🔹 **배포본** | `Single HTML/UIUX-DH-design-system.html` | 외부 공유 · 백업 · 단일 파일이 필요한 컨텍스트 |
| 🤖 **AI 문서** | `docs/` · `tokens/` · `foundations/` · `components/` | AI 에이전트가 구조로 이해 · 사람이 세부 읽기 |

세 곳은 **반드시 동기화** 되어야 합니다. 자세한 3단계 워크플로는 [CLAUDE.md](CLAUDE.md) 참조.

## 어디서 시작해야 하나요

| 질문 | 바로 가기 |
| --- | --- |
| 당장 보고 싶어요 | [index.html](index.html) 을 브라우저로 엶 |
| 디자인시스템이 뭐예요? | [docs/00-overview.md](docs/00-overview.md) |
| 지키는 원칙은? | [docs/01-principles.md](docs/01-principles.md) |
| 토큰은 어떻게 구성되나요? | [docs/02-token-architecture.md](docs/02-token-architecture.md) |
| 이름은 어떻게 붙이나요? | [docs/03-naming-conventions.md](docs/03-naming-conventions.md) |
| 그라데이션 써도 되나요? | [docs/04-gradient-policy.md](docs/04-gradient-policy.md) |
| 화면의 문구는 어떻게? | [docs/05-ux-writing.md](docs/05-ux-writing.md) |
| 실제 컬러 값이 궁금해요 | [tokens/primitives.json](tokens/primitives.json) |
| 컴포넌트 목록이 보고 싶어요 | [components/README.md](components/README.md) |
| 뭐가 바뀌었나요? | [CHANGELOG.md](CHANGELOG.md) |

## 수정 시 3단계 (필수)

디자인시스템을 수정할 때는 다음 **3가지 작업을 반드시 함께** 수행합니다.

1. **기본 수정** — `index.html` · `assets/css/main.css` · `assets/js/main.js`
2. **배포본 동기화** — `Single HTML/UIUX-DH-design-system.html`에 동일한 변경 반영 (CSS/JS 인라인)
3. **AI 문서 업데이트** — `docs/` · `tokens/` · `foundations/` · `components/` · `CHANGELOG.md`

> **하나라도 누락 금지.** 자세한 예시는 [CLAUDE.md](CLAUDE.md) 참조.

## 저장소를 유지하는 원칙

1. **토큰 이름으로 말합니다.** `#4F46E5` 대신 `--sm-interactive-brand-default`.
2. **같은 토큰 이름이 Light/Dark에서 다른 값**을 가집니다. 시맨틱 토큰은 테마를 횡단합니다.
3. **변경은 [CHANGELOG.md](CHANGELOG.md)에 누적**됩니다. 과거는 지우지 않습니다.
4. **새 컴포넌트는 자체 파일**을 가집니다. `components/` 아래에 추가합니다.
5. AI 작업 시에는 먼저 [CLAUDE.md](CLAUDE.md)를 읽습니다.

## 라이선스 & 유지

MAINTAINED BY /DH · 2026
