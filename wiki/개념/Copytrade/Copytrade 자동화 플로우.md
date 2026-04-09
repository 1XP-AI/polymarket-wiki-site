---
id: legacy_wiki_copytrade_0c3a80
title: Copytrade 자동화 플로우
type: concept
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-10T03:07:00Z'
as_of: '2026-04-10'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_00_index_ec3366
- legacy_raw_06_websocket_506430
- legacy_wiki_4526f6
- legacy_wiki_api_polymarket_api_62ef40
- legacy_wiki_copytrade_1f98b0
- legacy_wiki_copytrade_c6dea0
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_e2e01c
- legacy_wiki_copytrade_e81931
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
> 리더보드 기반 Copytrade를 자동화할 때 필요한 선별, 동기화, 실행, 리스크 관리 단계를 정리한 문서.

<!-- para: para_002 -->
Copytrade 자동화는 크게 1) 트레이더 선별, 2) 포지션·체결 동기화, 3) 주문 실행, 4) 리스크 모니터링 네 단계로 나눌 수 있다. 핵심은 "좋은 트레이더를 찾는 것"보다 "신호를 지연 없이 표준화하고, 잘못된 복제를 빠르게 차단하는 것"에 있다.

## 아키텍처 개요

<!-- para: para_003 -->
```text
┌─────────────────┐    ┌────────────────────┐    ┌───────────────────┐
│ Leaderboard     │    │ Polymarket CLOB    │    │ On-chain Data     │
│ Snapshot Engine │───▶│ / WebSocket Feed   │◀───│ / Wallet Events   │
└────────┬────────┘    └─────────┬──────────┘    └────────┬──────────┘
         │                       │                        │
         ▼                       ▼                        ▼
┌─────────────────┐    ┌────────────────────┐    ┌───────────────────┐
│ Trader Screen   │    │ Signal Normalizer  │    │ Position Tracker  │
│ & Scoring       │───▶│ (Entry / Exit)     │───▶│ Reconciliation    │
└────────┬────────┘    └─────────┬──────────┘    └────────┬──────────┘
         │                       │                        │
         ▼                       ▼                        ▼
┌─────────────────┐    ┌────────────────────┐    ┌───────────────────┐
│ Weight Engine   │    │ Order Executor     │    │ Risk Monitor      │
│ (Equal / Kelly) │───▶│ (CLOB API)         │    │ & Alert System    │
└─────────────────┘    └────────────────────┘    └───────────────────┘
```

<!-- para: para_004 -->
리더보드와 외부 프로필 데이터를 먼저 스크리닝 엔진에 넣고, 이후 WebSocket 및 CLOB/포지션 데이터를 합쳐 신호를 정규화한다. 실행 엔진은 주문만 담당하고, 별도 리스크 모니터가 서킷 브레이커와 알림을 처리하도록 분리하는 편이 운영상 안전하다.

## 운영 단계

<!-- para: para_005 -->
트레이더 선별 단계에서는 단순 수익률보다 승률, 최대 드로우다운, 평균 보유 시간, 거래 빈도, 특정 이벤트군 편중 여부를 함께 봐야 한다. 리더보드 상위권이라도 특정 시즌성 마켓에만 강한 계정은 자동 복제 대상으로 부적합할 수 있다. `[[팔로우 선별]]`과 `[[리더보드 데이터]]`가 이 단계의 기준 문서다.

<!-- para: para_006 -->
포지션 동기화 단계에서는 WebSocket 체결 스트림과 주기적 포지션 스냅샷을 함께 써야 한다. 스트림만 믿으면 연결 단절이나 누락 이벤트 때문에 복제 포지션이 어긋날 수 있으므로 `[[WebSocket & 실시간 데이터]]`와 `[[Polymarket API 레퍼런스]]`를 같이 보는 편이 안정적이다.

<!-- para: para_007 -->
주문 실행 단계에서는 리더의 주문을 그대로 복사하는 것보다, 내 계정 한도와 슬리피지 한도를 적용한 뒤 축소된 신호를 실행하는 편이 낫다. Neg-Risk 마켓과 유동성이 얕은 마켓은 일반 CLOB 마켓과 다른 보호 규칙을 두는 것이 안전하다.

<!-- para: para_008 -->
모니터링 계층은 손실 한도 초과 시 복제 중단, API 오류 누적 시 안전 정지, 대상 트레이더의 전략 붕괴 감지 시 제외, 슬리피지 급증 구간 회피, 사람이 검토할 수 있는 알림과 로그를 포함해야 한다. 운영 관점에서는 `[[Copytrade 성능 모니터링]]`과 `[[리스크 모니터링(Copytrade)]]`이 핵심이다.

## 실무 포인트

<!-- para: para_009 -->
```python
class CopytradePipeline:
    def __init__(self, config):
        self.clob_client = CLOBClient(config.api_key)
        self.ws = WebSocketFeed("wss://ws-api.polymarket.com")
        self.risk_monitor = RiskMonitor(max_drawdown=config.max_dd)

    async def run(self):
        await self.ws.connect()
        self.ws.on("trade", self.handle_trade_signal)
        while True:
            traders = await self.fetch_leaderboard_scores()
            weights = self.calculate_weights(traders)
            await self.rebalance_positions(weights)
            await asyncio.sleep(300)
```

<!-- para: para_010 -->
Copytrade 자동화의 성패는 체결 속도보다 예외 처리에서 갈린다. 리더보드가 좋아 보여도 급격한 노출 확대, 장중 유동성 붕괴, 시장 상태 전환, API 장애가 겹치면 복제 계정의 손실이 훨씬 커질 수 있다. 따라서 자동화 플로우에는 사람 검토용 로그, 서킷 브레이커, 재동기화 절차가 반드시 포함돼야 한다.
