# Handoff — v0.5.0 AI API Layer Migration

> **다음 세션이 이 문서만 읽고도 작업을 이어받을 수 있도록 작성된 핸드오프.**
> ~20시간 규모 작업이라 토큰을 여러 세션으로 분할 필요.

---

## 1. 현재 상태 (as of 2026-04-22)

| 항목 | 값 |
| --- | --- |
| 현재 배포 버전 | **v0.4.6** |
| origin/main 최신 커밋 | `74c7354` — Release & Governance 섹션 재작성 |
| 이번 세션 진행도 | **설계(Plan)만 완료, 실제 구현 0%** |
| Plan 문서 위치 | `~/.claude/plans/ai-shimmering-cherny.md` |
| 작업 브랜치 | `main` (브랜치 분기 없이 직접 커밋) |

### 세션 시작 시 반드시 실행
```bash
cd C:/Users/dev/desgin_system
git status                      # clean해야 함
git log --oneline -3            # 74c7354가 최상단이어야 함
git pull origin main            # 혹시 원격 변경 있는지
cat handoff.md                  # 이 문서 읽기
cat CHANGELOG.md | head -60     # 직전 릴리스 맥락 복기
```

---

## 2. 사용자 확정 의사결정

아래 4가지는 **이미 합의된 사항**. 다시 물어보지 말고 그대로 실행.

1. **Scope: Full** — P0 ~ P3 모두, ~20시간+
2. **JSON이 canonical source** — 모든 스펙은 JSON이 단일 진실의 출처, MD는 보조(점진적 제거 예정)
3. **`Single HTML/` 폴더 삭제** — Phase 4에서 실행
4. **CI 빌드 자동화 제외** — 토큰 중복 자동 제거 스크립트는 만들지 않음

### 중요한 철학적 프레이밍 (Toss 레퍼런스)
- Toss: *"디자인시스템은 제품, 팀은 고객"*
- 본 플랜: *"AI도 고객"* 으로 확장
- 사람용 레이어(MD·index.html)는 유지하되, **AI 전용 JSON API 레이어 신설**

---

## 3. 현재 구조 (AI 관점 문제 진단)

| 지표 | 현재 | 목표 |
| --- | --- | --- |
| AI 단일 쿼리 평균 read | 3–5 files | **1–2 files** |
| 토큰 값 중복 위치 | 6–7곳 (CSS + JSON + MD + Single HTML + 문서 예시) | 4곳 (Single HTML 제거) |
| 컴포넌트 HTML snippet 접근 | index.html grep | `schema.json.variants[].html` 직접 |
| Light/Dark 토큰 대조 | 2 파일 (semantic.light + semantic.dark) | 1 파일 (`theme-map.json`) |
| 의존성 스캔 | 런타임만 (`window.demoMatrix`) | 런타임 + 정적 (`system.json`) |

### 이미 있는 AI-friendly 자산 (재활용 필수)
- `assets/js/main.js`의 `buildDemoMatrix()` — 런타임 의존성 스캐너
- `index.html`의 18개 데모 섹션에 선언된 `data-uses="button,card,--sm-*,..."` 속성
- `components/*.md`의 YAML frontmatter (`component`, `version`, `sourceHtml`, `category`)
- `tokens/*.json`의 `$meta` 및 `"ref"` 백링크 구조

---

## 4. 실행 Phase (체크박스로 진행 관리)

> **세션이 끝날 때 이 체크박스를 업데이트하세요.**

### Phase 1 — Schema Foundation (~3hr, P0)

#### 1.1 메타 스키마 (`schemas/`)
- [ ] `schemas/component.schema.json` — JSON Schema Draft 2020-12
- [ ] `schemas/token.schema.json`
- [ ] `schemas/demo.schema.json`
- [ ] `schemas/snippet.schema.json`

#### 1.2 토큰 확장
- [ ] `tokens/theme-map.json` — Light/Dark pair 통합
  ```json
  {
    "--sm-content-primary":   { "light": "--p-neutral-100", "dark": "--p-neutral-0" },
    "--sm-interactive-brand": { "light": "--p-indigo-500",  "dark": "--p-indigo-400" }
  }
  ```

#### 1.3 Agent 가이드
- [ ] `AGENTS.md` (project root) — "X 원하면 Y 읽기" 디시전 트리
  - 현재 CLAUDE.md에서 AI 관련 내용을 분리·구조화
  - 결정 트리 예:
    | I want to... | Read this first |
    |---|---|
    | Use a component | `system.json` → `components/<id>.schema.json` |
    | Resolve token | `tokens/theme-map.json` |
    | HTML snippet | `components/<id>.schema.json` → `variants[].html` |

#### 1.4 루트 매니페스트
- [ ] `system.json` (project root) — AI 단일 진입점
  - 구조: `name`, `version`, `canonical`, `philosophy`, `entry`, `components[]`, `tokens{}`, `demos[]`
  - `components[].usedInDemos`는 `index.html`의 `data-uses`에서 역생성

### Phase 2 — Component Schemas (~10hr, P1)

**25개 컴포넌트 모두 `components/<id>.schema.json` 생성.**
Banner를 **모범 샘플로 먼저 만들고**, 나머지 24개는 이를 템플릿 삼아 복제.

#### 각 스키마의 필수 필드
```json
{
  "$schema": "../schemas/component.schema.json",
  "id": "banner",
  "name": "Banner",
  "version": "0.4.6",
  "category": "container",
  "description": "이미지+텍스트 프로모션. 두-색 그라데이션 금지.",
  "variants": [
    {
      "id": "hero",
      "label": "Hero",
      "description": "...",
      "html": "<div class=\"banner banner-hero\">...</div>",
      "tokens": { "bg": "--sm-interactive-brand-subtle" }
    }
  ],
  "sizes": [...],
  "states": ["rest","hover","active","focus","disabled"],
  "tokens": { "bg": "--cm-banner-bg", "fg": "--cm-banner-fg" },
  "accessibility": { "role": "link?", "minTouchTarget": 44 },
  "whenToUse": ["프로모션 강조", "캐러셀"],
  "whenNotToUse": ["두-색 그라데이션을 쓰고 싶을 때 (금지)"],
  "uxWriting": ["Eyebrow 짧게", "CTA는 동사+6자 이내"],
  "usedInDemos": ["demo-foodorder", "demo-shopping", "demo-booking", "demo-mypage"]
}
```

#### 우선순위 순서
1. [ ] `banner.schema.json` (모범 샘플)
2. [ ] `button.schema.json`
3. [ ] `badge.schema.json`
4. [ ] `card.schema.json` (others 파일로 저장됨 — ID는 `others`지만 `name`은 `Card`)
5. [ ] `text-field.schema.json`
6. [ ] `chip.schema.json`
7. [ ] `avatar.schema.json`
8. [ ] `list-item.schema.json`
9. [ ] `alert-toast.schema.json`
10. [ ] `progress-slider.schema.json`
11. [ ] `tabs-segment.schema.json`
12. [ ] `checkbox-radio-toggle.schema.json`
13. [ ] `border-divider.schema.json`
14. [ ] `bar-chart.schema.json`
15. [ ] `asset-icon.schema.json`
16. [ ] `dialog.schema.json`
17. [ ] `bottom-sheet.schema.json`
18. [ ] `popover-tooltip.schema.json`
19. [ ] `top-app-bar.schema.json`
20. [ ] `tab-bar.schema.json`
21. [ ] `drawer-breadcrumb.schema.json`
22. [ ] `skeleton-loader.schema.json`
23. [ ] `empty-state.schema.json`
24. [ ] `data-table.schema.json`
25. [ ] `accordion-tree.schema.json`

#### system.json 동기화
- [ ] 각 컴포넌트 스키마 생성 시 `system.json.components[]`에 엔트리 추가

### Phase 3 — Snippet Library (~2hr, P2)
- [ ] `snippets/patterns.json` — 10개 조합 패턴
  - `login-form`, `signup-step`, `pricing-card`, `product-card-badge`,
  - `promo-banner-compact`, `stat-card`, `empty-search`,
  - `confirm-dialog`, `toast-success`, `list-row-avatar`

### Phase 4 — Legacy Cleanup (~3hr, P3)
- [ ] `Single HTML/UIUX-DH-design-system.html` 삭제
- [ ] `Single HTML/` 폴더 자체 삭제
- [ ] `CLAUDE.md` 전면 재작성 — 4단계 → **3단계** 워크플로
  - ① 운영 진본 (index.html + CSS + JS)
  - ② JSON 스키마 (system.json + components/*.schema.json + tokens/theme-map.json)
  - ③ 사람·AI 문서 (AGENTS.md / CLAUDE.md / components/*.md)
- [ ] `CLAUDE.md`에서 "Single HTML" 언급 **전수 제거**
- [ ] `CLAUDE.md` AI 섹션을 `AGENTS.md`로 이전
- [ ] `README.md` 재작성 — 새 구조 도식 + 사람/AI 각각 진입점
- [ ] `components/*.md` 25개 frontmatter에 `canonical: "<id>.schema.json"` 추가
- [ ] `components/README.md` — JSON 레이어 설명 추가
- [ ] `CHANGELOG.md` v0.5.0 엔트리

### Phase 5 — Validation (~2hr, P3)
- [ ] `scripts/validate.mjs` (Node, 외부 의존성 없음)
  - 모든 JSON 파일 파싱 성공
  - `tokens/semantic.*.json`의 `ref` → `primitives.json` 존재 확인
  - `system.json.components[].schema` 파일 존재 확인
  - `usedInDemos` vs `index.html`의 `data-uses` 일치 확인
- [ ] `package.json` 생성 또는 갱신 (`"validate": "node scripts/validate.mjs"`)
- [ ] 실행하여 0 error 확인

### Phase 6 — 최종 검증 & 배포
- [ ] 브라우저에서 `index.html` 열어 25 컴포넌트 + 18 데모 정상 렌더
- [ ] 사이드바 링크 전부 동작
- [ ] 콘솔 오류 없음
- [ ] `window.demoMatrix` 정상 생성
- [ ] 3개 AI 질의 시나리오 수동 테스트:
  - "Banner hero variant HTML?" → 2 file reads
  - "브랜드 색 dark 모드?" → 1 file read
  - "Badge 쓰는 데모?" → 1 file read
- [ ] 논리별 3–4 커밋으로 분할 (Phase 단위 권장)
- [ ] `git push origin main`

---

## 5. 세션별 토큰 예산 가이드

이어받을 AI는 본인 컨텍스트 윈도우에 맞춰 다음 중 선택:

### 짧은 세션 (~4–5hr 분량)
**Phase 1 전체 + banner + 핵심 5종** 까지:
- 메타 스키마 4개
- theme-map.json
- AGENTS.md
- system.json (뼈대)
- banner / button / badge / card / text-field 스키마

### 중간 세션 (~8hr)
**Phase 1 + Phase 2 전체 (25종)**:
- 위 전부 + 남은 20개 컴포넌트 스키마

### 긴 세션 (~10hr)
**Phase 3 + 4 + 5 전체**:
- snippets/patterns.json
- Single HTML 삭제
- CLAUDE.md / README.md 재작성
- validate.mjs
- 커밋 + 푸쉬

각 세션 끝에 **이 handoff.md 체크박스 업데이트 + 커밋**.

---

## 6. Guardrails (지키지 않으면 작업 실패)

| 원칙 | 이유 |
| --- | --- |
| `index.html`의 `data-uses` 속성 **보존** | demoMatrix 런타임 스캐너가 의존 |
| `assets/js/main.js`의 `buildDemoMatrix()` **보존** | 기존 런타임 검증 로직 |
| `components/*.md`는 **처음에 유지** (수정 금지) | 사람 읽기용, Phase 4에서 canonical 프런트매터만 추가 |
| `Single HTML/` 삭제는 **Phase 4 끝**에 | 앞 Phase에서 참조용으로 남겨둠 |
| 커밋은 **Phase 단위**로 (한 번에 몰아 커밋 금지) | 되돌리기 쉬움 |
| 커밋 메시지 Korean + 상세 | 기존 저장소 스타일 매칭 |
| `node scripts/validate.mjs` **성공 후** push | 깨진 상태 원격 배포 방지 |
| JSON 스키마 정의 → 인스턴스 생성 순서 엄수 | 스키마 없이 스키마-기반 JSON 만들면 나중에 대규모 수정 |

---

## 7. 주요 참조 위치

### AI-friendly 자산 (재활용)
- `tokens/primitives.json` · `tokens/semantic.light.json` · `tokens/semantic.dark.json` — 이미 `$meta` 및 `ref` 구조
- `tokens/typography.json` — v0.4.1 부터 "한 벌 Pretendard" 반영
- `index.html`의 `<section class="demo-section" id="demo-*" data-uses="...">` 18개 — usedInDemos 추출 소스
- `assets/js/main.js` `buildDemoMatrix()` (lines 323–~360)

### 빈번히 봐야 할 문서
- `CLAUDE.md` — 현재 4단계 워크플로 (곧 3단계로 변경)
- `CHANGELOG.md` — v0.4.6이 마지막 릴리스
- `components/README.md` — 25종 컴포넌트 목록
- `components/banner.md` — 가장 최근 컴포넌트, 스키마 템플릿 기준

### 커밋 메시지 스타일 (매칭)
최근 커밋 참고:
- `74c7354` Release & Governance 섹션 재작성 + footer 최신화 (누락 9개 버전 추가, 최신순 정렬)
- `3b1f04d` v0.4.0~v0.4.6 릴리스 노트 7건 + CLAUDE.md 4단계 워크플로 도입
- `f8dc7d9` Banner 컴포넌트 문서 + Pretendard 단일 폰트 통합 + README 갱신
- `3e2a4e6` 실제 사용 데모 10종 추가 + 배너 컴포넌트 신설 + 탭바 하단 고정 + 브랜드 클린업

각 커밋 끝에:
```
Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
```

---

## 8. 실제 AI 질의 테스트 (완료 기준)

모든 Phase가 끝나면 다음 질의가 **1–2 파일 read** 로 해결되어야 함:

| 질의 | 기대 경로 | 최대 reads |
| --- | --- | --- |
| "Banner hero variant HTML 알려줘" | `system.json` → `components/banner.schema.json.variants[id=hero].html` | **2** |
| "브랜드 색 dark 모드 값?" | `tokens/theme-map.json` → `--sm-interactive-brand-default.dark` | **1** |
| "Badge 쓰는 모든 데모 리스트?" | `system.json.components[id=badge].usedInDemos` | **1** |
| "새 컴포넌트 추가 방법?" | `AGENTS.md` (워크플로 섹션) | **1** |
| "그라데이션 정책?" | `docs/04-gradient-policy.md` (system.json에서 링크 제공) | **1** |

---

## 9. 만약 문제가 생기면

- **git 상태가 dirty** → 이전 세션이 미완 커밋을 남겼을 수 있음. `git status`로 확인 후 판단
- **CHANGELOG.md 충돌** → v0.5.0 엔트리가 이미 있다면 이전 세션이 일부 완료. Phase 체크박스 상태 재확인
- **tokens/theme-map.json 존재** → Phase 1 이후 작업 중
- **`scripts/validate.mjs` 실행 실패** → 마지막 커밋을 `git diff`로 확인, 깨진 JSON 경로 먼저 수정
- **Single HTML 이미 삭제됨** → Phase 4 시작됨. components/*.md canonical 프런트매터 확인

---

## 10. 최종 DoD (Definition of Done)

- [ ] 모든 Phase 체크박스 체크됨
- [ ] `node scripts/validate.mjs` exit 0
- [ ] 브라우저 회귀 테스트 통과
- [ ] 3개 AI 질의 시나리오 수동 통과
- [ ] `git push origin main` 성공
- [ ] CHANGELOG v0.5.0 엔트리 추가
- [ ] `handoff.md` 파일 삭제 또는 "v0.5.0 이관 완료" 표기

---

*문서 작성: 2026-04-22 세션 종료 시점. 마지막 git 커밋 `74c7354`. Plan 파일 `~/.claude/plans/ai-shimmering-cherny.md` 병행 참조.*
