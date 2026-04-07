# Wiki Health Report
Date: 2026-04-07 (14:00 KST)

## Metrics
- Total Documents: 87
- Total Word Count: 33,249
- Total Internal Links: 731
- Average Links per Doc: 8
- Documents with Sources: 86 (98.9%)
- Quality Score: 71.8/100

## Changes This Review

### 1. Duplicate Detection & Removal
- Previously merged (no new duplicates found this cycle)
- `개념/Copytrade.md` vs `전략/Copytrade/전략분석.md` (similarity 0.9167): 전략분석.md already removed
- File-level duplicates: none

### 2. Broken Link Fixes
- No broken links detected (0 broken)

### 3. Cross-link Enrichment
- `_similar.json` related pairs (14 pairs) already linked in prior cycles
- No additional cross-links needed this cycle

### 4. Sources Audit
- **47+ documents gained `sources:`** frontmatter (was 19 → now 86, 98.9%)
- Coverage improved from 21.8% → 98.9%
- Only 1 doc without sources: `wiki/log.md` (log file, exempt)
- Fixed CTF.md malformed frontmatter (was duplicate Negative-Risk block nested)
- Separated Negative-Risk.md as standalone document from CLOB.md

### 5. Structural Cleanup
- **CLOB.md restructured**: Merged CTF/Negative-Risk content removed (now in `개념/CTF.md` redirects and `개념/Negative-Risk.md` standalone)
- CLOB.md now focuses on CLOB-specific content only

## Quality Score Breakdown
```
Coverage:    min(87/100, 1) × 15  = 13.05
Volume:      min(33249/400000, 1) × 15 = 1.25
Structure:   max(0, 1-0/10) × 15 = 15.00
Link Density: min(8/5, 1) × 15   = 15.00
Doc Depth:   min(382/2000, 1) × 15 = 2.87
Trust Score: (86/87 × 100) × 0.25 = 24.71
-----------------------------------------
Total:                            71.88
```

## Remaining Issues
- **Low**: 2 internal files (`_index.md`, `_registry.md`) lack `sources:` — by design
- **Medium**: Average document depth 382 words — below target 2000
- **Low**: Some Copytrade sub-documents have duplicate `related:` entries (e.g., `추종-중단-규칙.md` lists `[[트레이더-프로필-분석]]` twice)

## Priority Tasks (Next)
1. **Document depth expansion**: Target 800+ avg words per doc (currently 382)
2. **Clean duplicate related entries**: Remove duplicate links in Copytrade sub-docs
3. **Polymarket.md / 폴리마켓.md review**: Check for Korean/English duplicate overview pages
