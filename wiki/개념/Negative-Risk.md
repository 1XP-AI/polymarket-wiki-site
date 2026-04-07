---
title: "Negative-Risk"
category: "개념"
created: "2026-04-05"
sources:
  - url: "https://www.polymarket.com"
    raw: "raw/fetched/2026-04-05-polymarket-home.md"
    added: "2026-04-05"
  - url: "https://github.com/gnosis/conditional-tokens-contracts"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-07"
  - url: "https://polymarketcopytrading.com/risk-management"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://docs.polymarket.com/advanced/neg-risk"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://github.com/Polymarket/neg-risk-ctf-adapter/"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://cryptoslate.com/polymarket-processes-1-4-billion-as-negrisk-outshines-cft-markets/"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://github.com/Polymarket/neg-risk-ctf-adapter/blob/main/docs/NegRiskAdapter.md"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://docs.polymarket.com/trading/orders/overview"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
related:
  - "[[개념/CTF]]"
  - "[[개념/CLOB]]"
  - "[[전략/리스크-관리-심화]]"
  - "[[전략/Copytrade/리스크-헤징]]"
  - "[[개념/슬리피지]]"
  - "[[마켓/정치]]"
---

# Negative-Risk (네거티브 리스크)

> 한 줄 요약: 다중 결과 이벤트에서 자본 효율적으로 포지션을 구성해 리스크를 음수로 만드는 전략적 접근입니다.

Negative-Risk는 여러 결과 중 특정 결과에만 Yes를 걸고 나머지 No를 합성해 자본 효율을 높이는 기법입니다. 다중 결과 구조에서 헤지·아비트리지 형태로 사용되며, 예시와 계산법을 제공합니다. 실무에서는 슬리피지, 수수료, 마켓 유동성 한계를 반드시 고려해야 합니다.

## 개념과 원리

### 왜 "Negative"인가?

Negative-Risk라는 이름은 직관에 반합니다. 리스크가 "음수"라는 것은 실제로 **손실 가능성이 수학적으로 배제된 포지션**을 의미합니다. 다중 결과 이벤트에서 모든结果에 대한 포지션을 적절히 조합하면, 어떤 결과가 나오더라도 수익이 고정되거나 최소한 손실이 0이 되는 구조를 만들 수 있습니다.

### CTF 기반

Negative-Risk는 [[개념/CTF]](Conditional Token Framework)에 기반합니다. CTF는 하나의 조건(이벤트)을 여러 결과로 분할(split)하고, 다시 병합(merge)할 수 있게 합니다.

예를 들어 "A/B/C 중 누가 이길까?"라는 이벤트에서:
- $1을 입금하면 Yes-A + Yes-B + Yes-C 토큰을 각각 1개씩 받음 (Split)
- 모든 결과를 사면 총 비용 $1, 결과는 어느 것이든 $1로 정산 → 리스크 0
- 하지만 시장에서 개별 가격이 $1 미만이므로, 이를 활용해 차익 거래 가능

## 수학적 구조

### 기본 예시: 3자 경쟁

세 후보 A, B, C가 있고 각각 시장 가격이 $0.40, $0.35, $0.30이라고 가정합시다.

| 전략 | 비용 | A 당첨 시 | B 당첨 시 | C 당첨 시 |
|------|------|----------|----------|----------|
| Yes-A 매수 | $0.40 | $1.00 | $0.00 | $0.00 |
| Yes-B 매수 | $0.35 | $0.00 | $1.00 | $0.00 |
| Yes-C 매수 | $0.30 | $0.00 | $0.00 | $1.00 |
| **전부 매수** | **$1.05** | **$1.00** | **$1.00** | **$1.00** |

이 경우 전부를 사면 $0.05의 확정 손실입니다. 하지만 여기서Negative-Risk 전략은:

1. **A에 확신이 있을 때**: Yes-A를 $0.40에 매수 + Yes-B와 Yes-C를 market에서 매도(short)
   - Yes-B 매도: $0.35 수입, B 당첨 시 -$1.00 손해
   - Yes-C 매도: $0.30 수입, C 당첨 시 -$1.00 손해
   - 순 비용: $0.40 - $0.35 - $0.30 = **-$0.25** (음수 비용 = 즉각적 수익)
   - A 당첨 시: $1.00 - $0 - $0 = **$1.00**
   - B 당첨 시: $0 - $1.00 - $0 = **-$1.00** (하지만 이미 $0.25를 받았으므로 순 -$0.75)

   이 간단한 예에서 핵심은 **Yes-A를 $0.40에 사면서 동시에 반대 포지션을 $0.65에 팔 수 있다**는 것입니다. 순 비용 -$0.25는 즉각적인 Arbitrage입니다.

### 실제 활용: 불균형 탐지

Negative-Risk의 실무적 가치는 시장 가격이 올바르지 않을 때 발생합니다.

- 모든 Yes 가격의 합 > $1.00 → 과도 평가, No side에서 차익 가능
- 모든 Yes 가격의 합 < $1.00 → 저평가, All-Yes 바스켓 매수 → 확정 수익

현재 Polymarket의 Neg-Risk 마켓에서는 이러한 불균형이 실시간으로 교정되지만, 뉴스 이벤트 직후 짧은 순간 기회가 발생합니다.

## Copytrade에서의 Negative-Risk

[[전략/Copytrade/리스크-헤징]]에서 Negative-Risk는 헤징 도구로 활용됩니다.

### 활용 시나리오

1. **단일 베팅 헤지**: 특정 정치 마켓에서 Yes에 진입한 후, 나머지 모든 No를 합성해 구매 → 손실 한도 고정
2. **카테고리 분산**: 정치 마켓 전문 트레이더를 카피할 때, 해당 트레이더가 집중하는 마켓의 반대 포지션을 Negative-Risk로 구성 → 트레이더의 타이밍은 유지하면서 downside 보호
3. **[[전략/리스크-관리-심화]]**의 포지션 헤지와 결합: Negative-Risk로 손실 바닥을 만들고, 특정 결과에 대한 Upside만 오픈

### 주의사항

- **[[개념/슬리피지]]**: 다중 결과 포지션을 동시에 진입할 때 각 마켓의 가격 변동으로 계획한 비용이 달라질 수 있음
- **수수료**: 여러 마켓에 동시에 진입하므로 Maker/Taker 수수료가 누적됨 ([[개념/CLOB]])
- **유동성**: 니치 정치 마켓 ([[마켓/정치]])에서는 No 토큰의 유동성이 부족해 진입/청산이 어려울 수 있음

## 구현 의사코드

```python
def check_negative_risk_opportunity(market_prices):
    """Neg-Risk 기회 탐지: 모든 Yes 가격 합이 $1과 다른 경우"""
    total_yes = sum(p['yes_price'] for p in market_prices)
    
    if total_yes < 1.0:
        # All-Yes 바스켓 매수 → 확정 수익
        profit = 1.0 - total_yes
        return {"action": "buy_all_yes", "guaranteed_profit": profit}
    
    if total_yes > 1.0:
        # All-No 바스켓 매도 → 확정 수익
        # No 가격 = 1 - Yes 가격
        total_no = sum(1 - p['yes_price'] for p in market_prices)
        return {"action": "sell_all_no", "guaranteed_profit": total_no - 1.0}
    
    return None
```

## Neg-Risk 마켓 vs 일반 마켓

Polymarket은 공식적으로 "Neg-Risk" 마켓을 지원합니다. 이는 조건부 토큰을 사용하지 않고 독립적인 Yes/No 마켓을 여러 개 만든 방식으로, CTF Split/Merge 없이도 유사한 구조를 제공합니다.

| 구분 | Neg-Risk 마켓 | CTF 기반 마켓 |
|------|--------------|--------------|
| 구조 | 독립 Yes/No 마켓 | Split/Merge를 통한 토큰 조합 |
| 리스크 | 결과가 모두 독립 | 모든 결과가 토큰으로 연결 |
| 복잡도 | 낮음 (그냥 여러 마켓) | 높음 (토큰 조합 필요) |

## 관련 문서

- [[개념/CTF]] — Conditional Token Framework (Negative-Risk의 기술적 기반)
- [[개념/CLOB]] — 주문장 기반 실행, Maker/Taker 수수료
- [[전략/리스크-관리-심화]] — 리스크 관리 심화, 포지션 헤지
- [[전략/Copytrade/리스크-헤징]] — Copytrade 컨텍스트에서의 헤징 전략
- [[개념/슬리피지]] — 다중 진입 시 가격 변동 리스크
- [[마켓/정치]] — Neg-Risk가 자주 발생하는 정치 카테고리
