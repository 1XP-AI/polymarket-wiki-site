---
id: legacy_wiki_copytrade_0c3a80
title: Copytrade 자동화 플로우
type: concept
status: draft
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-09T14:10:11Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_copytrade_md_0c3a8011
tags:
- concept
- internal
---

# Copytrade 자동화 플로우

## Summary

<!-- para: para_001 -->
> 리더보드 기반 copytrade의 자동화 설계와 모니터링 체크리스트

## Key Facts

<!-- para: para_002 -->
Copytrade 자동화는 크게 1) 트레이더 선별, 2) 포지션 동기화, 3) 리스크 제어, 4) 모니터링·알림의 네 단계로 구성된다.

<!-- para: para_003 -->
```
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│  Leaderboard     │    │  Polymarket CLOB │    │  On-chain Data    │
│  Snapshot Engine │───▶│  WebSocket Feed  │◀───│  (Polygonscan)    │
└────────┬────────┘    └────────┬─────────┘    └────────┬──────────┘
         │                      │                       │
         ▼                      ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│  Trader Screen  │    │  Signal Normalizer│    │  Position Tracker │
│  & Scoring      │───▶│  (Entry/Exit)     │───▶│  Reconciliation   │
└────────┬────────┘    └────────┬─────────┘    └────────┬──────────┘
         │                      │                       │
         ▼                      ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌───────────────────┐
│  Weight Engine  │    │  Order Executor   │    │  Risk Monitor     │
│  (Kelly/Equal)  │───▶│  (CLOB API)       │    │  & Alert System   │
└─────────────────┘    └──────────────────┘    └───────────────────┘
```

1) 트레이더 선별
- 리더보드 및 과거 성과로 후보군을 만들고, 승률· 평균 포지션 크기· 최대 드로우다운을 기준으로 필터링한다. (관련: [[전략/Copytrade/팔로우-선별]], [[전략/Copytrade/알고리즘-선별-체크리스트]])
- Polycopy 등 서드파티 리더보드(Polycopy: 500K+ 트레이더)를 교차 검증해 단일 플랫폼 편향을 피한다.

## Details

<!-- para: para_004 -->
2) 포지션 동기화
- 선택된 트레이더의 온체인/오프체인 포지션을 감지하여, 신호(진입/청산)를 표준화한 후 사용자 포트폴리오에 반영한다. WebSocket(체결 스트림)과 Data API(포지션 스냅샷)를 병행 사용한다. (관련: [[기술/API/Polymarket-API-레퍼런스]], [[기술/WebSocket-실시간데이터]])
- Neg-Risk 마켓(`negRisk: true`)은 CTF 마켓과 주문 구조가 다르므로 `NegRiskAdapter` 컨트랙트 경로로 별도 처리한다.

<!-- para: para_005 -->
```python
class CopytradePipeline:
    def __init__(self, config):
        self.clob_client = CLOBClient(config.api_key)     # py-clob-client
        self.ws = WebSocketFeed("wss://ws-api.polymarket.com")
        self.risk_monitor = RiskMonitor(max_drawdown=config.max_dd)
        self.circuit_breaker = CircuitBreaker(threshold=0.05)  # 5% daily loss

async def run(self):
        await self.ws.connect()
        self.ws.on("trade", self.handle_trade_signal)
        self.ws.on("error", self.handle_ws_error)

<!-- para: para_006 -->
while True:
            traders = await self.fetch_leaderboard_scores()
            weights = self.calculate_weights(traders)
            await self.rebalance_positions(weights)
            await asyncio.sleep(300)

async def handle_trade_signal(self, trade):
        if self.circuit_breaker.is_open():
            log.warn("Circuit breaker open — skipping signal")
            return

normalized = self.normalize_signal(trade)
        if not self.risk_monitor.check(normalized):
            log.warn(f"Risk check failed for {normalized.event_id}")
            return

await self.execute_order(normalized)

def calculate_weights(self, traders):

<!-- para: para_007 -->
if len(traders) == 0:
            return {}
        base = 1.0 / len(traders)
        return {t.wallet: base for t in traders}

if __name__ == "__main__":

## Open Questions

<!-- para: para_008 -->
Pending review.

## Related Pages

<!-- para: para_009 -->
Source summary: source_summary_src_wiki_copytrade_md_0c3a8011
