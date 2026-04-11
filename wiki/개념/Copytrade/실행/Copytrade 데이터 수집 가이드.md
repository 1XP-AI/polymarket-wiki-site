---
id: legacy_wiki_copytrade_eff435
title: Copytrade 데이터 수집 가이드
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-11T11:42:46Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 2
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_copytrade
- legacy_raw_00_index_ec3366
- legacy_raw_05_badd78
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
- legacy_wiki_copytrade_bb99a4
- legacy_wiki_copytrade_cbba22
- legacy_wiki_copytrade_copytrade_4b2b9f
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_e140b9
- legacy_wiki_copytrade_e2e01c
- legacy_wiki_copytrade_e7d623
- legacy_wiki_index_925404
- legacy_wiki_negative_risk_7a5dd0
- legacy_wiki_theo_e3e7fe
tags:
- concept
sources:
- url: https://polymarketanalytics.com/traders
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
- url: https://polycopy.app/discover
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
cluster: Copytrade
cluster_group: 실행
doc_role: playbook
---
# Copytrade 데이터 수집 가이드

## 요약

<!-- para: para_001 -->
> Copytrade 전략 수립을 위해 필요한 데이터 소스와 수집/저장/검증 방법을 정리한 가이드입니다.

<!-- para: para_002 -->
1. 목적

- 리더보드, 포지션, 거래내역 등 트레이더 행동 데이터를 수집하여
  - 카피 후보 선별
  - 전략 패턴 분석
  - 백테스트 및 리스크 모델링

<!-- para: para_003 -->
- [[리더보드 & 트레이더 데이터]] — API 필드 및 활용법
