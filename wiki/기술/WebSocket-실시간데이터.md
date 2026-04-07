---
title: "WebSocket 실시간데이터"
category: "기술"
created: "2026-04-05"
sources:
  - url: "https://gamma-api.polymarket.com/events?limit=20&active=true"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://docs.polymarket.com"
    raw: "raw/06-WebSocket-실시간데이터.md"
    added: "2026-04-07"
  - url: "https://docs.polymarket.com/websocket"
    raw: "raw/fetched/2026-04-07-websocket-details.md"
    added: "2026-04-07"
related:
  - "[[기술/API/Polymarket-API-레퍼런스]]"
  - "[[개념/Polymarket]]"
  - "[[데이터/Polymarket-GitHub-리포트]]"
  - "[[전략/Copytrade/추종-실행-속도-최적화]]"
  - "[[전략/Copytrade/자동화-플로우]]"
  - "[[데이터/수집-파이프라인]]"
---

# WebSocket 실시간데이터

> 한 줄 요약: Market/User/Sports/RTDS 채널을 통한 실시간 오더북·트레이드 스트림 사용법, 재접속 전략, Copytrade 지연 최소화 패턴.

## 채널 개요

Polymarket은 4가지 WebSocket 채널을 제공하며, 용도와 인증 요구사항이 다르다.

| 채널 | 인증 | 용도 |
|------|------|------|
| Market | 불필요 | 공개 오더북·가격·거래 실시간 스트림 |
| User | L2 Auth 필요 | 개인 주문/체결/포지션 이벤트 |
| Sports | 불필요 | 스포츠 경기 스코어·상태 업데이트 |
| RTDS | 불필요 | 외부 데이터(크립토 시세, 주가, 코멘트) |

### Market Channel (Public)

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

### User Channel (Authenticated)

L2 서명(L2 Auth)이 필요하다. 개인 이벤트만 수신:

- 주문 생성/매칭/체결/취소 상태 변경
- 포지션 증감 실시간 반영
- Copytrade에서 **내 포지션이 원본 트레이더와 얼마나 동기화되어 있는지** 실시간 확인 가능

### Sports Channel & RTDS

Sports Channel은 스포츠 경기의 실시간 스코어 업데이트를 전송한다. RTDS(Real-Time Data Socket)는 외부 데이터(코인 시세, 주가, 뉴스 코멘트)를 스트리밍 — 예측 마켓 가격과 외부 이벤트 간 **상관관계 분석**에 활용.

## Copytrade에서의 실시간 신호 감지

### 방법 1: Market Channel 구독 + 주소 필터링

- 관심 마켓 전체를 WebSocket 구독
- 모든 거래 이벤트 수신 후 특정 트레이더 주소로 필터링
- **장점**: 실시간성 최고
- **단점**: 거래 이벤트에 트레이더 주소가 항상 포함되지 않음

### 방법 2: REST API 폴링

- `/trades?address={wallet}` 을 주기적 호출
- 새 거래 감지 시 카피 실행
- **장점**: 트레이더별 거래 내역 정확
- **단점**: 폴링 간격만큼 지연 발생(보통 1~5초)

### 방법 3: 온체인 이벤트 구독 (Polygon RPC)

- Polygon 네트워크에서 CTF 컨트랙트 이벤트 구독
- **장점**: 가장 빠르고 주소 투명
- **단점**: 구현 복잡도 높음, Polygon 노드 운영 필요

### 권장 조합

```
Market Channel (실시간 마켓 감시)
    + REST API 폴링 (특정 트레이더 거래 확인, 3초 간격)
    + 온체인 이벤트 (대규모 거래 즉시 감지)
```

이 조합은 [[전략/Copytrade/추종-실행-속도-최적화]]에서 다루는 지연 최소화 전략의 핵심이다.

## 재접속(Reconnection) 전략

WebSocket은 불안정하므로 재접속 로직이 필수:

1. **Exponential backoff**: 1초 → 2초 → 4초 → 8초 → 최대 30초
2. **구독 복원**: 재접속 후 모든 마켓 ID 재구독 필요
3. **스냅샷 동기화**: 재접속 시 REST API로 오더북 스냅샷 조회 후 WebSocket 증분 업데이트와 병합
4. **하트비트**: Polymarket WS는 ping/pong으로 생존 확인 — 30초 내 응답 없으면 강제 재접속

## 지연(Latency) 최적화

Copytrade에서 WebSocket 레이턴시는 직접적인 수익 손실로 연결:

- **로케이션**: Polymarket 서버와 물리적 거리가 가까운 리전(AWS us-east-1 등)에서 실행
- **비동기 처리**: WebSocket 메시지 파싱과 주문 제출을 별도 스레드로 분리
- **프리펫치**: CLOB 오더북을 로컬에서 유지하고, WebSocket 이벤트로 즉시 업데이트
- [[개념/슬리피지]] — 지연이 클수록 슬리피지 비용 증가

## 관련 문서

- [[기술/API/Polymarket-API-레퍼런스]] — REST API 엔드포인트 전체
- [[전략/Copytrade/추종-실행-속도-최적화]] — WebSocket 기반 지연 최소화
- [[전략/Copytrade/자동화-플로우]] — WebSocket을 활용한 포지션 동기화
- [[개념/슬리피지]] — 레이턴시와 슬리피지의 관계
- [[기술/온체인-컨트랙트]] — Polygon 온체인 이벤트 구독
