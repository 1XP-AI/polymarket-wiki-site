---
id: legacy_wiki_copytrade_copytrade_4b2b9f
title: Copytrade-리더보드-심화
type: concept
status: draft
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T14:10:10Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_copytrade_copytrade_md_4b2b9fdc
tags:
- concept
- internal
---

# Copytrade-리더보드-심화

## 요약

<!-- para: para_001 -->
> 리더보드 데이터를 기반으로 Copytrade 대상을 선별·스코어링·추적하는 체계를 구축합니다. 단순 순위가 아닌 "누구를 따라 거래할 것인가"의 답을 구조화합니다.

## 핵심 사실

<!-- para: para_002 -->
이 문서는 Polymarket 리더보드에서 발견되는 트레이더 기록을 심화 분석하여 Copytrade 대상 선별에 직접 활용할 수 있는 지표와 워크플로우를 제안합니다. 목적은 "누구를 따라 거래할 것인가"에 대한 의사결정을 구조화하고, 리스크 관리를 위해 정량·정성적 신호를 결합하는 것입니다.

<!-- para: para_003 -->
Polymarket 리더보드는 단일 공식 엔드포인트가 아니라 여러 소스에서 각기 다른 형태로 제공됩니다. | 소스 | URL | 특징 |
|------|-----|------|
| 공식 월간 | `https://data-api.polymarket.com/v1/leaderboard?window=monthly` | PnL 기준, 가장 공식적 |
| 공식 전체 | `https://clob.polymarket.com/rewards/leaderboard` | 리워드 기준, maker 활동 반영 |
| PolymarketAnalytics | `https://polymarketanalytics.com/traders` | 지갑별 PnL, 승률, 포지션 동시 조회 |
| PolyBurg | `https://polyburg.com/polymarket-top-traders` | 실시간 랭킹 + conviction score |
| Merlin.trade | `https://merlin.trade/leaderboard` | ROI·PnL·Volume 동시 정렬 |
| LaikaLabs | `https://laikalabs.ai/prediction-markets/top-polymarket-traders` | copy-ready 지갑 + 전략 요약 |

Copytrade 봇은 **공식 API를 폴링 기준으로 삼고**, 타 플랫폼은 교차검증용으로 활용합니다.

## 세부 내용

<!-- para: para_004 -->
raw/fetched/2026-04-05-leaderboard-monthly.md에서 상위 10위:

| 순위 | 지갑 | PnL | 거래량 | PnL/Vol 비율 |
|------|------|-----|--------|-------------|
| 1 | 0x4924...3782 | $848,046 | $823,673 | 103% |
| 2 | Countryside | $666,795 | $21,585 | 3,089% |
| 3 | BBPK | $356,683 | $1,322,967 | 27% |

**해석 키워드**: PnL/Vol 비율이 100%를 초과하면 소수 대형 베팅에서 적중, 낮으면 고빈도 소규모 거래형입니다. Copytrade 관점에서는 전자가 신호당 기대수익은 높으나 샘플 리스크가 크고, 후자는 일관성은 높으나 [[전략/Copytrade/실행-비용]](슬리피지+수수료) 누적 영향을 더 받습니다. 자세한 분석은 [[트레이더/0x492442eab586f242b53bda933fd5de859c8a3782]] 참조.

<!-- para: para_005 -->
각 지표를 계산하는 구체적인 방법을 제시합니다.

<!-- para: para_006 -->
```
30일 수익률 = (현재 지갑 가치 - 30일 전 지갑 값) / 30일 전 지갑 값
승률(30일) = (수익 거래 수) / (총 거래 수)
기대값(EV) = (승률 × 평균승폭) - ((1-승률) × 평균패폭)
```

- **Copytrade 필터**: 30일 수익률 > 0 AND 거래수 >= 10
- EV > 0.05(5%) 이상이면 "신호당 기대 긍정"으로 분류

<!-- para: para_007 -->
```
샤프 비율(30일) = (일평균수익 - 무위험금리) / 일수익표준편차
승률 std = rolling 7일 승률의 표준편차
```

- 승률 std < 15%: tinggi nhất quán
- 샤프 > 1.0: 위험조정 수익 양호
- 샤프 < 0.5: 변동성 대비 수익 부족

## 열린 질문

<!-- para: para_008 -->
| 공식 월간 | `https://data-api.polymarket.com/v1/leaderboard?window=monthly` | PnL 기준, 가장 공식적 |

## 관련 페이지

<!-- para: para_009 -->
소스 요약: source_summary_src_wiki_copytrade_copytrade_md_4b2b9fdc
