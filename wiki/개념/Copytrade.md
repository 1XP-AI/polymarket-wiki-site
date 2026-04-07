---
title: "Copytrade"
category: "개념"
created: "2026-04-05"
sources:
  - url: "https://www.polymarket.com"
    raw: "raw/fetched/2026-04-05-polymarket-home.md"
    added: "2026-04-05"
  - url: "https://polymarket.gitbook.io"
    raw: "raw/fetched/2026-04-05-polymarket-gitbook.md"
    added: "2026-04-05"
  - url: "https://gamma-api.polymarket.com/events"
    raw: "raw/fetched/2026-04-05-polymarket-events.md"
    added: "2026-04-05"
  - url: "https://polymarketanalytics.com/traders"
    raw: "raw/fetched/2026-04-05-polymarket-analytics.md"
    added: "2026-04-05"
  - url: "https://docs.polymarket.com/api"
    raw: "raw/fetched/2026-04-06-polymarket-docs-api.md"
    added: "2026-04-06"
  - url: "https://data.polymarket.com/leaderboard"
    raw: "raw/fetched/2026-04-06-polymarket-data-leaderboard.md"
    added: "2026-04-06"
  - url: "https://polymarket.com/blog"
    raw: "raw/fetched/2026-04-06-polymarket-blog.md"
    added: "2026-04-06"
  - url: "https://predicting.top/"
    raw: "raw/fetched/2026-04-05-market-trends.md"
    added: "2026-04-06"
  - url: "https://gamma-api.polymarket.com/markets?limit=100"
    raw: "raw/fetched/2026-04-06-polymarket-markets-100.md"
    added: "2026-04-06"
  - url: "https://polymarket.com/help"
    raw: "raw/fetched/2026-04-06-polymarket-help.md"
    added: "2026-04-06"
  - url: "https://polymarket.com/leaderboard?period=monthly"
    raw: "raw/fetched/2026-04-06-leaderboard-monthly-2.md"
    added: "2026-04-06"
  - url: "https://data.polymarket.com"
    raw: "raw/fetched/2026-04-06-polymarket-data.md"
    added: "2026-04-06"
  - url: "https://github.com/polymarket"
    raw: "raw/fetched/2026-04-06-github-polymarket.md"
    added: "2026-04-06"
  - url: "https://reddit.com/r/polymarket"
    raw: "raw/fetched/2026-04-05-reddit-polymarket.md"
    added: "2026-04-06"
  - url: "https://gamma-api.polymarket.com/leaderboard"
    raw: "raw/fetched/2026-04-06-polymarket-leaderboard-api.md"
    added: "2026-04-06"
  - url: "https://data-api.polymarket.com/v1/leaderboard"
    raw: "raw/fetched/2026-04-06-data-api-leaderboard.md"
    added: "2026-04-06"
  - url: "https://polymarket.com/faq"
    raw: "raw/fetched/2026-04-06-polymarket-faq.md"
    added: "2026-04-06"
  - url: "https://polymarket.statuspage.io"
    raw: "raw/fetched/2026-04-06-polymarket-status.md"
    added: "2026-04-06"
  - url: "https://twitter.com/Polymarket"
    raw: "raw/fetched/2026-04-06-polymarket-twitter.md"
    added: "2026-04-06"
  - url: "https://polymarket.medium.com"
    raw: "raw/fetched/2026-04-06-polymarket-medium.md"
    added: "2026-04-06"
  - url: "https://investopedia.com/terms/c/copy-trading.asp"
    raw: "raw/fetched/2026-04-06-investopedia-copy-trading.md"
    added: "2026-04-06"
  - url: "https://www.etoro.com/en/copytrading/"
    raw: "raw/fetched/2026-04-06-etoro-copytrading.md"
    added: "2026-04-06"
  - url: "https://www.binance.com/en/support/faq/360047025592"
    raw: "raw/fetched/2026-04-06-binance-copytrading.md"
    added: "2026-04-06"
  - url: "https://www.quantstart.com/articles/market-impact-slippage/"
    raw: "raw/fetched/2026-04-06-quantstart-slippage.md"
    added: "2026-04-06"
  - url: "https://www.investopedia.com/terms/s/slippage.asp"
    raw: "raw/fetched/2026-04-06-investopedia-slippage.md"
    added: "2026-04-06"
related:
  - "[[리더보드-트레이더-데이터]]"
  - "[[Copytrade-전략분석]]"
  - "[[API-레퍼런스]]"
  - "[[Theo]]"
  - "[[Polymarket 개요]]"
  - "[[리스크-관리-심화]]"
  - "[[Copytrade-리더보드-심화]]"
---

# Copytrade

> 리더보드 트레이더를 따라 거래하는 전략 설명 (심화)

## 요약

Copytrade는 리더보드 상의 검증된 트레이더를 추종해 그들의 포지션 변화를 자동으로 복제하는 전략이다. 이 문서는 기존 개요를 확장하여: 계량적 평가 지표, 백테스트 설계, 실행·슬리피지 고려, 운영 모니터링 체크리스트 및 구현 템플릿을 제시한다. 또한 운영 사례와 구체적 사이징 예시를 추가해 실전 사용에 바로 적용할 수 있도록 구성했다.

## 핵심 개념(요약)

- 목표: 숙련 트레이더의 의사결정에서 발생하는 [[copytrade|알파(정보 우위)]]를 재현하되, 복제에 따른 비용·[[리스크|리스크]]를 계량적으로 통제한다.
- 접근법: 트레이더 행동을 이벤트(포지션 진입/청산)로 감지 → 필터링(유의미성·중복노출·유동성) → 사이징 규칙 적용 → 실행 → 모니터링으로 루프 완성.

## 계량적 선택·평가 지표

1. 일관성 지표
   - 최근 N일(예: 30/60/90) 누적수익률과 표준편차
   - 연속 베팅 시 승률(Win Streak / Loss Streak) 분포
2. 샘플 크기 및 신뢰성
   - 트레이더가 같은 타입(마켓)에서 수행한 거래 수
   - 거래당 평균 노출기간
3. 알파 신호 강도
   - 트레이더의 평균 정보계수(IC): 트레이더 신호와 이후 수익 간의 상관계수
   - 샤프/Sortino 비율 (수익의 리스크조정 성과)
4. 유동성·임박성·정책 리스크
   - 시장별 평균 호가 스프레드·잔존유동성(상위 N 오더) 측정
   - 이벤트 마감까지 남은 시간(임박성)으로 가중치 조정
5. 중복노출(클러스터링)
   - 동일 주제/이벤트(예: 동일 예측 질문)에 여러 팔로우로 인한 [[리더보드-트레이더-데이터|포지션 집중도]]

## 백테스트 설계 (권장)

- 데이터 필요
  - 리더보드 스냅샷(시간별), 마켓 상태(당시 가격·유동성), 체결/청산 로그
  - raw/fetched 에 저장된 스냅샷 파일을 사용
- 시뮬레이션 구성
  1) 이벤트 재현: 트레이더 A의 포지션 변경을 시점 t로 고정
  2) 실행 모델: 실제 마켓 유동성·수수료·슬리피지 모델 반영
  3) 사이징: 비율 기반(계정자본 대비) 또는 목표 델타 기반
  4) 평가: 거래비용을 뺀 순수 알파, 누적수익 곡선, 최대 낙폭(MDD), 회복기간
- 민감도 분석
  - 슬리피지, 수수료, 추종 지연(latency)을 ±범위로 변동시켜 민감도 표 작성

## 실행(운영) 고려사항

- 레이턴시 최적화
  - 리더보드 이벤트 탐지 → 신속히 주문 제출까지의 경로 최적화
  - [[API-예제-샘플|WebSocket 실시간 데이터]]와 폴링의 하이브리드 사용
- 주문 유형
  - [[개념-CLOB|시장가 주문]]은 빠르지만 [[슬리피지|슬리피지]] 위험 증가
  - 제한가+IOC/FOC 혼합으로 제출 후 미체결 시 대체 전략
- 실패 모드
  - 주문 거부, 부분 체결, 마켓 상태 급변에 따른 자동 재평가

## 추종 규칙 예시(의사코드)

- Detect: 트레이더 A가 market X에 "Yes" 노출을 신규로 구축했을 때
  1) if liquidity(X) < threshold -> skip
  2) compute exposure = min(max_size, account_capital * target_pct)
  3) check duplicate_exposure(cluster_key) -> if > limit then reduce/skip
  4) submit order with price_control (limit or pegged)
  5) on partial_fill -> attempt completion up to slippage_limit

## 운영 사례 및 사이징 예시

- 사례 A: 소형 마켓(유동성 낮음)에서의 안전한 접근
  - 전제: 계정자본 10,000 USD, 목표 카피비율 target_pct = 0.5% → target_trade_size = 50 USD
  - 시장 유동성 검사: 상위 오더의 잔존 유동성이 200 USD일 때, 단일 진입으로 시장 영향이 크므로 분할 진입(예: 5회, 10 USD씩) 권장
  - 비용 예시: 예상 슬리피지 0.5% + 수수료 0.2% → 총 거래비용 약 0.7% 적용

- 사례 B: 임박성 높고 유동성 양호한 대형 마켓
  - 같은 계정자본 기준 target_pct를 2%로 상향 적용 가능, 단 거래 전 리스크 알림과 상한(예: max_size)을 확인

- 사이징 계산(간단)
  - account_capital * target_pct = raw_size
  - adjusted_size = min(raw_size, max_size, liquidity_limit)
  - 분할 횟수 = ceil(adjusted_size / intended_slice_size)

- 운영 팁
  - 슬리피지·부분체결 이력에 따라 트레이더별 가중치 보정
  - 동일 이벤트에 대한 다중 팔로우는 클러스터링 키로 집계하여 포지션 상한 적용

## 모니터링 & 알림

- 성능 알림
  - 1일/7일 급격한 성과 저하 → 자동 팔로우 중지 플래그
- [[전략/Copytrade/리스크-관리|리스크 알림]]
  - 누적 손실(계정 %) 초과 시 휴지 상태로 전환
- 무결성 검사
  - [[리더보드-트레이더-데이터|리더보드 데이터]]와 실행 로그의 타임스탬프 불일치 감지

## 구현 체크리스트

- [ ] 리더보드 스냅샷 파이프라인 연결 (raw/fetched)
- [ ] 평가 지표(30/60/90) 계산 모듈
- [ ] 백테스트 모듈(슬리피지·지연 파라미터 포함)
- [ ] 실행 엔진(주문 타입 대응, 부분 체결 핸들링)
- [ ] 모니터링 대시보드 및 알림 룰

## 추가 심화: 데이터 예시, 백테스트 파라미터 샘플, 구현 템플릿

### 데이터 예시
- 리더보드 스냅샷(예):
  - {timestamp: "2026-03-01T12:00:00Z", trader_id: "0xabc...", market_id: "mkt123", side: "Yes", size: 75.0, price: 0.62}
- 마켓 유동성 스냅샷(예):
  - {timestamp: "2026-03-01T12:00:00Z", market_id: "mkt123", best_bid: 0.615, best_ask: 0.625, top_n_liquidity: 500.0}

이런 스냅샷들을 시간순으로 정렬해 이벤트 기반 시뮬레이션을 수행한다.

### 백테스트 파라미터 샘플
- latency_ms: [0, 100, 500]
- slippage_pct: [0.0, 0.2, 0.5, 1.0]
- fee_pct: [0.1, 0.2, 0.3]
- slice_size_usd: [10, 25, 50]

각 조합에 대해 누적수익·MDD·회복기간을 기록해 민감도 표를 만든다.

### 구현 템플릿 (Python 의사코드)

```python
# event-driven follow logic (pseudo)
for event in leaderboard_events:
    if not passes_filters(event):
        continue
    target = compute_size(account_capital, event, params)
    slices = split_into_slices(target, params['slice_size_usd'])
    for s in slices:
        res = submit_order(market_id=event.market_id, side=event.side, size=s)
        handle_partial_fill(res)
    record_execution(event, res)
```

> 실제 구현에서는 주문 재시도, 가격 보호(price guard), 재진입 제한(reentry cooldown) 등을 반드시 포함해야 한다.

### 운영 지표 및 권장 임계값 (예시)
- 즉시 중지(Stop-follow) 조건:
  - 연속 손실 5회 또는 7일 누적 손실 > 5% 계정
  - 트레이더의 최근 30일 거래수 < 10 (신뢰도 부족)
- 경고(Warning) 조건:
  - 부분체결 비율 > 30% (시장 충격 또는 유동성 부족)
  - 평균 슬리피지 > 0.5% (실행 정책 재검토 필요)

## 참고(간단한 참조 예시)

- 구현 예시는 [[API-레퍼런스]], [[실시간데이터(WebSocket)]], 및 데이터 파이프라인 문서를 참고해라.

## 관련 문서

- [[Copytrade-전략분석]] — 심화 가이드
- [[리더보드-트레이더-데이터]] — 데이터 원본 및 리더보드 분석
- [[API-레퍼런스]] — 실시간 마켓 조회 및 포지션 데이터
- [[리스크-관리-심화]] — 위험관리 상세
- [[Copytrade-리더보드-심화]] — 리더보드 전용 분석
