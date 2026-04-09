---
id: legacy_wiki_api_polymarket_api_62ef40
title: Polymarket API 레퍼런스
type: concept
status: draft
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T14:10:09Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_api_polymarket_api_md_62ef406d
tags:
- concept
- internal
---

# Polymarket API 레퍼런스

## 요약

<!-- para: para_001 -->
> Gamma API, Data API, CLOB API의 핵심 엔드포인트 요약 + curl/Python 예제 및 운영 패턴

## 핵심 사실

<!-- para: para_002 -->
Polymarket의 주요 공개 엔드포인트(예: /events, /markets, /profiles)는 마켓 리스트, 이벤트 메타데이터, 사용자 프로필(공개된 경우)을 제공합니다. - **Gamma API**: 이벤트, 마켓, 프로필, 검색 등을 제공(공개)
- **Data API**: 포지션, 트레이드, 리더보드 등 상세 데이터
- **CLOB API**: 오더북, 주문, 체결 데이터(읽기: 공개)

간단한 호출 예:

```
GET https://gamma-api.polymarket.com/events?limit=20&active=true
```

<!-- para: para_003 -->
- GET /events?limit=20&active=true — 활성 이벤트 목록
- GET /markets?limit=50 — 마켓 목록(페이로드에 시장 상태 포함)
- GET /profiles/{address} — 공개 프로필(가능한 경우)

## 세부 내용

<!-- para: para_004 -->
```bash
curl -s "https://gamma-api.polymarket.com/events?limit=20&active=true" | jq '.'
```

<!-- para: para_005 -->
```bash
curl -s "https://gamma-api.polymarket.com/markets?limit=50" | jq '.results[] | {id: .id, name: .name, state: .state, price: .price}'
```

<!-- para: para_006 -->
```bash
curl -s "https://gamma-api.polymarket.com/profiles/0x1234..." | jq '.'
```

> 주의: 실제 주소나 프로필 엔드포인트는 공개 여부에 따라 응답이 제한될 수 있습니다.

<!-- para: para_007 -->
```json
{
  "id": "market_abc123",
  "name": "Will country X hold elections in 2026?",
  "state": "open",
  "price": 0.42,
  "liquidity": 12500
}
```

## 열린 질문

<!-- para: para_008 -->
GET https://gamma-api.polymarket.com/events?limit=20&active=true

<!-- para: para_009 -->
- GET /events?limit=20&active=true — 활성 이벤트 목록

<!-- para: para_010 -->
- GET /markets?limit=50 — 마켓 목록(페이로드에 시장 상태 포함)

## 관련 페이지

<!-- para: para_011 -->
소스 요약: source_summary_src_wiki_api_polymarket_api_md_62ef406d
