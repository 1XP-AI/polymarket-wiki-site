# Health report

**Last Review: 2026-04-06**

## Summary
- total_docs: 90 (중복 제거: 트레이더-검증-체크리스트.md, 포지션-관리.md)
- total_words: 32,602
- avg_words_per_doc: 362 words
- dead_links: 0
- avg_links_per_doc (본문): 0 (심각한 문제)
- docs_with_sources: 20 / 90 (22.2%)
- quality_score: 31.05 / 100

## Quality Breakdown
- 커버리지: 13/15 (90 docs vs 100 target)
- 볼륨: 1/15 (32.6k words vs 400k target)
- 구조: 15/15 (dead links 없음)
- 링크 밀도: 0/15 (본문 링크 전무 - critical)
- 문서 깊이: 2/15 (평균 362 words vs 2000 target)
- 신뢰도: 0.05/0.25 (22% sources)

## Critical Issues
1. **본문 위키링크 부재** (0개)
   - 90개 중 90개 문서가 본문에 [[링크]]가 없음
   - frontmatter의 related 필드만 있음
   - 즉시 해결 필요

2. **출처(sources) 부족** (71개 문서)
   - 다음 20개를 제외한 모든 문서에 sources가 필요:
     - Copytrade 관련 문서 (개념/전략)
     - 기술 문서 (API, WebSocket, 온체인)
   - truth_score 개선 필요

3. **문서 깊이 부족**
   - 평균 362 words vs 목표 2000 words
   - 많은 문서가 100줄 미만의 stub 상태

## Completed in this review
✓ 중복 제거
  - 트레이더-검증-체크리스트.md → 트레이더-프로필-분석.md에 병합 후 삭제
  - 포지션-관리.md → 포지션-사이즈-전략.md로 통합 후 삭제
  - 관련 링크 5곳 업데이트

✓ 빈 링크 점검
  - 깨진 [[링크]] 없음 (모두 정상)

✓ frontmatter 오류 수정
  - 트레이더/Theo/프로필.md YAML 오류 수정

## Next Priority Actions
1. **본문 위키링크 추가** (현재: 0 → 목표: 3+)
   - _similar.json의 related 배열을 본문에 추가
   - 각 문서마다 최소 2~3개의 교차 링크 추가
   - "## 관련 문서" 섹션에 [[파일명]] 형식으로 기록

2. **주요 문서 sources 추가** (20 → 60+)
   - 우선순위: Copytrade-전략.md, 전략분석.md, 개념-Copytrade.md
   - raw/sources.md 또는 raw/fetched/* 파일 참조

3. **문서 깊이 확대** (362 → 1000+)
   - stub 문서 통합 또는 상세 작성
   - 예: 30줄 미만 문서 87개 → 병합/삭제

## 통계
- 중복 제거됨: 2개
- 수정된 파일: 13개
- 추가된 링크: 0개 (아직 작업 미완료)
- 변경사항: git rm 2, git add/modify 13
