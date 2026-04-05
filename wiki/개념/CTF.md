---
title: "CTF (Conditional Token Framework)"
category: "concept"
created: "2026-04-04"
source: "derived from raw/01-Polymarket-개요.md, raw/07-온체인-컨트랙트.md"
related:
  - "[[개요]]"
  - "[[컨트랙트]]"
  - "[[CLOB]]"
  - "[[Negative-Risk]]"
---

# CTF (Conditional Token Framework)

> 예측 시장 결과를 토큰으로 변환하여 거래할 수 있게 해주는 핵심 프레임워크.

## 개요

CTF(Conditional Token Framework)는 Gnosis의 Condition Tokens 사양을 Polymarket에 적용한 것으로, 예측 시장의 각 결과를 **고유 ERC-1155 토큰**으로 표현합니다.

핵심 원리: `$1 USDC.e → Yes 토큰 + No 토큰 = $1 가치`

## 핵심 트랜잭션 3가지

### 1. Split (분할)

USDC.e를 특정 마켓의 Yes/No 토큰 쌍으로 분할합니다.

```
사용자: $1.00 USDC.e持有
  ↓ Split 트랜잭션 실행
결과: $1.00 Yes 토큰 + $1.00 No 토큰 (합 = $1.00)
```

#### Split 상세 절차

```
1. 사용자가 CTF 컨트랙트 호출
   splitCollateral(
     collateral: USDC.e 주소,
     conditionId: 마켓 condition ID,
     collateralAmount: 분할할 USDC.e 수량,
     outcomeSlotCount: 2 (Yes/No)
   )

2. 컨트랙트가 USDC.e를 ERC-20로 받고
   동일한 가치의 Yes 토큰 + No 토큰을 민팅

3. 사용자가 Yes/No 토큰 각각을 받음
```

#### 코드 예시 (ethers.js)

```javascript
const ctf = new ethers.Contract(CTF_ADDRESS, CTF_ABI, signer);

const collateral = "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174"; // USDC.e
const conditionId = "0x..."; // 마켓 condition ID
const amount = ethers.utils.parseUnits("100", 6); // $100 USDC.e

await ctf.splitCollateral(
  collateral,
  conditionId,
  amount,
  2  // Yes/No = 2 outcomes
);
```

### 2. Merge (결합)

Yes/No 토큰을 다시 USDC.e로 결합합니다. Split의 **역연산**.

```
사용자: $1.00 Yes 토큰 + $1.00 No 토큰持有
  ↓ Merge 트랜잭션 실행
결과: $1.00 USDC.e 회수 (둘 중 하나는 $0이 됨)
```

#### Merge 상세 절차

```
1. 사용자가 CTF 컨트랙트 호출
   mergePositions(
     collateral: USDC.e 주소,
     conditionId: 마켓 condition ID,
     collateralAmount: 결합할 토큰 수량
   )

2. 컨트랙트가 Yes 토큰 + No 토큰을 소각(burn)
   동일한 가치의 USDC.e를 민팅하여 반환
```

#### Merge가 유용한 경우
- **포지션 정리**: Yes/No를 동시에持有할 때 USDC.e로 전환
- **비용 절감**: 마켓 결과가 불투명할 때 토큰 대신 USDC.e 보유
- ** arbitrage**: 토큰 시장 가격이 USDC.e와 괴리 있을 때

### 3. Redeem (상환)

마켓 결과가 확정된 후, 승리 토큰을 USDC.e로 상환합니다.

```
마켓 결과: "Yes" 확정
사용자: $0.00 No 토큰 → 소각
사용자: $1.00 Yes 토큰 → $1.00 USDC.e로 상환
```

#### Redeem 상세 절차

```
1. UMA 오라클이 마켓 결과 확정
2. 컨트랙트가 결과 기록 (Winning Outcome 설정)
3. 사용자가 CTF 컨트랙트 호출
   redeemPositions(
     collateral: USDC.e 주소,
     conditionId: 마켓 condition ID,
     indexSets: 승리 outcome의 비트맵
   )
4. 승리 토큰 → USDC.e로 자동 전환
```

#### Redeem 예시

```javascript
// "Yes"가 승리한 경우, indexSets = 1 (비트맵)
// "No"가 승리한 경우, indexSets = 2

await ctf.redeemPositions(
  collateral,
  conditionId,
  1  // Yes 승리
);
```

## 토큰 구조 (ERC-1155)

CTF는 **ERC-1155** 멀티 토큰 표준을 사용합니다:

```
마켓 A (conditionId: 0x...001)
  ├── 토큰 ID 1: Yes 토큰 (collection ID 1)
  └── 토큰 ID 2: No 토큰 (collection ID 2)

마켓 B (conditionId: 0x...002)
  ├── 토큰 ID 1: Yes 토큰 (collection ID 1)
  └── 토큰 ID 2: No 토큰 (collection ID 2)
```

하나의 ERC-1155 컨트랙트로 **여러 마켓의 토큰**을 관리합니다.

## 포지션 생명주기

```
  $1.00 USDC.e
       ↓ [Split]
  $1.00 Yes + $1.00 No
       ↓ [거래소에서 매도]
  현금화 또는 포지션 정리
       ↓ [마켓 결과 확정]
  $1.00 USDC.e (Yes 승)
       ↓ [Redeem]
  $1.00 USDC.e 회수 완료
```

## Split/Merge/Redeem의 관계

| 트랜잭션 | 방향 | 비용 |
|----------|------|------|
| Split | USDC.e → Yes + No | 가스비 + 슬리피지 |
| Merge | Yes + No → USDC.e | 가스비 |
| Redeem | Winning 토큰 → USDC.e | 가스비 (무료인 경우 많음) |

## 마켓메이킹과의 관계

마켓메이커는 [[리베이트]] 참고:

- Split으로 유동성을 제공할 때 → Maker Rebate 수령
- 마켓 양쪽에 Split + Merge를 반복 → 무위험 수익 가능 (이론상)
- [[CLOB]]의 오더북 매칭과 결합

## Negative Risk에서의 CTF

[[Negative-Risk]] 참고:

- NegRisk 마켓에서는 3개 이상의 outcome 토큰 존재
- Split 시 → outcome 수만큼 토큰 생성
- NegRiskExchange가 다중 토큰 간 가격을 관리

## 온체인 컨트랙트 주소

| 네트워크 | CTF 컨트랙트 |
|----------|-------------|
| Polygon Mainnet (137) | 공식 문서에서 최신 확인 |
| Amoy Testnet (80002) | 테스트용 별도 주소 |

## 관련 문서

- [[개요]] — 플랫폼의 자본 효율적 거래 구조
- [[컨트랙트]] — 블록체인 수준에서의 토큰 작동 방식
- [[CLOB]] — 오더북 기반 가격 형성
- [[Negative-Risk]] — Negative Risk 마켓에서의 토큰 작동
