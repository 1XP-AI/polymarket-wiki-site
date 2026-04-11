---
id: legacy_wiki_copytrade_c6dea0
title: Copytrade 포지션 리밸런싱 가이드
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T23:20:14Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 7
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_copytrade
- legacy_raw_03_copytrade_c17abe
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_59552d
- legacy_wiki_copytrade_8c09ff
- legacy_wiki_copytrade_e2e01c
tags:
- concept
sources:
- url: https://www.polymarket.com
- url: https://gamma-api.polymarket.com/markets
- url: https://docs.polymarket.com/api
- url: https://data.polymarket.com/leaderboard
- url: https://www.quantstart.com/articles/market-impact-slippage/
- url: https://polymarketanalytics.com/traders
- url: https://www.investopedia.com/terms/h/hedge.asp
cluster: Copytrade
cluster_group: 실행
doc_role: playbook
---
# Copytrade 포지션 리밸런싱 가이드

## 요약

<!-- para: para_001 -->
> 포지션 리밸런싱은 따라가기(copytrade) 전략에서 위험을 일정 수준으로 유지하기 위해 주기적으로 또는 이벤트 기반으로 포지션 규모를 조정하는 과정이다.

<!-- para: para_002 -->
Copytrade 환경에서는 팔로우 대상 트레이더의 진입/청산 신호를 단순 복제하는 것만으로는 리스크 관리가 어렵다. 트레이더의 레버리지, 포지션 규모, 시장 변동성에 따라 선행 리밸런싱(rebalancing) 또는 후행 리밸런싱이 필요하다.

<!-- para: para_003 -->
- 포지션 당 위험(예: 금전적 손실 한도)을 일정 범위로 유지
- 계정 전체 위험노출(총 포지션 대비 비율)을 관리
- 트레이더의 급격한 포지션 확대/축소에 의해 발생하는 슬리피지 및 청산 위험 완화
- 포트폴리오 내 마켓 간 상관관계 변화 대응 — 두 마켓이 예상 외로 높은 상관관계를 가지게 되면 노출 집중 발생

<!-- para: para_004 -->
- 계정 자본의 X%를 각 팔로우 포지션에 할당
- 팔로우 대상이 기존 대비 포지션 규모를 n배로 늘리면, 내 복제 포지션은 사전에 정한 비율로 제한
- 장점: 단순 구현, 예측 가능한 최대 손실
- 단점: 리더의 전략을 충분히 복제하지 못할 수 있음

<!-- para: para_005 -->
- 포지션의 달러(또는 스테이블) 가치 상한/하한 설정
- 트레이더 포지션이 상한을 넘으면 차액을 축소하여 리스크 유지
- 시장 가격 변동에 따라 명목 가치가 변하므로 일일 재계산 권장

<!-- para: para_006 -->
- 변동성(VIX 유사 지표) 상승, 주문장 깊이 급감, 중요한 뉴스 발생 시 자동 축소
- Polymarket 특정 이벤트: 선거 토론, 법정 판결, 주요 스포츠 결과 발표 전 24시간 내 포지션 50% 축소 권장
- 이벤트 종료 후 점진적 복귀 (full position까지 3~5단계 스케일인)

<!-- para: para_007 -->
- 팔로우 중인 포지션 간 상관관계가 0.7+로 상승하면, 두 포지션의 합산 노출을 단일 포지션 상한으로 관리
- Polymarket에서는 관련 이벤트(예: "A후보 당선"과 "B당 승리")가 높은 상관관계를 보이므로 주의

## 세부 내용

<!-- para: para_008 -->
| 주기 | 방식 | 적합한 상황 |
|------|------|-------------|
| 일일 | 비율 재계산, 상한 점검 | 일반 운영 |
| 이벤트 전 | 포지션 50% 축소 | 선거, 큰 발표 |
| 실시간 | API 트리거 기반 | 고빈도 자동화 |
| 주간 | 포트폴리오 전체 재검토 | 전략 리셋 |

<!-- para: para_009 -->
- 최대 포지션 노출: 계정 자본의 5~10%
- 슬리피지 버퍼: 예상 슬리피지 대비 추가 1~2%
- 동시 팔로우 수 제한: 10~20명 이내
- 최대 동시 마켓 노출: 계정 자본의 30% 이내

<!-- para: para_010 -->
```python
if trader_position_size > max_allowed_multiplier:
    target_size = base_size * max_allowed_multiplier
else:
    target_size = trader_position_size * my_follow_ratio

place_order(size=target_size)
```

<!-- para: para_011 -->
운용 단계에서는 Polymarket API로 프로파일과 포지션을 조회하고, 주문장 깊이를 확인한 뒤 진입 시점을 조정해야 한다. Rate limit을 고려해 배치 주문을 쓰고, 유동성 얕은 마켓에서는 리밸런싱 빈도 자체를 낮추는 편이 안전하다.

<!-- para: para_012 -->
- 관련 문서: [[Copytrade 자동화 플로우]], [[포지션 사이즈 전략]], [[Copytrade 리스크 관리]], [[Copytrade]], [[팔로우 선별]]
