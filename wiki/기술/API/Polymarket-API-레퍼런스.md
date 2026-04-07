---
title: "Polymarket API 레퍼런스"
category: "api"
created: "2026-04-05"
sources:
  - url: "https://gamma-api.polymarket.com/markets?limit=50"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://www.polyverify.com/leaderboard"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://polymarket-bot.co/polymarket-api-tutorial"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://docs.polymarket.com/api-reference/clients-sdks"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://www.alphascope.app/blog/polymarket-bot-tutorial"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://www.predictengine.ai/blog/polymarket-api-tutorial"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://github.com/sambergo/quick-polymarket-api-setup-tutorial"
    raw: "raw/fetched/2026-04-07-negative-risk-and-api.md"
    added: "2026-04-07"
  - url: "https://gamma-api.polymarket.com/markets?limit=10"
    added: "2026-04-05"
  - url: "https://clob.polymarket.com/rewards/leaderboard"
    added: "2026-04-05"
related:
  - "[[개념/Polymarket]]"
  - "[[개념/CLOB]]"
  - "[[트레이더/리더보드/데이터]]"
  - "[[마켓/Polymarket-이벤트-스냅샷-2026-04-05]]"
  - "[[기술/WebSocket-실시간데이터]]"
  - "[[트레이더/Theo]]"
  - "[[전략/Copytrade/자동화-플로우]]"
  - "[[전략/Copytrade/Copytrade-리더보드-심화]]"
---

# Polymarket API 레퍼런스

> Gamma API, Data API, CLOB API의 핵심 엔드포인트 요약 + curl/Python 예제 및 운영 패턴

## 개요

Polymarket의 주요 공개 엔드포인트(예: /events, /markets, /profiles)는 마켓 리스트, 이벤트 메타데이터, 사용자 프로필(공개된 경우)을 제공합니다.

- **Gamma API**: 이벤트, 마켓, 프로필, 검색 등을 제공(공개)
- **Data API**: 포지션, 트레이드, 리더보드 등 상세 데이터
- **CLOB API**: 오더북, 주문, 체결 데이터(읽기: 공개)

간단한 호출 예:

```
GET https://gamma-api.polymarket.com/events?limit=20&active=true
```

## 주요 엔드포인트

- GET /events?limit=20&active=true — 활성 이벤트 목록
- GET /markets?limit=50 — 마켓 목록(페이로드에 시장 상태 포함)
- GET /profiles/{address} — 공개 프로필(가능한 경우)

## curl 예제

### 1) 활성 이벤트 가져오기

```bash
curl -s "https://gamma-api.polymarket.com/events?limit=20&active=true" | jq '.'
```

### 2) 특정 마켓 가져오기

```bash
curl -s "https://gamma-api.polymarket.com/markets?limit=50" | jq '.results[] | {id: .id, name: .name, state: .state, price: .price}'
```

### 3) 리더보드에서 트레이더 프로필 조회(주소를 알 때)

```bash
curl -s "https://gamma-api.polymarket.com/profiles/0x1234..." | jq '.'
```

> 주의: 실제 주소나 프로필 엔드포인트는 공개 여부에 따라 응답이 제한될 수 있습니다.

### 예시 응답(JSON) 샘플

```json
{
  "id": "market_abc123",
  "name": "Will country X hold elections in 2026?",
  "state": "open",
  "price": 0.42,
  "liquidity": 12500
}
```

### jq를 이용한 간단한 파이프라인

- 모든 오픈 마켓의 id와 현재 가격만 추출하여 CSV로 저장:

```bash
curl -s "https://gamma-api.polymarket.com/markets?limit=50" \
  | jq -r '.results[] | [.id, (.price|tostring)] | @csv' > markets.csv
```

- 특정 트레이더의 최근 포지션 요약(가정된 필드 사용):

```bash
curl -s "https://gamma-api.polymarket.com/profiles/0x1234.../positions" \
  | jq '.positions | map({market_id: .marketId, size: .size, side: .side})'
```

## Python 예제

실전 사용을 위한 권장 패턴:

- 세션을 재사용하여 TCP 연결 오버헤드를 줄입니다.
- 실패 시 점진적 백오프를 사용해 rate limit과 네트워크 오류를 완화합니다.
- 응답 스키마를 검사해 예상 필드가 없을 경우 안전하게 건너뛰거나 경고를 냅니다.
- 리더보드에서 상위 트레이더를 가져와 각 트레이더가 활동한 마켓과 매칭하는 방식으로 연동합니다.

```python
import requests
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry

session = requests.Session()
adapter = HTTPAdapter(max_retries=Retry(total=3, backoff_factor=1, status_forcelist=[429, 500, 502, 503, 504]))
session.mount("https://", adapter)

resp = session.get("https://gamma-api.polymarket.com/markets", params={"limit": 50})
if resp.status_code == 200:
    data = resp.json()
    for m in data.get("results", []):
        print(m.get("id"), m.get("name"), m.get("state"))
```

## Node.js 예제

Node.js `fetch`를 사용한 예제:

```js
import fetch from 'node-fetch';

async function fetchMarkets(limit = 50) {
  const url = `https://gamma-api.polymarket.com/markets?limit=${limit}`;
  const res = await fetch(url, { timeout: 5000 });
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const data = await res.json();
  return data.markets || data;
}

fetchMarkets(20).then(m => console.log(m.slice(0,3))).catch(console.error);
```

## 리더보드-마켓 연동 워크플로우

1. 리더보드 상위 N명 주소 수집
2. 각 주소의 프로필/포지션 조회
3. 포지션에 포함된 market_id로 마켓 정보를 조회하여 매칭
4. 트레이더별로 활동 마켓 요약(문맥: volume, 최근 트랜잭션 시간 등)

이 과정을 자동화하면, 누가 어떤 마켓에서 높은 영향력을 발휘하는지 파악할 수 있어 copytrade 대상 선별시 유용합니다.

## 운영상 주의사항

- **Rate limit**: 동일 엔드포인트를 짧은 간격으로 반복 호출하지 마십시오. 반복 호출 시 지연(sleep + backoff)을 반드시 추가하세요.
- **인증**: 공개 엔드포인트는 인증 없이 접근 가능하지만, 더 민감한 엔드포인트는 API key가 필요할 수 있습니다.
- **스키마 변경**: 응답 스키마가 바뀌면 파서가 실패하므로 schema validation과 로깅을 통해 빠르게 감지하세요.
- **개인정보**: 공개되지 않은 지갑/개인 정보는 수집/공유하지 마세요.
- **실시간 데이터**: 실시간 업데이트가 필요하면 WebSocket 피드와 조합하여 사용하고, 백필(backfill)은 REST API로 보강하세요.
- **인증 엔드포인트**: 인증이 필요한 엔드포인트는 키 없이 접근 불가하므로 raw 수집 단계에서 건너뛰도록 설계하세요.

## 관련 문서

- [[기술/WebSocket-실시간데이터]] — WebSocket 실시간 데이터 / 실시간 데이터 수집 방법
- [[기술/온체인-컨트랙트]] — 온체인 연동이 필요한 경우
- [[트레이더/리더보드/데이터]] — 리더보드 데이터 구조 및 해석
- [[개념/CLOB]] — 주문장부 관련 개념 및 용어
- [[전략/Copytrade/Copytrade-리더보드-심화]] — 리더보드 분석을 Copytrade 파이프라인에 연결

## 참조

[^1]: raw/02-API-레퍼런스.md
