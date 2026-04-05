---
title: "Copytrade 전략분석"
category: "strategy"
created: "2026-04-05"
source: "raw/03-Copytrade-전략분석.md"
related:
  - "[[Polymarket-개요]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[CLOB]]"
  - "[[CTF]]"
  - "[[API-레퍼런스]]"
---

# Copytrade 전략분석

> 리더보드 상위 트레이더를 따라 거래(copytrade)할 때 고려할 전략과 리스크를 심화 정리합니다.

## 내용

이 문서는 리더보드 기반 copytrade 파이프라인의 기술적 구성, 구현 예시, 그리고 리스크 완화 방안을 구체적으로 다룹니다.

### 주요 데이터 소스 및 호출 예시

- 리더보드

```
GET https://data-api.polymarket.com/v1/leaderboard?window=weekly&limit=20
```

- 트레이더 프로필

```
GET https://gamma-api.polymarket.com/public-profile?address={WALLET}
```

- 트레이더 포지션

```
GET https://data-api.polymarket.com/positions?address={WALLET}
```

- 트레이더 거래 내역

```
GET https://data-api.polymarket.com/trades?address={WALLET}&limit=50
```

- 실시간 감지 (예: WebSocket 또는 폴링)
  - Market 채널로 체결/주문 이벤트 수신
  - 특정 지갑의 거래 탐지: 폴링으로 /trades 또는 /positions를 주기 조회

### 파이프라인(심화)

1. 리더보드 스냅샷(주기: 1h~24h) 수집 → 후보 트레이더 선정
2. 프로필·포지션 히스토리 수집(백필 및 최근 N건)
3. 실시간 모니터링: WebSocket + 폴링 병행
   - WebSocket으로 마켓 이벤트 수신
   - 트레이더별 변화는 /positions, /trades 폴링으로 보완
4. 거래 감지 시 신호 생성(TraderEvent)
5. 주문 생성 로직: 포지션 크기 계산 → 주문 유형 결정 (Limit/Market)
6. 포지션 관리: 익절/손절 룰, 타임아웃, 리밸런싱

### 주문 생성 예시 (curl)

- 포지션 조회(감지용):
```
curl -s "https://data-api.polymarket.com/positions?address=0xABCDEF..."
```

- 마켓 정보 조회:
```
curl -s "https://gamma-api.polymarket.com/markets?limit=10"
```

(주의: 인증이 필요한 엔드포인트는 사용하지 않음)

### 실전 고려사항

- Latency (지연): 감지→주문 사이의 시간차를 최소화하기 위해 WebSocket 우선, 로컬 캐시와 빠른 판단 로직 사용
- Slippage (슬리피지): 대상 트레이더의 주문 규모 대비 내 주문 규모를 제한하여 가격 충격 최소화
- Rate limits: API 호출량을 제어하고, 백오프(backoff) 정책 구현
- 전략 변경 탐지: 대상 트레이더의 스타일(마켓 선호, 포지션 크기)이 급변하면 자동으로 추종 중단

### 트레이더 선별(심화된 체크리스트)

정량적 지표
- 누적 PnL, 승률, 거래빈도, MDD, 샤프

정성적 지표
- 마켓 유형 선호(정치/크립토/스포츠), 공개 발언의 일관성, 소셜 신호

### 리스크 관리(구체화)

- 분산: 상위 5~10명에 분산하여 단일 트레이더 리스크 축소
- 포지션 사이징: 대상 포지션의 1~10% 수준으로 진입(계정 리스크에 비례)
- 스톱로스/타임아웃: 포지션별 최대 보유시간과 손실 한도를 설정
- 모니터링: 실시간 PnL, 거래 실패, API 장애 알람

### 실전 예시: 포지션 사이징 계산 (간단한 규칙)

다음 섹션에서는 포지션 사이징 규칙을 더 구체화하고, 슬리피지와 체결 확률을 고려한 보정 방법을 추가합니다.

#### 포지션 사이징: 단계별 규칙 (구체화)

1. 계정 리스크 산정
   - 계정 총자본(Account)과 허용 최대 손실 비율(R_max)을 정합니다. 예: Account = $100,000, R_max = 1% → MaxLoss = $1,000.
2. 트레이더 신뢰도 점수(C_trader)
   - 과거 90일 승률, 누적 PnL의 Z-스코어, 시장 적합성(선호 마켓 일치 여부), 소셜 신호의 일관성 등을 결합해 0..1로 정규화.
   - 가중치 예시: 승률(40%), 누적 PnL(30%), 시장 적합성(20%), 소셜(10%).
3. 초기 배분(B_base)
   - B_base = MaxLoss * allocation_factor
   - allocation_factor 예시: 0.2 (한 트레이더에 우선 할당하는 비율)
   - 예: MaxLoss $1,000 → B_base = $200
4. 유동성 제한(L_market)
   - 목표 마켓의 24h 거래량 또는 오더북 누적 깊이(예: 상위 10틱의 볼륨)로부터 체결 가능 최대 크기 산정.
   - 예: 상위 10틱 누적볼륨 = $10,000 → L_market = $10,000
5. 슬리피지 보정(S_slip)
   - 간단 모델: S_slip = min(0.05, estimated_price_impact)
   - estimated_price_impact는 분할 실행 시 예상 평균 가격 변화(%)
6. 최종 포지션 산출
   - raw_target = B_base * C_trader
   - liquidity_cap = L_market * liquidity_share (예: 0.05)
   - position_size = min(raw_target, liquidity_cap) * (1 - S_slip)

예시 계산 (수치적용)
- Account = $100,000, R_max=1% → MaxLoss=$1,000
- allocation_factor=0.2 → B_base=$200
- C_trader=0.8 → raw_target=$160
- L_market=$10,000, liquidity_share=0.05 → liquidity_cap=$500
- estimated_price_impact=0.01 → S_slip=0.01
→ position_size = min(160,500) * (1 - 0.01) = 160 * 0.99 = $158.4

#### 슬리피지·체결 확률 보정 (구체화)

- 체결 확률(P_fill): 지정가 주문의 과거 체결률을 기반으로 추정. 예: 최근 30일 지정가 체결률 0.6
- 체결 기대값(E_fill): E_fill = position_size * P_fill - (expected_fees + slippage_cost_estimate)
- 의사결정 룰:
  - E_fill > 0 이고 P_fill >= P_min(예: 0.3)일 때 진입
  - P_fill 낮으면 분할 주문 또는 시장가 사용으로 전환
- 분할 실행 계획:
  - 티어드(예: 4분할)로 시간/틱 간격을 두고 실행
  - 각 티어별 예상 P_fill, slippage 추정치를 사용해 동적 사이징

#### 주문 실행 안전장치

- Time-in-force 및 취소 규칙: 지정 시간이 지나면 자동 취소 또는 재평가
- 슬리피지 임계치: 실시간 예상 슬리피지가 임계값(예: 3%) 초과 시 주문 보류
- 전략 중단 조건: 트레이더 스타일 급변(최근 24시간 내 포지션 방향성 변경 2회 이상), API 장애, 급격한 마켓 변동성

#### 의사결정 예시 (pseudocode, 개선)

```
# inputs
account_balance = A
max_account_risk_pct = R_max
trader_confidence = C_trader
target_market_liquidity = L_market
allocation_factor = 0.2
liquidity_share = 0.05

MaxLoss = A * R_max
B_base = MaxLoss * allocation_factor
raw_target = B_base * C_trader
liquidity_cap = L_market * liquidity_share
estimated_price_impact = estimate_slippage(raw_target, orderbook)
S_slip = min(0.05, estimated_price_impact)
position_size = min(raw_target, liquidity_cap) * (1 - S_slip)

P_fill = estimate_fill_prob(position_size, historical_orders)
E_fill = position_size * P_fill - (expected_fees + slippage_cost(position_size))

if E_fill > 0 and P_fill >= 0.3:
    execute_tiered_orders(position_size)
else:
    skip_or_reduce_position()
```

#### 백테스트 및 시뮬레이션 (권장 사항)

- 시뮬레이션은 실제 주문 비용(수수료, 슬리피지), 네트워크/처리 지연을 반영해야 함
- 여러 트레이더를 동시 추종하는 경우 포트폴리오 레벨의 상관관계를 모델링하여 최대 드로다운을 산정
- 민감도 분석: C_trader, allocation_factor, liquidity_share 변화에 따른 PnL 분포 확인
- 테스트 데이터: 리더보드 이력, 오더북 스냅샷(가능한 경우), 트레이더 트레이드 히스토리

## 관련 문서 (업데이트)

- [[API-레퍼런스]] — 데이터 수집과 엔드포인트 예시
- [[CLOB]] — 주문장부 개념과 유동성/스프레드 영향
- [[CTF]] — 토큰화된 포지션 이해
- [[리더보드-트레이더-데이터]] — 트레이더 메트릭 템플릿

