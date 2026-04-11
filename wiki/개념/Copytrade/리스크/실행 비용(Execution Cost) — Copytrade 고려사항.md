---
id: legacy_wiki_copytrade_e140b9
title: 실행 비용(Execution Cost) — Copytrade 고려사항
type: concept
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-11T16:39:57Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_copytrade
- legacy_wiki_923782
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://www.polymarket.com
- url: https://gamma-api.polymarket.com/markets
- url: https://docs.polymarket.com/api
- url: https://www.quantstart.com/articles/market-impact-slippage/
- url: https://www.investopedia.com/terms/s/slippage.asp
cluster: Copytrade
cluster_group: 실행
doc_role: analysis
---
# 실행 비용(Execution Cost) — Copytrade 고려사항

## 요약

<!-- para: para_001 -->
> 한 줄 요약: Copytrade에서 주문 실행 비용(수수료, 슬리피지, 시장 충격)을 정량적으로 추정하고 이를 리스크·포지션 관리에 반영하는 실무 가이드.

<!-- para: para_002 -->
Copytrade 전략은 단순히 '누구를 따라가는가'에 더해 '어떻게 실행하느냐'가 수익성에 큰 영향을 미칩니다. 실행 비용은 다음 요소로 구성됩니다.

<!-- para: para_003 -->
- 플랫폼 수수료: Polymarket은 거래 수수료를 부과. 고빈도 트레이더의 경우 누적 수수료가 수익의 상당 부분을 잠식.

<!-- para: para_004 -->
- 주문 제출 시 기대 가격과 체결 가격의 차이. [[슬리피지(Slippage)]] 문서를 참조.
- 유동성이 낮은 마켓에서 특히 심각하며, 포지션 크기에 비례하여 비선형적으로 증가할 수 있음.

<!-- para: para_005 -->
- 대형 주문이 시장 가격을 움직이는 효과. 리더의 포지션을 그대로 따라했을 때, 여러 팔로워의 동시 진입이 추가적인 비용을 유발.
- Kyle's lambda 모델 적용: 시장 충격 = λ * 주문량.

<!-- para: para_006 -->
- 주문 지연, 네트워크 지연, 리더의 주문과 팔로워 간 타이밍 차이로 인한 불이익. 자동화 시스템에서는 타이밍 동기화와 큐잉 전략이 중요.
- [[Copytrade 데이터 수집 가이드]] 참고: 실행 지연이 3초 이상이면 슬리피지가 50% 이상 증가하는 마켓 존재.

<!-- para: para_007 -->
- 매수/매도 호가 간 차이. 유동성 공급자가 드문 시장에서 스프레드가 넓어 비용 상승.
- 마감 48시간 이내 마켓은 스프레드가 급격히 축소되지만, 반대로 30일 이상 남은 마켓은 스프레드가 10~20%에 달할 수 있음.
