---
title: "CTF (Conditional Token Framework)"
category: "개념"
created: "2026-04-05"
sources:
  - url: "https://www.polymarket.com"
    added: "2026-04-05"
  - url: "https://github.com/gnosis/conditional-tokens-contracts"
    added: "2026-04-05"
  - url: "https://docs.polymarket.com/advanced/neg-risk"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://github.com/Polymarket/neg-risk-ctf-adapter/"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://github.com/Polymarket/neg-risk-ctf-adapter/blob/main/docs/NegRiskAdapter.md"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://cryptoslate.com/polymarket-processes-1-4-billion-as-negrisk-outshines-cft-markets/"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://deepwiki.com/qualiaenjoyer/polymarket-apis/3.2-negative-risk-markets"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
---

# CTF (Conditional Token Framework)

> Polymarket 예측시장의 토큰 기반 — 조건부 토큰을 Split/Merge/Join하여 다중 결과 마켓을 구성하고 청산하는 프레임워크

## 개요

CTF(Conditional Token Framework)는 Gnosis(현 Conditional Tokens)에서 개발한 ERC-1155 기반 스마트 컨트랙트 표준입니다. Polymarket의 초기 핵심 인프라로, 하나의 예측 이벤트를 여러 조건부 결과 토큰으로 분할하고, 거래 후 다시 병합하여 정산할 수 있게 합니다.

핵심 불변식: **1 USDC = Yes₁ + Yes₂ + … + Yesₙ** (n개 결과의 완전한 집합)

이 불변식이 CTF의 기초입니다. $1을 컨트랙트에 입금(split)하면 모든 결과 토큰을 각각 1개 받고, 반대로 모든 결과 토큰을 1개씩 모아서 컨트랙트에 보내면(join/merge) $1을 돌려받습니다. 어떤 결과가 발생하더라도 이 관계가 성립하므로, 시스템 전체적으로 리스크가 없습니다.

## 세 가지 핵심 연산

### 1. Split (분할)

USDC를 조건부 토큰 집합으로 변환합니다.

```
split(collectionId, indexSet, amount)
→ 각 outcome별로 amount만큼의 토큰 발급
```

예: "A vs B" 바이너리 마켓에서 $100 Split
- 입력: $100 USDC
- 출력: Yes-A 100개 + Yes-B 100개
- 비용: $100, 가치: $100 (어떤 결과가 나와도 $100 정산)

Split 자체는 리스크가 없습니다. 다만 가스비가 발생하고, 토큰을 시장에 내놓는 순간 가격 변동에 노출됩니다.

### 2. Merge (병합)

조건부 토큰 집합을 USDC로 되돌립니다.

```
merge(collectionId, indexSet, amount)
→ 각 outcome 토큰 amount개 소각 → USDC 환불
```

포지션을 청산하거나 확정 손익을 실현할 때 사용합니다. Split의 역연산입니다.

### 3. Join / Position 조합

서로 다른 마켓의 토큰을 결합해 더 복잡한 조건부 포지션을 만들 수 있습니다. 예를 들어 "A가当选 AND B가 금리인상" 같은 복합 조건은 두 마켓 토큰의 교집합으로 표현 가능합니다.

## Polymarket에서의 실제 동작

Polymarket의 초기 설계는 전적으로 CTF에 기반했습니다.

1. **마켓 생성**: 운영자가 이벤트를 등록 → CTF 컨트랙트가 outcome 토큰 생성
2. **거래**: 사용자가 [[개념/CLOB]]에서 Yes/No 토큰 매매
3. **결과 확정 **(resolve): 오라클이 결과 보고 → 해당 outcome 토큰만 $1로 정산, 나머지는 $0
4. **청산**: 당첨 토큰을 Redeem하여 USDC 인출

Polymarket은 점차 [[개념/Negative-Risk]] 마켓으로 전환하고 있습니다. 2025년 기준 Neg-Risk가 $1.4B 이상의 거래량을 처리하며 CTF 마켓을 앞질렀습니다. Neg-Risk는 CTF의 Split/Merge를 직접 사용하지 않고, 독립적인 Yes/No 마켓을 여러 개 만든 후 어댑터 컨트랙트로 연결하는 방식입니다.

| 구분 | CTF | Neg-Risk |
|------|-----|----------|
| 토큰 | ERC-1155 조건부 토큰 | 독립 ERC-20 마켓 토큰 |
| 다중결과 | Split/Merge로 연결 | NegRiskAdapter로 통합 |
| 사용자 복잡도 | 높음 (토큰 조합 이해 필요) | 낮음 (그냥 여러 마켓 거래) |
| 가스비 | Split/Merge 트랜잭션 발생 | 오더 생성 시 플래그만 추가 |
| Copytrade 적합성 | 토큰 ID 추적 필요 | 단순 지갑 이벤트 팔로우 |

## Copytrade 관점에서의 CTF

[[개념/Copytrade]]에서 CTF의 토큰 구조를 이해하는 것이 중요한 이유는 다음과 같습니다:

1. **포지션 식별**: CTF 기반 마켓은 ERC-1155 토큰 ID로 포지션을 추적해야 합니다. 단순 Yes/No가 아니라 특정 collectionId + indexSet 조합을 해석해야 [[트레이더/리더보드/데이터]]에서 리더의 실제 포지션을 correctly 파악할 수 있습니다.

2. **Negative-Risk 헤징**: [[전략/Copytrade/리스크-헤징]]에서 CTF의 Merge 연산을 활용하면, 여러 마켓의 No 토큰을 모아 USDC로 환원하면서 손실을 고정할 수 있습니다.

3. **아비트리지**: CTF의 불변식(Yes₁ + … + Yesₙ = $1)이 시장에서 무너지면 차익 기회가 발생합니다. 시장 가격의 합이 $1 미만이면 All-Yes 바스켓 매수, $1 초과면 All-No 바스켓 매도로 확정 수익을 얻을 수 있습니다.

4. **슬리피지 관리**: CTF Split 후 개별 토큰을 시장에 매도할 때, 각 토큰의 [[개념/슬리피지]]가 누적됩니다. 여러 토큰을 순차적으로 처분하면 첫 번째 거래가 나머지 토큰 가격에 영향을 줄 수 있습니다.

## 온체인 확인: ERC-1155 토큰 ID 구조

CTF 토큰의 고유 ID는 다음과 같이 구성됩니다:

```
tokenId = keccak256(parentCollectionId, conditionId) × 2**128 | index
```

- `parentCollectionId`: 상위 마켓이 있다면 그 collection
- `conditionId`: 조건 자체의 고유 식별자 (오라클 + outcome count)
- `index`: outcome 인덱스 (0=All, 1=첫번째 결과, 2=두번째 결과, …)

Copytrade 봇을 만들 때는 이 토큰 ID를 해석해서 "어떤 마켓의 어떤 결과에 베팅했는지"를 복원해야 합니다. [[기술/온체인-컨트랙트]]에서 관련 컨트랙트 주소를 참조하세요.

## CTF vs Neg-Risk: Copytrade에 미치는 영향

Neg-Risk가 CTF를 대체하면서 Copytrade의 복잡도가 크게 줄었습니다:

- **CTF 시대**: ERC-1155 event 로그를 파싱 → 토큰 ID 디코딩 → 마켓 매핑 → 트레이더 포지션 추정
- **Neg-Risk 시대**: 일반 ERC-20 Transfer 이벤트 + 오더 북 기록으로 직관적 추적 가능

하지만 아직 CTF 기반 마켓이 존재하므로, 완전한 Copytrade 시스템을 구축하려면 두 구조 모두를 지원해야 합니다. [[전략/Copytrade/자동화-플로우]]에서 온체인 리스너 설계 시 이 점을 고려해야 합니다.

## 관련 문서

- [[개념/Negative-Risk]] — CTF를 대체한 Neg-Risk 구조, 실무적 헤징
- [[개념/CLOB]] — CTF 토큰의 실제 거래가 이루어지는 오더북
- [[개념/Copytrade]] — CTF 토큰 구조를 고려한 포지션 복제
- [[기술/온체인-컨트랙트]] — ERC-1155 토큰 ID 디코딩, 컨트랙트 주소
- [[전략/Copytrade/리스크-헤징]] — CTF Merge 연산을 활용한 손실 고정
- [[개념/슬리피지]] — 다중 토큰 처분 시 누적 슬리피지
