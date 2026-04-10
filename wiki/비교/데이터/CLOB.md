---
id: legacy_wiki_clob_064e27
title: CLOB
type: comparison
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-10T16:01:53Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 9
evidence_coverage: 1.0
confidence: medium
related_pages:
- comparison_데이터
- legacy_raw_05_badd78
- legacy_raw_fetched_2026_04_05_polymarket_markets_a295cb
- legacy_wiki_394666
- legacy_wiki_923782
- legacy_wiki_96e938
- legacy_wiki_api_polymarket_api_62ef40
- legacy_wiki_copytrade_698574
- legacy_wiki_copytrade_6a6853
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_e7d623
- legacy_wiki_copytrade_eff435
- legacy_wiki_index_925404
- legacy_wiki_polymarket_cd5a08
tags:
- comparison
sources:
- url: https://gamma-api.polymarket.com/markets?limit=10
- url: https://polymarket-bot.co/polymarket-api-tutorial
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://docs.polymarket.com/api-reference/clients-sdks
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://polyblock.trade/info/tools/polymarket-api-guide
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://rekko.ai/docs/guides/polymarket-api-guide
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://pm.wiki/learn/polymarket-api
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://www.alphascope.app/blog/polymarket-bot-tutorial
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://agentbets.ai/guides/polymarket-api-guide/
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://deepwiki.com/polymarket-arbitrage-bot/polymarket-arbitrage-bot/2.2-polymarket-clob-api-client
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
cluster: 데이터
cluster_group: API/레퍼런스
doc_role: data-reference
---
# CLOB

## 요약

<!-- para: para_001 -->
> 한 줄 요약: CLOB는 중앙지정가주문장으로, Bid/Ask 방식의 오더북 매칭을 의미합니다.

<!-- para: para_002 -->
CLOB는 주문이 가격-수량 형태로 쌓이고, 매칭 엔진이 호가를 교차시켜 체결을 발생시키는 구조입니다. Polymarket의 CLOB는 읽기용 API가 공개되어 있으며, maker에는 리베이트가 존재할 수 있습니다.

<!-- para: para_003 -->
전통적 CLOB vs Polymarket 예측시장의 차이점:

- **유동성 분포**: CLOB는 특정 호가 레벨에 유동성이 집중되나, AMM은 가격 곡선 전체에 유동성이 분포한다.
- **슬리피지 성격**: CLOB에서는 호가 깊이에 따라 체결 가격이 단계적으로 이동하는 반면, AMM은 수학적 곡선에 따라 즉시 가격이 변한다.

<!-- para: para_004 -->
- 복제자는 원 트레이더의 주문 규모와 시장의 호가 깊이를 비교해 진입 비율을 조정해야 한다(분할 진입 권장).
- 원 트레이더가 사용하는 주문 유형(마켓/리미트)과 Polymarket의 체결 메커니즘을 분석하여, 복제 알고리즘의 실패 모드를 정의해야 한다(부분 체결, 미체결, 높은 슬리피지).
- 리더보드 상위 트레이더의 행동이 호가 스냅샷과 결합될 때 시장 충격을 미리 예측할 수 있다.

<!-- para: para_005 -->
1. 호가 레벨별 잔량(depth)을 L_i라 하고, 목표 진입량을 Q라 하면 단순 누적으로 필요한 가격 수준을 찾을 수 있다.

<!-- para: para_006 -->
- 진입 규모 제한 및 분할 주문: 원 트레이더 주문의 일정 비율로만 진입하여 슬리피지 노출을 줄인다.
- 사전 유동성 검사: 거래 전 호가 깊이와 최근 체결량을 검사해 예상 슬리피지를 추정한다.
- 리스크 모니터링: 실행 후 실제 체결가와 기대가의 편차를 로깅하여 복제 전략의 성능을 지속적으로 보정한다.

<!-- para: para_007 -->
- [[Polymarket 개요]] — Polymarket의 전체 구조와 CLOB의 위치 설명
- [[Copytrade 데이터 수집 가이드]] — CLOB 특성이 Copytrade 실행리스크에 미치는 영향
- [[Polymarket API 레퍼런스]] — CLOB 읽기·모니터링을 위한 엔드포인트 참조
- [[리더보드 & 트레이더 데이터]] — 리더보드 트레이더의 대규모 주문이 오더북에 미치는 사례 분석
- [[Copytrade 데이터 수집 가이드]] — CLOB 기반 실시간 포지션 복제
- [[슬리피지(Slippage)]] — 슬리피지 정의와 완화 전략
- [[Polymarket API 레퍼런스]] — Polymarket API와 리더보드 연동 예제
