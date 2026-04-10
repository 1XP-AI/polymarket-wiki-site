---
id: legacy_wiki_copytrade_01e411
title: 성과 분석 지표 (Copytrade 성능 메트릭)
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T16:13:32Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_923782
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_59552d
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_e81931
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://data.polymarket.com/leaderboard
  raw: raw/fetched/2026-04-06-polymarket-leaderboard-api.md
- url: https://polymarket.com/leaderboard?period=monthly
  raw: raw/fetched/2026-04-06-leaderboard-monthly-2.md
- url: https://gamma-api.polymarket.com/markets
  raw: raw/fetched/2026-04-05-polymarket-markets.md
- url: https://docs.polymarket.com/api
  raw: raw/fetched/2026-04-06-polymarket-docs.md
- url: https://www.quantstart.com/articles/market-impact-slippage/
  raw: raw/fetched/2026-04-06-quantstart-slippage.md
---
# 성과 분석 지표 (Copytrade 성능 메트릭)

## 요약

<!-- para: para_001 -->
> Copytrade 대상의 성과를 계량적으로 평가하고 비교하기 위한 핵심 지표, 계산법, 실제 적용 패턴을 정리한다.

<!-- para: para_002 -->
Copytrade에서는 단순한 승률만으로 트레이더를 평가하면 오판할 위험이 크다. 고승률 + 저거래수 트레이더는 우연에 의한 결과일 수 있으며, 리더보드의 기간별 순위는 특정 마켓 이벤트에 편향될 수 있다.

<!-- para: para_003 -->
| 지표 | 계산식 | 해석 |
|------|--------|------|
| 순수익(ROI) | 기간수익 / 평균포지션규모 | 절대적 수익 수준 |
| 연환산화 수익률 | `(1 + ROI)^(365/일수) - 1` | 기간 차이 보정 |
| 누적수익곡선 | 일자별 누적 PnL 시계열 | 지속성 시각화 |

<!-- para: para_004 -->
| 지표 | 계산식 | 권장 임계값 |
|------|--------|-------------|
| 변동성(Volatility) | `std(포지션별수익률)` | 낮을수록 안정적 |
| 샤프 유사 비율 | `(평균수익 - 시장평균) / 수익Std` | >1.0 권장 |
| Sortino 비율 | `(평균수익 - 시장평균) / downside_std` | >1.2 권장 |
| 최대 낙폭(MDD) | `(최저점 - 최고점) / 최고점` | >15% 면 경고 |
| Calmar 비율 | `연환산화수익 / abs(MDD)` | >2.0 우수 |

Prediction market 특성상 "무위험이자율" 대신 **시장 평균 수익률**을 베이스라인으로 사용한다. 예를 들어 상위 50개 마켓의 평균 수익률이 5%라면, 이를 무위험수익 대용으로 차감한다.

<!-- para: para_005 -->
| 지표 | 측정 | 활용 |
|------|------|------|
| 승률(Win Rate) | 수익거래 / 총거래 | 기본 필터, 단독사용 금지 |
| 기대값(EV) | `승률×평균이익 - (1-승률)×평균손실` | EV > 0 이면 장기 흑자 기대 |
| 홀딩 타임 | 평균 `청산시간 - 진입시간` | 단타vs장기 분류 |
| 거래 빈도 | 30일당 거래건수 | 실행비용 민감도 판단 |
| 평균 베팅 사이즈 | `총베팅액 / 거래건수` | 자본 요구량 추정 |
| 연속승/패 스크 streak | 최장연승, 최장연패 | 심리적 압박도 측정 |

<!-- para: para_006 -->
| 지표 | 측정 | 중요성 |
|------|------|--------|
| 부분체결 비율 | 부분체결건 / 총주문건 | >30% 면 유동성 경고 |
| 평균 슬리피지 | `체결가 - 기대가` | [[슬리피지(Slippage)]] 참고 |
| 시장 충격비용 | 대형주문 전후 가격 차이 | [[Copytrade 데이터 수집 가이드]] |

<!-- para: para_007 -->
각 지표를 z-score로 표준화 후 가중합하여 종합 점수를 산출한다. python

```python
def compute_trader_score(metrics: dict, weights: dict) -> float:
    """
    트레이더 종합 점수 계산
```

metrics keys: win_rate, sharpe, mdd, volume, recency, holding_days
    weights keys: 동일 (총합 1.0)
    """
