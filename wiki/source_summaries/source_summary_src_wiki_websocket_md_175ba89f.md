---
id: source_summary_src_wiki_websocket_md_175ba89f
title: 'Source Summary: WebSocket 실시간데이터'
type: source_summary
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T14:10:09Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: high
related_pages:
- legacy_wiki_websocket_175ba8
tags:
- internal
- internal
---

# Source Summary: WebSocket 실시간데이터

## Summary

<!-- para: para_001 -->
> 한 줄 요약: Market/User/Sports/RTDS 채널을 통한 실시간 오더북·트레이드 스트림 사용법, 재접속 전략, Copytrade 지연 최소화 패턴.

## Key Facts

<!-- para: para_002 -->
Polymarket은 4가지 WebSocket 채널을 제공하며, 용도와 인증 요구사항이 다르다. | 채널 | 인증 | 용도 |
|------|------|------|
| Market | 불필요 | 공개 오더북·가격·거래 실시간 스트림 |
| User | L2 Auth 필요 | 개인 주문/체결/포지션 이벤트 |
| Sports | 불필요 | 스포츠 경기 스코어·상태 업데이트 |
| RTDS | 불필요 | 외부 데이터(크립토 시세, 주가, 코멘트) |

<!-- para: para_003 -->
관심 마켓의 토큰 ID를 지정하여 구독. 수신 이벤트:

- **order_book**: bid/ask 가격과 수량 변경
- **trade**: 체결 내역(가격, 수량, 방향)
- **market_update**: 마켓 상태 변경(일시정지, 결과 확정 등)

```python
import websocket, json

ws = websocket.WebSocketApp("wss://ws.polymarket.com",
    on_message=lambda ws, msg: handle(json.loads(msg)))

def handle(data):
    event = data.get("type")
    if event == "trade":
        price = data.get("price")
        size = data.get("size")
        if price and 0 < price < 1:
            print(f"[체결] {price:.3f} × {size}")

ws.run_forever()
```

## Details

<!-- para: para_004 -->
L2 서명(L2 Auth)이 필요하다. 개인 이벤트만 수신:

- 주문 생성/매칭/체결/취소 상태 변경
- 포지션 증감 실시간 반영
- Copytrade에서 **내 포지션이 원본 트레이더와 얼마나 동기화되어 있는지** 실시간 확인 가능

<!-- para: para_005 -->
Sports Channel은 스포츠 경기의 실시간 스코어 업데이트를 전송한다. RTDS(Real-Time Data Socket)는 외부 데이터(코인 시세, 주가, 뉴스 코멘트)를 스트리밍 — 예측 마켓 가격과 외부 이벤트 간 **상관관계 분석**에 활용.

<!-- para: para_006 -->
- 관심 마켓 전체를 WebSocket 구독
- 모든 거래 이벤트 수신 후 특정 트레이더 주소로 필터링
- **장점**: 실시간성 최고
- **단점**: 거래 이벤트에 트레이더 주소가 항상 포함되지 않음

<!-- para: para_007 -->
- `/trades?address={wallet}` 을 주기적 호출
- 새 거래 감지 시 카피 실행
- **장점**: 트레이더별 거래 내역 정확
- **단점**: 폴링 간격만큼 지연 발생(보통 1~5초)

## Open Questions

<!-- para: para_008 -->
- `/trades?address={wallet}` 을 주기적 호출
