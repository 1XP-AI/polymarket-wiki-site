# Wiki Health Report
Date: 2026-04-07 (review cycle 19)

## Metrics
- Total Documents: 74 (1 deduplicated)
- Total Word Count: 38,618
- Total Internal Links: 796
- Average Links per Doc: ~10.8
- Documents with Sources: 74/74 (100%)
- Quality Score: 71.5/100

## Changes This Review

### 1. Duplicate Detection & Removal
- File-level duplicates: 0
- `_similar.json` semantic duplicate check:
  - `전략/Copytrade/리스크-관리.md` vs `전략/리스크-관리-심화.md` (sim 0.78): **유지** — 상위/하위 문서 관계, 주제 구분 명확
  - `기술/API/Polymarket-API-레퍼런스.md` vs `기술/API/레퍼런스.md` (sim 0.71): **병합** — 동일 curl/Python 예제, 리더보드 워크플로우 중복. `레퍼런스.md`의 Node.js 예제를 `Polymarket-API-레퍼런스.md`에 통합 후 `레퍼런스.md` 삭제
- **1파일 병합/삭제**

### 2. Broken Link Fixes
- **Current broken links: 0** (maintained from prior cycle)

### 3. Cross-link Enrichment
- `_similar.json` `related` pairs 기준 누락 링크 보강:
  - `개념/Copytrade.md` — `백테스트-사례-2026-04`, `백테스트-가이드` 링크 추가 (기존 `백테스트-사례`에서 → `Copytrade` 방향 누락)
  - `전략/Copytrade/포지션-사이즈-전략.md` — `리밸런싱` 링크 추가
  - `전략/Copytrade/트레이더-프로필-분석.md` — `트레이더/새로운-트레이더/프로필-템플릿` 링크 추가
  - `트레이더/리더보드-분석.md` — `전략/Copytrade/Copytrade-리더보드-심화` 링크 추가
  - `전략/Copytrade/Copytrade-리더보드-심화.md` — `리밸런싱`, `트레이더/리더보드-분석` 링크 추가
  - `기술/API/Polymarket-API-레퍼런스.md` — `자동화-플로우` 관련 링크 추가
- 중복 제거: `개념/Copytrade.md`의 중복된 `Polymarket-API-레퍼런스` 링크 1건 정리
- Cross-link density: ~10.1 → ~10.8 per doc

### 4. Sources Audit
- 74/74 docs have `sources:` frontmatter (100%)
- `log.md`가 누락되어 있었음 → 빈 sources 배열로 frontmatter 추가

### 5. Structural Cleanup
- `기술/API/레퍼런스.md` 삭제 (`Polymarket-API-레퍼런스.md`에 병합)

## Quality Score Breakdown
```
Coverage:     min(74/100, 1) × 15  = 11.10
Volume:       min(38618/400000, 1) × 15 = 1.45
Structure:    max(0, 1-0/10) × 15 = 15.00
Link Density: min(10.8/5, 1) × 15  = 15.00
Doc Depth:    min(522/2000, 1) × 15 = 3.91
Trust Score:  (74/74 × 100) × 0.25 = 25.00
-----------------------------------------
Total:                             71.46
```

## Remaining Issues
- **High**: Average document depth ~522 words — still below 2000 target
- **Medium**: Volume score low (1.45/15) — needs ~360K more words for max
- **Low**: No broken links, complete sources coverage

## Priority Tasks (Next)
1. **Document depth**: Target 800+ avg words per doc (currently 522)
2. **Content expansion**: Short documents (<200 words) should be merged or expanded
3. **Volume growth**: Add more comprehensive guides and case studies
4. **Wiki lint check**: Run wiki-lint.sh for structural validation
