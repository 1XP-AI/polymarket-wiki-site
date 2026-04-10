---
id: legacy_wiki_copytrade_copytrade_5e34e9
title: Copytrade 성능 모니터링
type: comparison
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T16:13:32Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 2
evidence_coverage: 1.0
confidence: medium
related_pages:
- comparison_copytrade
- legacy_wiki_0x492442eab586f242b53bda933fd5de859c8a3782_e83e3b
- legacy_wiki_923782
- legacy_wiki_clob_064e27
- legacy_wiki_copytrade_01e411
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_3f7013
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_511614
- legacy_wiki_copytrade_6a6853
- legacy_wiki_copytrade_8c09ff
- legacy_wiki_copytrade_a22c55
- legacy_wiki_copytrade_bb61e6
- legacy_wiki_copytrade_cbba22
- legacy_wiki_copytrade_copytrade_4b2b9f
- legacy_wiki_copytrade_e140b9
- legacy_wiki_copytrade_e2e01c
- legacy_wiki_copytrade_e7d623
- legacy_wiki_copytrade_eff435
- legacy_wiki_index_925404
- legacy_wiki_negative_risk_7a5dd0
- legacy_wiki_theo_e3e7fe
tags:
- comparison
sources:
- url: https://polymarketcopytrading.com/risk-management
- url: https://www.polycopytrade.net/blog/polymarket-copy-trading-risk-management.php
cluster: Copytrade
cluster_group: 리스크
doc_role: analysis
---
# Copytrade 성능 모니터링

## 요약

<!-- para: para_001 -->
> Copytrade 전략의 실행 품질과 트레이더 성과를 지속적으로 추적·계측하는 방법

<!-- para: para_002 -->
1. **복제 정확도**: 원본 트레이더 포지션 대비 팔로워 포지션 일치율

<!-- para: para_003 -->
- **실시간**(초-분): WebSocket 기반 가격·포지션 변화 감지
- **주기적**(1시간~1일): 집계 지표 계산 및 리포트 생성
- **임계치 기반**: 복제 정확도 < 90%, API 오류율 > 5% 시 경보

<!-- para: para_004 -->
- [[Copytrade 데이터 수집 가이드]] — 실시간 리스크 지표 정의 (sim 0.7273)
- [[Copytrade 데이터 수집 가이드]] — 자동화 파이프라인과 모니터링 연동
- [[Copytrade 데이터 수집 가이드]] — 리스크 정책과 연계
- [[Copytrade 데이터 수집 가이드]] — 실행 시간 최적화
- [[Copytrade 데이터 수집 가이드]] — 자동화 선별 체크리스트 (sim 0.6920)
- [[Copytrade 데이터 수집 가이드]] — 리스크 헤징 기법 (sim 0.7386)
- [[Copytrade 데이터 수집 가이드]] — 성과 분석 지표
