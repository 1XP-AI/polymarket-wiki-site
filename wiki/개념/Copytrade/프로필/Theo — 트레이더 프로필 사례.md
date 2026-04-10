---
id: legacy_wiki_theo_e3e7fe
title: Theo — 트레이더 프로필 사례
type: concept
status: verified
created_at: '2026-04-09T14:10:12Z'
last_updated: '2026-04-09T16:13:32Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_bb99a4
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_e7d623
- legacy_wiki_copytrade_eff435
- legacy_wiki_link_2026_04_05_4bcb54
tags:
- concept
sources:
- url: https://polymarket.com/leaderboard
  raw: raw/fetched/2026-04-06-polymarket-leaderboard-api.md
- url: https://data-api.polymarket.com/v1/leaderboard
  raw: raw/fetched/2026-04-06-data-api-leaderboard.md
- url: https://polymarketanalytics.com/traders
  raw: raw/fetched/2026-04-05-polymarket-analytics.md
- url: https://www.ai-polymarket.com/polytrader/copy-trading.html
  raw: raw/fetched/2026-04-06-copytrade-sources.md
- url: https://alphawhale.trade/blog/posts/polymarket-copy-trading-guide
  raw: raw/fetched/2026-04-06-copytrade-sources.md
cluster: Copytrade
cluster_group: 프로필
doc_role: example
---
# Theo — 트레이더 프로필 사례

## 요약

<!-- para: para_001 -->
> 리더보드 상위 랭커이자 copytrade 팔로우 대상으로 자주 인용되는 트레이더 사례 프로필

<!-- para: para_002 -->
Theo는 Polymarket 리더보드에서 꾸준히 상위권에 랭크되는 트레이더로, copytrade 전략에서 '팔로우-worthy'한 사례로 여러 가이드에서 참조된다. 이 문서는 Theo의 프로필을 예시로 삼아 **실제 트레이더 분석 방법론**을 적용한 사례 연구이다.

<!-- para: para_003 -->
리더보드 API와 Polymarket Analytics 데이터를 기준으로 한 지표(예시 스냅샷):

| 지표 | 값(예시) |
|------|---------|
| 리더보드 순위(월간) | Top 10 |
| 누적 PnL | $200k ~ $500k 범위 |
| 평균 승률 | 55-65% |
| 거래 빈도 | 주당 5-15회 |
| 선호 마켓 | 정치, 크립토, 거시 |

> 실제 최신 데이터는 `https://data-api.polymarket.com/v1/leaderboard`와 `https://polymarketanalytics.com/traders`에서 확인해야 한다.

<!-- para: para_004 -->
Theo의 포지션 히스토리를 보면 **이벤트 임박 전 early entry** 경향이 관찰된다:

- 여론조사/뉴스 발표 직후, 시장 가격이 아직 반영되지 않은 시점에 진입
- 정보 우위(information edge)보다는 **속도 우위(speed edge)**에 가까운 패턴
- 관련: [[Copytrade 데이터 수집 가이드]] — 추종 시 레이턴시 최소화가 핵심

<!-- para: para_005 -->
- 대형 마켓: 계정 자본의 2-5% 수준으로 분할 진입
- 소형 마켓(유동성 낮음): 0.5-1% 이하로 제한
- 관련: [[Copytrade 데이터 수집 가이드]] — 유동성 기반 사이징 규칙 적용

<!-- para: para_006 -->
- 결과가 명확해질 때까지 홀딩하는 경향(HODL)
- 일부 포지션은 부분 익절, 나머지는 정산까지 보유
- 손절 기준이 명확하지 않아 copytrade 추종 시 자체 스토프로스 필요

<!-- para: para_007 -->
| 기준 | 평가 |
|------|------|
| 일관성 | 양호 — 장기간 상위 랭크 |
| 샘플 크기 | 충분 — 수백 회 거래 |
| 전략 투명성 | 낮음 — 공개 소셜 부재 |
| 유동성 영향 | 중 — 대형 마켓 중심이라 슬리피지 작음 |
| 리스크 | 전략 변경 가능성, 과도한 추종으로 인한 클러스터 리스크 |
