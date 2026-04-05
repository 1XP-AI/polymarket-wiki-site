---
title: "Polymarket API 레퍼런스 요약"
category: "infrastructure"
created: "2026-04-05"
source: "raw/02-API-레퍼런스.md"
related:
  - "[[Polymarket 개요]]"
  - "[[CLOB]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[Polymarket-이벤트-스냅샷-2026-04-05]]"
---

# Polymarket API 레퍼런스 요약

> Gamma API, Data API, CLOB API의 핵심 엔드포인트 요약

## 내용

- Gamma API: 이벤트, 마켓, 프로필, 검색 등을 제공(공개)
- Data API: 포지션, 트레이드, 리더보드 등 상세 데이터
- CLOB API: 오더북, 주문, 체결 데이터(읽기: 공개)

간단한 호출 예:

```
GET https://gamma-api.polymarket.com/events?limit=20&active=true
```

## 관련 문서

- [[Polymarket 개요]]

## 참조

[^1]: raw/02-API-레퍼런스.md
---
title: "API 레퍼런스"
category: "api"
created: "2026-04-05"
source: "raw/02-API-레퍼런스.md"
related:
  - "[[Polymarket 개요]]"
  - "[[WebSocket-실시간데이터]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[CLOB]]"
  - "[[Theo]]"
  - "[[Copytrade-리더보드-심화]]"
---

# API 레퍼런스

> Polymarket 공개 API와 실전 사용 예제(Deepen) — curl 예제, 응답 샘플, 간단한 jq 파싱 포함

## 내용

Polymarket의 주요 공개 엔드포인트(예: /events, /markets, /profiles)는 마켓 리스트, 이벤트 메타데이터, 사용자 프로필(공개된 경우)을 제공합니다. 아래 예제는 비인증(public) 엔드포인트를 사용한 기본 수집 흐름입니다.

### 주요 엔드포인트

- GET /events?limit=20&active=true — 활성 이벤트 목록
- GET /markets?limit=50 — 마켓 목록(페이로드에 시장 상태 포함)
- GET /profiles/{address} — 공개 프로필(가능한 경우)

### 간단한 curl 예제

1) 활성 이벤트 가져오기

curl -s "https://gamma-api.polymarket.com/events?limit=20&active=true" | jq '.'

2) 특정 마켓 가져오기

curl -s "https://gamma-api.polymarket.com/markets?limit=50" | jq '.results[] | {id: .id, name: .name, state: .state, price: .price}'

3) 리더보드에서 트레이더 프로필 조회(주소를 알 때)

curl -s "https://gamma-api.polymarket.com/profiles/0x1234..." | jq '.'

> 주의: 실제 주소나 프로필 엔드포인트는 공개 여부에 따라 응답이 제한될 수 있습니다.

### 예시 응답(JSON) 샘플

{
  "id": "market_abc123",
  "name": "Will country X hold elections in 2026?",
  "state": "open",
  "price": 0.42,
  "liquidity": 12500
}

### jq를 이용한 간단한 파이프라인

- 모든 오픈 마켓의 id와 현재 가격만 추출하여 CSV로 저장:

curl -s "https://gamma-api.polymarket.com/markets?limit=50" \
  | jq -r '.results[] | [.id, (.price|tostring)] | @csv' > markets.csv

- 특정 트레이더의 최근 포지션 요약(가정된 필드 사용):

curl -s "https://gamma-api.polymarket.com/profiles/0x1234.../positions" \
  | jq '.positions | map({market_id: .marketId, size: .size, side: .side})'

### 사용 팁

- Rate limit를 염두에 두고, 동일 엔드포인트를 짧은 간격으로 반복 호출하지 마십시오.
- 실시간 업데이트가 필요하면 WebSocket 피드와 조합하여 사용하고, 백필(backfill)은 REST API로 보강하세요.
- 인증이 필요한 엔드포인트는 키 없이 접근 불가하므로 raw 수집 단계에서 건너뛰도록 설계하세요.

## 관련 문서

- [[WebSocket-실시간데이터]] — 실시간 데이터 수집 방법
- [[온체인-컨트랙트]] — 온체인 연동이 필요한 경우
