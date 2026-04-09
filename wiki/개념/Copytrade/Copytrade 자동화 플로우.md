---
id: legacy_wiki_copytrade_0c3a80
title: Copytrade 자동화 플로우
type: concept
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-09T16:57:58Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_06_websocket_506430
- legacy_wiki_api_polymarket_api_62ef40
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://github.com/Fabianhvandijk/polymarket-copytrade
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
- url: https://github.com/agc-desarrollo/polymarket-trading-bot
  raw: raw/fetched/2026-04-06-copytrade-sources.md
- url: https://gamma-api.polymarket.com/events
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://docs.polymarket.com/api-reference/clients-sdks
  raw: raw/fetched/2026-04-07-negative-risk-and-api.md
- url: https://polycopy.app/discover
  raw: raw/fetched/2026-04-07-leaderboard-and-risk.md
---
# Copytrade 자동화 플로우

## 요약

<!-- para: para_001 -->
> 리더보드 기반 copytrade를 자동화할 때 필요한 선별, 동기화, 실행, 리스크 관리 단계를 정리한 문서

<!-- para: para_002 -->
Copytrade 자동화는 크게 1) 트레이더 선별, 2) 포지션/체결 동기화, 3) 주문 실행, 4) 리스크 모니터링 네 단계로 나눌 수 있다. 핵심은 "좋은 트레이더를 찾는 것"보다 "신호를 지연 없이 표준화하고, 잘못된 복제를 빨리 차단하는 것"에 있다.

<!-- para: para_003 -->
```text
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│ Leaderboard     │    │ Polymarket CLOB  │    │ On-chain Data     │
│ Snapshot Engine │───▶│ WebSocket Feed   │◀───│ (Polygonscan)     │
└────────┬────────┘    └────────┬─────────┘    └────────┬──────────┘
         │                      │                       │
```

▼                      ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│ Trader Screen   │    │ Signal           │    │ Position Tracker  │
│ & Scoring       │───▶│ Normalizer       │───▶│ Reconciliation    │
└────────┬────────┘    └────────┬─────────┘    └────────┬──────────┘
         │                      │                       │
         ▼                      ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│ Weight Engine   │    │ Order Executor   │    │ Risk Monitor      │
│ (Kelly/Equal)   │───▶│ (CLOB API)       │    │ & Alert System    │
└─────────────────┘    └──────────────────┘    └───────────────────┘

<!-- para: para_004 -->
트레이더 선별 단계에서는 리더보드 수익률만 보지 말고 승률, 최대 드로우다운, 평균 보유 시간, 거래 빈도, 특정 이벤트군 편중 여부를 함께 봐야 한다. 리더보드 정보는 [[Copytrade 데이터 수집 가이드]]와 연결해서 해석하는 편이 낫다.

<!-- para: para_005 -->
```python
class CopytradePipeline:
    def __init__(self, config):
        self.clob_client = CLOBClient(config.api_key)
        self.ws = WebSocketFeed("wss://ws-api.polymarket.com")
        self.risk_monitor = RiskMonitor(max_drawdown=config.max_dd)
        self.circuit_breaker = CircuitBreaker(threshold=0.05)

    async def run(self):
        await self.ws.connect()
        self.ws.on("trade", self.handle_trade_signal)
        self.ws.on("error", self.handle_ws_error)

        while True:
            traders = await self.fetch_leaderboard_scores()
            weights = self.calculate_weights(traders)
            await self.rebalance_positions(weights)
            await asyncio.sleep(300)

    async def handle_trade_signal(self, trade):
        if self.circuit_breaker.is_open():
            log.warn("Circuit breaker open; skipping signal")
            return

        normalized = self.normalize_signal(trade)
        if not self.risk_monitor.check(normalized):
            log.warn(f"Risk check failed for {normalized.event_id}")
            return

        await self.execute_order(normalized)

    def calculate_weights(self, traders):
        if len(traders) == 0:
            return {}
        base = 1.0 / len(traders)
        return {t.wallet: base for t in traders}
```

<!-- para: para_006 -->
실제 구현에서는 WebSocket만으로 충분하지 않다. 체결 스트림이 끊길 수 있으므로 주기적 포지션 스냅샷과 온체인 데이터로 재조정해야 하며, Neg-Risk 마켓은 일반 CTF 마켓과 다른 경로로 처리할 가능성을 열어 둬야 한다.

<!-- para: para_007 -->
운영 체크리스트는 단순하다. 손실 한도 초과 시 복제 중단, API 오류 누적 시 안전 정지, 대상 트레이더의 전략 붕괴 감지 시 제외, 슬리피지 급증 구간 회피, 그리고 사람이 검토할 수 있는 알림/로그를 남기는 구조를 먼저 갖춰야 한다.
