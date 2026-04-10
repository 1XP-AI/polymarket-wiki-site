---
id: legacy_wiki_api_polymarket_api_62ef40
title: Polymarket API 레퍼런스
type: concept
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-10T16:31:53Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 3
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_00_index_ec3366
- legacy_wiki_clob_064e27
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_698574
- legacy_wiki_index_925404
tags:
- concept
sources:
- url: https://api.polymarketanalytics.com/
- url: https://docs.polymarket.com/api-reference/introduction
- url: https://pypi.org/project/polymarket-apis/
cluster: Copytrade
doc_role: data-reference
---
# Polymarket API 레퍼런스

## 요약

<!-- para: para_001 -->
> Gamma API, Data API, CLOB API의 핵심 엔드포인트 요약 + curl/Python 예제 및 운영 패턴

<!-- para: para_002 -->
Polymarket의 주요 공개 엔드포인트(예: /events, /markets, /profiles)는 마켓 리스트, 이벤트 메타데이터, 사용자 프로필(공개된 경우)을 제공합니다. - **Gamma API**: 이벤트, 마켓, 프로필, 검색 등을 제공(공개)
- **Data API**: 포지션, 트레이드, 리더보드 등 상세 데이터
- **CLOB API**: 오더북, 주문, 체결 데이터(읽기: 공개)

간단한 호출 예:

GET https://gamma-api.polymarket.com/events?limit=20&active=true

<!-- para: para_003 -->
- GET /events?limit=20&active=true — 활성 이벤트 목록
- GET /markets?limit=50 — 마켓 목록(페이로드에 시장 상태 포함)
- GET /profiles/{address} — 공개 프로필(가능한 경우)

<!-- para: para_004 -->
curl -s "https://gamma-api.polymarket.com/events?limit=20&active=true" | jq '.'

<!-- para: para_005 -->
Polymarket의 `markets` 엔드포인트에서 최대 50개의 시장 데이터를 가져오는 예시입니다.

```bash
curl -s "https://gamma-api.polymarket.com/markets?limit=50" | jq '.results[] | {id: .id, name: .name, state: .state, price: .price}'
```

<!-- para: para_006 -->
curl -s "https://gamma-api.polymarket.com/profiles/0x1234..." | jq '.'

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

<!-- para: para_008 -->
GET https://gamma-api.polymarket.com/events?limit=20&active=true

<!-- para: para_009 -->
- GET /events?limit=20&active=true — 활성 이벤트 목록

<!-- para: para_010 -->
- GET /markets?limit=50 — 마켓 목록(페이로드에 시장 상태 포함)

## 추가 내용

<!-- para: para_011 -->
- **Public (인증 불필요)**: 마켓 데이터 조회, 가격 조회, 오더북 조회
- **L1 Auth (지갑 서명만)**: 초기 설정, API 키 생성
- **L2 Auth (API 키)**: 주문 생성/취소, 트레이드 조회, 포지션 관리

## 세부 내용

<!-- para: para_012 -->
Introduction - Polymarket Documentation

<!-- para: para_013 -->
Falcon API는 예측 시장에 필요한 실시간 시장 데이터, 거래자 분석, 예측 신호를 개발자와 AI 에이전트가 활용할 수 있도록 제공하는 인프라 계층입니다. 예측 시장 정보를 어떤 방식으로 사용할지 선택할 수 있습니다.

<!-- para: para_014 -->
Polymarket APIs는 PyPI에서 제공됩니다. 일부 기능은 JavaScript가 꺼져 있으면 제대로 동작하지 않을 수 있으니, 문제가 발생하면 JavaScript를 활성화해 보세요.
