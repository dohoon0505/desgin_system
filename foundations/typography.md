---
title: Typography
section: foundation
version: 0.3.0
tokens:
  - ../tokens/typography.json
sourceHtml: UIUX-DH-design-system.html#L4151-L4219
---

# Typography

Pretendard Variable 한 벌로 모든 위계를 구성합니다. 한국어의 시각 밀도를 고려해 line-height를 넉넉히 잡고, tracking은 크기에 따라 조정됩니다.

## 폰트 패밀리

- **Sans (기본)**: `Pretendard Variable` → [CDN](https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/variable/pretendardvariable-dynamic-subset.min.css)
- **Mono (코드·메타)**: `JetBrains Mono`

## 스케일

| Token | Weight / Size | Leading | Tracking | 용도 |
| --- | --- | --- | --- | --- |
| `--text-display-lg` | 700 / 56px | 1.1 | -3.5% | 히어로 최대 타이틀 |
| `--text-display-md` | 700 / 44px | 1.12 | -3% | 섹션 타이틀 |
| `--text-display-sm` | 700 / 36px | 1.2 | -2.5% | 부제목 |
| `--text-heading-lg` | 700 / 28px | 1.3 | -2% | 페이지 헤더 |
| `--text-heading-md` | 700 / 22px | 1.35 | -1.5% | 카드 제목 |
| `--text-heading-sm` | 600 / 18px | 1.4 | -1% | 블록 제목 |
| `--text-body-lg` | 400 / 17px | 1.55 | — | 강조 본문 |
| **`--text-body-md`** | 400 / 15px | 1.6 | — | **기본 본문** |
| `--text-body-sm` | 400 / 13px | 1.55 | — | 보조 본문·설명 |
| `--text-label-lg` | 600 / 15px | 1.4 | — | 큰 라벨·버튼 |
| `--text-label-md` | 600 / 13px | 1.4 | — | 라벨·버튼 |
| `--text-label-sm` | 600 / 11px | 1.4 | — | 태그·뱃지 |
| `--text-caption` | 500 / 12px | 1.45 | — | 캡션·도움말 |
| `--text-overline` | 600 / 11px | 1.4 | +8%, uppercase | 섹션 메타·태그 |

정본: [tokens/typography.json](../tokens/typography.json)

## 사용 규칙

- **기본 본문은 `body-md` (15px).** 더 작게 내려가지 않습니다.
- **Display/Heading은 tracking 음수** 필수. 큰 글자는 자간을 좁혀야 읽힙니다.
- **Mono는 의미를 가진 곳에만** — 코드, 숫자 강조, 메타 태그. 장식 금지.
- 반응형: 모바일에서 display-lg → display-md 로 단계 하향 권장.
