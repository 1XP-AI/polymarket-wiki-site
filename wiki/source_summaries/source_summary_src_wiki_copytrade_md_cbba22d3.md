---
id: source_summary_src_wiki_copytrade_md_cbba22d3
title: 'Source Summary: 알고리즘 선별 체크리스트'
type: source_summary
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-09T14:10:11Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: high
related_pages:
- legacy_wiki_copytrade_cbba22
tags:
- internal
- internal
---

# Source Summary: 알고리즘 선별 체크리스트

## Summary

<!-- para: para_001 -->
> 자동화/반자동화 환경에서 리더보드 기반 트레이더를 시스템적으로 선별하기 위한 체크리스트

## Key Facts

<!-- para: para_002 -->
리더보드 데이터와 온체인/오프체인 신호를 결합해 copytrade 대상으로 적합한 트레이더를 정량적으로 선별하는 절차와 모니터링 포인트를 제시한다.

<!-- para: para_003 -->
1. 데이터 소스 확인
   - 리더보드(Polymarket), 트랜잭션(온체인), 트위터/Reddit 언급 횟수, API 이벤트 피드 등을 우선 수집
   - 수집 주기와 신선도 기준 설정(예: 24시간 이내 활동)

2.

## Details

<!-- para: para_004 -->
- Theo와 같은 상위 트레이더를 예시로, 최근 30일 승률 65%, 평균 보유기간 3일, 평균 슬리피지 0.3% → 자동화 후보(점수 0.78)

<!-- para: para_005 -->
- [[전략/Copytrade/Copytrade-리더보드-심화]] — 리더보드에서 트레이더를 추출하는 방법
- [[전략/Copytrade/Copytrade-성능-모니터링]] — 자동화 후 성능 계측 가이드
- [[전략/Copytrade/리스크-관리]] — 팔로우 포트폴리오 리스크 규칙

(문서 생성: 1사이클 Expand 작업)

## Open Questions

<!-- para: para_006 -->
No open questions extracted.
