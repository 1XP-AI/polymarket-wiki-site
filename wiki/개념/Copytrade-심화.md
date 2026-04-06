---
title: "Copytrade 심화"
category: "concept"
created: "2026-04-05"
sources:
  - url: "raw/03-Copytrade-전략분석.md"
    raw: "raw/03-Copytrade-전략분석.md"
    added: "2026-04-05"
  - url: "https://github.com/agc-desarrollo/polymarket-trading-bot"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-06"
  - url: "https://coincodecap.com/top-10-tools-to-copy-trade-polymarket-traders"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-06"
  - url: "https://www.alphascope.app/blog/polymarket-copy-trading"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-06"
related:
  - "[[전략분석]]"
  - "[[데이터]]"
  - "[[CTF]]"
  - "[[레퍼런스]]"
---

# Copytrade 심화

> 상위 트레이더의 포지션을 자동으로 따라하는 전략의 심화 개념.

## Copytrade란?

다른 트레이더의 거래를 **실시간으로 감지하고 따라하는** 전략. Polymarket에서는 공개 API를 통해 누구의 포지션이든 조회 가능하므로, copytrade가 기술적으로 구현 가능하다.

## 핵심 데이터 소스

### 1. 리더보드 (Leaderboard)

```
GET https://data-api.polymarket.com/v1/leaderboard
파라미터: window=all|daily|weekly|monthly, limit, offset
```

- 수익률 기준 트레이더 순위
- 트레이더 지갑 주소 획득 가능
- 기간별 필터링 (전체/일간/주간/월간)

### 2. 트레이더 프로필

```
GET https://gamma-api.polymarket.com/public-profile?address={wallet}
```

- 프로필 정보, 거래 통계

### 3. 트레이더 포지션

```
GET https://data-api.polymarket.com/positions?address={wallet}
```

- 현재 보유 포지션 전체 조회
- 마켓별 토큰 수량, 방향 (Yes/No)

### 4. 트레이더 거래 내역

```
GET https://data-api.polymarket.com/trades?address={wallet}
```

- 과거 거래 기록
- 체결 가격, 수량, 시간, 방향

### 5. 실시간 감지 (WebSocket)

- Market Channel로 특정 마켓의 거래 실시간 수신
- 특정 트레이더의 거래를 필터링하려면 trades 폴링 또는 온체인 이벤트 구독

## Copytrade 파이프라인

```
1. 리더보드에서 상위 트레이더 선별
   ↓
2. 선별된 트레이더의 포지션/활동 모니터링
   ↓
3. 새로운 거래 감지
   ↓
4. 동일 마켓에 동일 방향으로 주문 생성
   ↓
5. 포지션 관리 (익절/손절/청산 따라하기)
```

## 트레이더 선별 기준

### 정량적 기준
- **총 수익률**: 누적 PnL
- **승률**: 수익 거래 / 전체 거래
- **샤프 비율**: 위험 대비 수익
- **MDD (Maximum Drawdown)**: 최대 손실폭
- **거래 빈도**: 너무 적으면 표본 부족, 너무 많으면 수수료 부담
- **거래 마켓 수**: 분산 투자 여부

### 정성적 기준
- **마켓 유형 선호도**: 정치? 스포츠? 크립토?
- **포지션 크기**: 대규모 자금 → 신뢰도 높을 수 있음
- **활동 기간**: 최근에만 활동 vs 장기 트랙 레코드

## 리스크 관리

### 주요 리스크
1. **시간 지연 (Latency)**: 감지 → 주문 사이 시간차로 불리한 가격에 진입
2. **유동성**: 카피 대상이 대규모 주문 → 슬리피지 발생
3. **전략 변경**: 트레이더가 갑자기 전략 변경
4. **수수료 침식**: 카피 트레이더는 대부분 Taker → 수수료 부담
5. **역선택**: 과거 성과 ≠ 미래 성과

### 대응 전략
- **다수 트레이더 분산 카피**: 1명에 올인하지 않음
- **포지션 크기 제한**: 카피 대상 대비 작은 비율로 진입
- **스톱로스**: 카피 대상이 청산하지 않더라도 자체 손절
- **성과 모니터링**: 일정 기간 성과 미달 시 자동 중단
- **딜레이 분석**: 진입 시점의 가격 vs 감지 시점 가격 비교

## 기술적 제약

1. **Polymarket에는 공식 Copytrade 기능이 없음** — 직접 구현 필요
2. **지오블로킹**: 미국 등 일부 지역에서 접근 제한
3. **Rate Limit**: API 호출 빈도 제한 있음
4. **온체인 지연**: 블록 확인 시간 존재
5. **Gasless 한계**: Relayer 방식이므로 트랜잭션 순서 보장 어려움

## 관련 문서

- [[전략분석]] — 전략 분석 문서
- [[데이터]] — 분석에 필요한 데이터 소스
- [[CTF]] — Negative Risk 마켓에서의 카피 전략
- [[레퍼런스]] — 구현을 위한 API 활용법
