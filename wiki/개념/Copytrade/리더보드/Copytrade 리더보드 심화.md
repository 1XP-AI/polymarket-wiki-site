---
id: legacy_wiki_copytrade_copytrade_4b2b9f
title: Copytrade 리더보드 심화
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-10T09:55:17Z'
as_of: '2026-04-10'
owners:
- wiki-system
source_count: 8
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_03_copytrade_c17abe
- legacy_raw_05_badd78
- legacy_wiki_0x492442eab586f242b53bda933fd5de859c8a3782_e83e3b
- legacy_wiki_4526f6
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_bb99a4
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://data.polymarket.com/leaderboard
- url: https://gamma-api.polymarket.com/markets
- url: https://polymarketanalytics.com/traders
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
- url: https://www.predictengine.ai/blog/how-to-use-polymarket-leaderboard
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
- url: https://laikalabs.ai/prediction-markets/top-polymarket-traders
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
- url: https://merlin.trade/leaderboard
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
- url: https://data-api.polymarket.com/v1/leaderboard
  raw: raw/fetched/2026-04-05-leaderboard-monthly.md
- url: https://polyburg.com/polymarket-top-traders
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
---
# Copytrade 리더보드 심화

## 요약

<!-- para: para_001 -->
> 리더보드 상위 계정을 단순 순위표가 아니라 "추종 후보 풀"로 해석하기 위한 선별 기준과 점수화 관점을 정리한 문서

<!-- para: para_002 -->
리더보드에서 중요한 것은 순위 자체보다 순위를 만든 거래 습관이다. 수익이 높아도 소수 대형 적중형인지, 지속적으로 거래하는 일관형인지에 따라 copytrade 적합성은 크게 달라진다.

## 우선 확인할 소스 계층

<!-- para: para_003 -->
기준점은 공식 리더보드와 공식 프로필 데이터다. 외부 대시보드는 교차검증이나 설명 보조에는 유용하지만, 후보 필터의 기준은 항상 공식 데이터 축으로 두는 편이 안정적이다.

<!-- para: para_004 -->
외부 대시보드가 도움이 되는 지점은 세 가지다. 첫째, 특정 지갑을 더 빠르게 찾을 수 있다. 둘째, ROI나 conviction처럼 공식 문서에 없는 파생 지표를 참고할 수 있다. 셋째, 여러 랭킹 축을 비교하며 과대평가된 계정을 걸러낼 수 있다.

## 후보 선별 지표

<!-- para: para_005 -->
리더보드 심화 단계에서는 `수익 규모`, `거래량 대비 효율`, `활동 지속성`, `포지션 집중도`, `손실 이후 회복력`을 함께 본다. 이 다섯 항목을 같이 봐야 일시적 급등 계정과 반복 가능한 전략 계정을 구분할 수 있다.

<!-- para: para_006 -->
예를 들어 거래량 대비 수익 비율이 과도하게 높은 계정은 한두 번의 대형 적중이 반영됐을 가능성이 있다. 반대로 거래량이 매우 크고 수익이 완만한 계정은 일관성은 높지만 추종 시 슬리피지 비용이 빠르게 누적될 수 있다.

<!-- para: para_007 -->
실무적으로는 "상위 10위 전체를 따라간다"보다, 상위권 중에서 거래 패턴이 다른 두세 명을 골라 비교하는 접근이 낫다. 이 비교는 [[트레이더 프로필 분석]]과 함께 읽을 때 가장 유용하다.

## 운영 해석

<!-- para: para_008 -->
리더보드 심화 문서는 후보를 줄이는 단계다. 실제 자동화 설계나 주문 복제 로직을 바로 설명하는 문서는 아니다. 따라서 이 문서의 출력은 "누가 팔로우 후보인가"이며, 다음 단계는 [[Polymarket Copytrade 전략 분석]]이나 [[Copytrade 자동화 플로우]]로 넘어가야 한다.

<!-- para: para_009 -->
정리하면 리더보드 심화는 순위표를 읽는 기술이 아니라 후보 풀을 정제하는 기술이다. 점수는 출발점일 뿐이고, 실제 추종 여부는 프로필·포지션·리스크 규칙까지 붙여서 판단해야 한다.
