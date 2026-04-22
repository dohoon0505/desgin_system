# Handoff — v0.5.0 AI API Layer Migration

> **✅ v0.5.0 마이그레이션 완료** (2026-04-22 세션)
> 모든 Phase가 구현되어 `origin/main`에 반영됨.

---

## 🎯 최종 상태

| 항목 | 값 |
| --- | --- |
| 배포 버전 | **v0.5.0-dev** (코드 반영 · CHANGELOG 등재 · 태깅은 선택) |
| 검증 결과 | `node scripts/validate.mjs` → **9 OK / 28 warn / 0 error** |
| 커밋 | `e284bbc` → `1e18a1a` → `c3d07b9` → `656f171` (Phase 1→2→3+5→4) |
| 남은 작업 | 선택 사항 (아래 "Follow-up" 참조) |

---

## ✅ 완료된 Phase

### Phase 1 — Schema Foundation ✅
- `schemas/component.schema.json`
- `schemas/token.schema.json`
- `schemas/demo.schema.json`
- `schemas/snippet.schema.json`
- `tokens/theme-map.json` (29개 Light/Dark pair)
- `AGENTS.md` (AI 결정 트리)
- `system.json` (25 컴포넌트 · 18 데모 · 토큰 인덱스)

### Phase 2 — 25개 Component Schemas ✅
모든 컴포넌트가 `components/<id>.schema.json` 로 canonical 데이터화:

- Interactive: button · text-field · chip · checkbox-radio-toggle
- Feedback: badge · alert-toast
- Data: bar-chart · asset-icon · progress-slider · avatar
- Container: card (others) · banner · border-divider · list-item
- Navigation: tabs-segment · top-app-bar · tab-bar · drawer-breadcrumb
- Overlay: dialog · bottom-sheet · popover-tooltip
- State: skeleton-loader · empty-state
- Density: data-table · accordion-tree

### Phase 3 — Snippet Library ✅
`snippets/patterns.json` · 10개 조합 패턴:
- login-form · signup-step · pricing-card · product-card-badge
- promo-banner-compact · stat-card · empty-search
- confirm-dialog · toast-success · list-row-avatar

### Phase 4 — Legacy Cleanup ✅
- `Single HTML/` 폴더 **삭제** (10,300줄 제거)
- `CLAUDE.md` 전면 재작성 — 4단계 → **3단계** (운영 진본 + JSON 스키마 + 서술 문서)
- `CHANGELOG.md` **v0.5.0 엔트리** 추가
- `components/README.md` — JSON canonical 원칙 명시

### Phase 5 — Validator ✅
- `scripts/validate.mjs` — Node 네이티브, 외부 의존성 없음
- 검증: JSON 유효성 · 토큰 ref 해석 · system.json ↔ schema 일치 · usedInDemos ↔ data-uses 교차

---

## 📊 달성한 효과

| 지표 | Before (v0.4.6) | After (v0.5.0) |
| --- | --- | --- |
| AI 단일 쿼리 평균 read | 3–5 files | **1–2 files** |
| 토큰 중복 위치 | 6–7곳 | **4곳** (Single HTML 제거) |
| 컴포넌트 HTML snippet 접근 | index.html grep | `schema.json.variants[].html` **직접** |
| Light/Dark 토큰 대조 | 2 파일 비교 | `theme-map.json` **1 파일** |
| 파일 총 라인 수 | ~22K | **~15K** (Single HTML 제거 -10K + JSON 추가 +3K) |
| 드리프트 원천 | Single HTML 동기화 필요 | 제거됨 |
| AI 에이전트 진입점 | CLAUDE.md 서술 | `AGENTS.md` + `system.json` **구조화** |

---

## 🧪 AI 질의 테스트 (성공)

| 질의 | 실제 경로 | Read 수 |
| --- | --- | --- |
| "Banner hero variant HTML?" | `components/banner.schema.json` → `variants[id=hero].html` | **1** |
| "브랜드 색 dark 모드?" | `tokens/theme-map.json` → `--sm-interactive-brand-default.darkValue` | **1** |
| "Badge 쓰는 모든 데모?" | `system.json` → `components[id=badge].usedInDemos` 또는 `components/badge.schema.json.usedInDemos` | **1** |
| "새 컴포넌트 추가 방법?" | `AGENTS.md` → "자주 하는 작업" 섹션 | **1** |

---

## 📦 새로 생성된 파일 (35개)

```
system.json                               # AI 루트 매니페스트
AGENTS.md                                 # AI 결정 트리
handoff.md                                # 이 문서

schemas/                                  # 메타 스키마 4개
├── component.schema.json
├── token.schema.json
├── demo.schema.json
└── snippet.schema.json

components/*.schema.json × 25             # 각 컴포넌트 JSON canonical

tokens/theme-map.json                     # Light/Dark 29 pair

snippets/patterns.json                    # 10 조합 패턴

scripts/validate.mjs                      # 검증 스크립트
```

삭제: `Single HTML/` 폴더 전체

수정: `CLAUDE.md`, `CHANGELOG.md`, `components/README.md`, `components/*.schema.json` 5개 (demo-delivery 잔존 제거)

---

## 🔍 Follow-up (선택 · 권장 순서)

### 우선순위 높음 (AI 친화도 개선)
1. **components/*.md 25개에 `canonical` 프런트매터 추가** — 각 MD 상단에 `canonical: "<id>.schema.json"` 표기
2. **`data-uses` 속성 완성도** — 현재 경고 28건 해결 (`asset` 아이콘을 모든 데모에 명시적 선언 등)

### 우선순위 중간 (기능 확장)
3. **README.md 재작성** — 새 구조 도식, AI/사람 진입점 안내
4. **`docs/02-token-architecture.md` 현행화** — v0.5.0 구조 반영 (JSON canonical 언급)
5. **v0.5.0 정식 릴리스 태깅** — `v0.5.0-dev` → `v0.5.0`, git tag 발행

### 우선순위 낮음 (장기)
6. **MD → JSON 완전 이전** — 현재 MD는 보조, 나중에 자동 생성으로 전환
7. **CI 자동화** — GitHub Actions로 `validate.mjs` 실행
8. **토큰 빌드 파이프라인** — `tokens/*.json` → CSS 자동 생성

---

## 📝 이어받을 때 (필요 시)

```bash
git pull origin main
cat handoff.md              # 이 문서 (최종 상태)
cat CHANGELOG.md | head -70 # v0.5.0 엔트리 확인
node scripts/validate.mjs   # 현재 건강 체크
```

다음 세션은 위 "Follow-up" 우선순위에 따라 선택 진행. 각 항목은 독립적이라 하나씩 해도 됨.

---

## 🏁 완료 기준 (DoD) — 모두 달성

- [x] 모든 Phase 체크박스 완료
- [x] `node scripts/validate.mjs` exit 0
- [x] 3개 AI 질의 시나리오 1–2 read로 해결
- [x] Single HTML 폴더 삭제, index.html 정상 유지
- [x] CHANGELOG v0.5.0 엔트리 추가
- [x] `git push origin main` 성공
- [ ] `handoff.md` 파일 — 이 세션 종료 후 선택 유지/삭제

---

## 🎖 세션 기록

| 커밋 | 내용 |
| --- | --- |
| `e284bbc` | Phase 1 — Schema Foundation (7 files) |
| `1e18a1a` | Phase 2 — 25개 컴포넌트 스키마 (25 files, +1538 lines) |
| `c3d07b9` | Phase 3+5 — Snippets + Validator (7 files, +292 lines) |
| `656f171` | Phase 4 — Single HTML 제거 + CLAUDE.md 재작성 (4 files, +152/−10503) |
| (이 커밋) | handoff.md 최종 상태 업데이트 |

**총 변경**: +3,503 lines added / −10,516 lines removed = **순 −7,013 lines** (대부분 Single HTML 삭제)

*세션 종료: 2026-04-22. Toss 철학 "디자인시스템은 제품, 팀은 고객" → "AI도 고객" 으로 확장 성공.*
