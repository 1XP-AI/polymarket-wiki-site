# Wiki Health Report
Date: 2026-04-07 (review cycle 29)

## Metrics
- Total Documents: 69 (no change)
- Total Word Count: ~47,858
- Total Content Internal Links: ~918
- Average Links per Doc: ~13.3
- Documents with Sources (URLs): 61/69 (88.4%)
- Quality Score: 69.4/100

## Changes This Review

### 1. Duplicate Detection & Removal
- File-level duplicates: 0
- Semantic duplicates (`_similar.json` duplicates 0.90+): 0
- `_similar.json` duplicate candidate: `개념/CTF.md` ↔ `기술/온체인-컨트랙트.md` (similarity 0.79) — below 0.90 threshold, no merge needed

### 2. Broken Link Fixes
- No broken links found
- All `[[링크]]` references resolve to existing files

### 3. Cross-link Enrichment
- `_similar.json` `related` pairs: 23 pairs (similarity 0.6~0.9)
- Links added/updated:
  - `Copytrade-리더보드-자동화.md` → `[[개념/Copytrade]]`, `[[전략/Copytrade/추종-실행-속도-최적화]]`, `[[전략/Copytrade/리더보드-심층-분석]]`
  - `리더보드-심층-분석.md` (frontmatter) → `[[전략/Copytrade/Copytrade-리더보드-자동화]]`
  - `Copytrade-성능-모니터링.md` → `[[전략/Copytrade/성과-분석-지표]]`, `[[전략/Copytrade/알고리즘-선별-체크리스트]]`
  - `Copytrade-성능-모니터링.md` (related section) → added sim references for 알고리즘-선별-체크리스트, 리스크-모니터링
  - `알고리즘-선별-체크리스트.md` (frontmatter) → `[[전략/Copytrade/팔로우-선별]]`, `[[전략/Copytrade/리밸런싱]]`
  - `팔로우-선별.md` (frontmatter) → `[[전략/Copytrade/리밸런싱]]`
  - `매수-타이밍-심화.md` → `[[전략/Copytrade/Copytrade-리더보드-자동화]]`
  - `개념/Copytrade.md` (frontmatter) → `[[전략/Copytrade/매수-타이밍-심화]]`
  - `리더보드-심층-분석.md` → body link for `추종-실행-속도-최적화`
  - `리스크-모니터링.md` → deduplicated frontmatter entries, added cross-links
  - `Polymarket-GitHub-리포트.md` → removed duplicate frontmatter entry `[[개념/프로그램-개요]]`

### 4. Sources Audit
- 61/69 docs have `sources:` with URLs (88.4%)
- No new source gaps introduced
- No inline footnote `[^N]` migration needed

## Quality Score Breakdown
```
Coverage:     min(69/100, 1) × 15  = 10.35
Volume:       min(47858/400000, 1) × 15 = 1.79
Structure:    max(0, 1-0/10) × 15 = 15.00
Link Density: min(13.3/5, 1) × 15  = 15.00
Doc Depth:    min(693/2000, 1) × 15 = 5.20
Trust Score:  (61/69 × 100) × 0.25 = 22.10
-----------------------------------------
Total:                             69.4/100
```

### Score Change from Cycle 28
| Metric | Cycle 28 | Cycle 29 | Δ |
|--------|----------|----------|---|
| Docs | 69 | 69 | 0 |
| Word Count | ~46,800 | ~47,858 | +1,058 |
| Avg Words/Doc | 678 | 693 | +15 |
| Avg Links/Doc | ~12.9 | ~13.3 | +0.4 |
| Sources % | 88.4% | 88.4% | 0 |
| Quality Score | 69.3 | 69.4 | +0.1 |

Score improvement driven by cross-link enrichment (+0.4 links/doc) and modest word count growth.

## Remaining Issues
- **High**: Average document depth ~693 words — still below 2000 target (~5.20/15 score)
- **Medium**: Volume score low (1.79/15) — needs ~352K more words for max
- **Medium**: 8 docs still lack URL sources
- **Low**: `_similar.json` stale entries for deleted files need cleanup
- **None**: No broken links, good cross-link density (~13.3/doc), frontmatter deduped

## Priority Tasks (Next)
1. **Document depth**: Short docs (<300 words) — merge or expand
2. **Sources coverage**: 8 docs without URL sources — add reference URLs
3. **_similar.json cleanup**: Remove stale references to deleted files
4. **Content expansion**: Target 800+ avg words per doc for depth score improvement
5. **Frontmatter consistency**: Remove duplicate entries in `related` arrays across docs
