---
id: legacy_wiki_923782
title: 슬리피지(Slippage)
type: concept
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-10T16:01:53Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 3
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_리스크
- legacy_wiki_clob_064e27
- legacy_wiki_copytrade_01e411
- legacy_wiki_copytrade_6a6853
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_e140b9
- legacy_wiki_copytrade_e7d623
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://polymarketcopytrading.com/risk-management
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
- url: https://www.ai-polymarket.com/polytrader/copy-trading.html
  raw: raw/fetched/2026-04-06-copytrade-sources.md
- url: https://www.polycopy.dev/guides/how-to-copy-trade-polymarket
  raw: raw/fetched/2026-04-06-copytrade-sources.md
cluster: 리스크
cluster_group: 핵심 리스크
doc_role: analysis
---
# 슬리피지(Slippage)

## 요약

<!-- para: para_001 -->
> 주문 체결 시 기대 가격과 실제 체결 가격의 차이로 인한 손실 또는 비용

<!-- para: para_002 -->
슬리피지(영어: Slippage)는 주문이 감지되거나 전송된 시점의 기대 가격과 실제 체결 가격 사이의 차이로 발생하는 비용이며, 특히 대형 주문·저유동성 시장·지연 상황에서 커진다.

<!-- para: para_003 -->
슬리피지는 다음 요인으로 발생한다:

- 유동성 부족: 주문량이 시장의 호가 깊이를 초과하면 거래가 점진적으로 더 불리한 가격대에서 체결된다.
- 시간 지연(Latency): 거래 감지 → 주문 전송 → 체결에 이르는 시간차 동안 가격이 변동한다.

<!-- para: para_004 -->
Copytrade에서는 원 트레이더의 주문을 따라 빠르게 진입해야 하므로 슬리피지는 직접적인 수익 감소 요인이다. 특히 원 트레이더가 대형 포지션을 열거나 빠르게 연속 거래를 할 때 복제자(copytrader)는 높은 슬리피지를 경험할 가능성이 크다. 슬리피지는 단순한 수수료보다도 복제 성과에 큰 영향을 미칠 수 있다.

<!-- para: para_005 -->
- 포지션 크기 제한: [[Copytrade 데이터 수집 가이드]]의 권장 비율에 따라 원 트레이더 주문 대비 작은 비율로 진입한다.
- 슬리피지 한도 설정: 예상 최대 슬리피지 이상이면 진입 취소(리미트 또는 스프레드 기반 진입).
- 유동성 고려: 마켓의 호가 깊이와 최근 체결량을 모니터링하여 대형 주문을 회피.

<!-- para: para_006 -->
아래는 슬리피지를 측정하고 요약 통계를 계산하는 간단한 예제입니다. 실제 운영에서는 체결 히스토리와 감지 시점의 기대가(또는 원 트레이더의 진입 가격)를 정합해야 합니다. 수식 예제:

- 절대 슬리피지_i = executed_price_i

- 상대 슬리피지_i (%) = (executed_price_i

<!-- para: para_007 -->
df = pd.DataFrame({

'expected_price': [0.40, 0.41, 0.39, 0.42],

'executed_price': [0.44, 0.405, 0.395, 0.43]
