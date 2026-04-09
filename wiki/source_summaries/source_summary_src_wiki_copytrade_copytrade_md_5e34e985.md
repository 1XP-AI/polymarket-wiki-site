---
id: source_summary_src_wiki_copytrade_copytrade_md_5e34e985
title: 'Source Summary: Copytrade 성능 모니터링'
type: source_summary
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T14:10:10Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: high
related_pages:
- legacy_wiki_copytrade_copytrade_5e34e9
tags:
- internal
- internal
---

# Source Summary: Copytrade 성능 모니터링

## Summary

<!-- para: para_001 -->
> Copytrade 전략의 실행 품질과 트레이더 성과를 지속적으로 추적·계측하는 방법

## Key Facts

<!-- para: para_002 -->
1. **복제 정확도**: 원본 트레이더 포지션 대비 팔로워 포지션 일치율
2.

<!-- para: para_003 -->
- **실시간**(초-분): WebSocket 기반 가격·포지션 변화 감지
- **주기적**(1시간~1일): 집계 지표 계산 및 리포트 생성
- **임계치 기반**: 복제 정확도 < 90%, API 오류율 > 5% 시 경보

## Details

<!-- para: para_004 -->
- [[전략/Copytrade/리스크-모니터링]] — 실시간 리스크 지표 정의 (sim 0.7273)
- [[전략/Copytrade/자동화-플로우]] — 자동화 파이프라인과 모니터링 연동
- [[전략/Copytrade/리스크-관리]] — 리스크 정책과 연계
- [[전략/Copytrade/추종-실행-속도-최적화]] — 실행 시간 최적화
- [[전략/Copytrade/알고리즘-선별-체크리스트]] — 자동화 선별 체크리스트 (sim 0.6920)
- [[전략/Copytrade/리스크-모니터링]] — 리스크 헤징 기법 (sim 0.7386)
- [[전략/Copytrade/성과-분석-지표]] — 성과 분석 지표

## Open Questions

<!-- para: para_005 -->
No open questions extracted.
