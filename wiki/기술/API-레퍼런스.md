---
title: "API 레퍼런스"
category: "api"
created: "2026-04-05"
source: "raw/02-API-레퍼런스.md"
related:
  - "[[Polymarket 개요]]"
  - "[[WebSocket-실시간데이터]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[Copytrade-전략분석]]"
---

# API 레퍼런스

> Polymarket 공개 API 엔드포인트와 사용 예제 요약

## 내용

Polymarket의 주요 공개 엔드포인트와 실무에서 바로 활용 가능한 예제를 포함한다. 모든 예제는 읽기 전용(public) 엔드포인트를 사용하며, 인증이 필요한 경로는 주석으로 구분한다.

### 핵심 엔드포인트

- Gamma API: /events, /markets, /profiles (Base: https://gamma-api.polymarket.com)
- Data API: /positions, /trades, /leaderboard (Base: https://data-api.polymarket.com)
- CLOB API: /orderbook, /orders (Base: https://clob.polymarket.com) — 읽기(조회)는 공개, 쓰기(주문 제출)는 인증 필요

---

## 빠른 시작 예제

### 마켓 목록 조회 (curl)

```bash
curl -s "https://gamma-api.polymarket.com/markets?limit=20" -H "Accept: application/json" | jq '.'
```

응답에서 마켓 id, 제목(title), 상태(active/closed), 가격 관련 필드를 확인할 수 있다. limit, offset(또는 cursor) 파라미터로 페이징할 수 있다.

### 특정 마켓의 오더북(간단 조회)

```bash
curl -s "https://clob.polymarket.com/orderbook?market_id=MARKET_ID" -H "Accept: application/json" | jq '.'
```

읽기 전용 오더북 조회는 공개. 주문 제출은 인증 필요.

### 특정 프로필(트레이더) 조회 (예: 리더보드 주소)

```bash
curl -s "https://gamma-api.polymarket.com/profiles/0xADDRESS" -H "Accept: application/json" | jq '.'
```

프로필 응답에서 공개 메타(닉네임, 활동 정보)와 포지션 요약을 확인할 수 있다.

---

## 응답 예제와 필드 설명

### Markets 엔드포인트(요약 응답 예시)

```json
{
  "markets": [
    {
      "id": "12345",
      "title": "Will X happen by 2026?",
      "state": "active",
      "price": 0.72,
      "volume": 12450,
      "created_at": "2026-03-30T12:34:56Z"
    }
  ],
  "next_cursor": "eyJvZmZzZXQiOjEw" 
}
```

- id: 마켓 고유 ID
- title: 마켓 제목
- state: active / closed
- price: 현재 시장 가격 (0-1 범위)
- volume: 누적 거래량
- next_cursor: 페이징을 위한 커서 (있을 경우 추가 호출로 다음 페이지 조회)

> 페이징: limit + cursor(or offset)을 사용. 커서 기반 페이징이 있는 경우 `next_cursor`를 다음 호출에 넣어 반복 조회.

### Orderbook 응답(요약)

```json
{
  "bids": [[0.70, 10], [0.69, 50]],
  "asks": [[0.73, 5], [0.74, 20]],
  "last_updated": "2026-04-05T10:12:00Z"
}
```

- bids/asks: [price, size] 형식의 배열
- last_updated: 서버 타임스탬프

---

## 실용 예제: TypeScript로 활성 마켓 가져와 필터링하기

```ts
import fetch from 'node-fetch';

type Market = {
  id: string;
  title: string;
  state: string;
  price: number;
  volume: number;
};

async function fetchActiveMarkets(limit = 50): Promise<Market[]> {
  const res = await fetch(`https://gamma-api.polymarket.com/markets?limit=${limit}`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const body = await res.json();
  // API 응답 구조에 따라 파싱
  return (body.markets || []).filter((m: Market) => m.state === 'active');
}

fetchActiveMarkets(20).then(ms => {
  ms.forEach(m => console.log(`${m.id} ${m.title} ${m.price}`));
});
```

- 실무 팁: 대량 조회 시 rate limit을 고려해 `sleep` 또는 `backoff`를 적용한다. 실패 시 재시도 로직을 구현할 것.

## 추가 예제: Python (requests)

```py
import requests

BASE = 'https://gamma-api.polymarket.com'

def fetch_active_markets(limit=20):
    r = requests.get(f"{BASE}/markets?limit={limit}")
    r.raise_for_status()
    body = r.json()
    return [m for m in body.get('markets', []) if m.get('state') == 'active']

if __name__ == '__main__':
    markets = fetch_active_markets(20)
    for m in markets:
        print(m['id'], m.get('title'), m.get('price'))
```

- 설명: Python 예제는 requests로 빠르게 마켓 리스트를 가져와 active만 필터링하는 간단한 흐름을 보여준다. 실무에서는 세션 재사용, 타임아웃, 재시도(backoff) 정책을 추가할 것.

## 실무 스니펫: 오더북과 리더보드 조회 (curl)

- 특정 마켓 오더북 조회 (curl)

```bash
curl -s "https://clob.polymarket.com/orderbook?market_id=MARKET_ID" -H "Accept: application/json" | jq '.'
```

- 리더보드 상위 트레이더 조회 (Data API)

```bash
curl -s "https://data-api.polymarket.com/leaderboard?limit=10" -H "Accept: application/json" | jq '.'
```

- 활용 팁: 오더북으로부터 bid/ask 깊이와 상위 레벨 사이즈를 읽어 포지션 사이징을 결정할 수 있다. 리더보드 엔드포인트를 주기적으로 가져와 신규 상위 트레이더를 감지하는 파이프라인에 활용하라.

## 결합 사용 예

1. 리더보드에서 상위 트레이더 지갑 주소를 가져온다.
2. 각 지갑의 프로필/포지션 엔드포인트를 호출하여 최근 포지션을 파싱한다.
3. 관심 마켓의 오더북 깊이와 매칭하여 copytrade 실행 가능성을 평가한다.

- 보안: 주문(쓰기)은 인증이 필요하므로 키 관리는 안전한 vault(환경변수, 시크릿 매니저 등)를 사용하라.


---

## 페이징, Rate Limit, 캐싱 팁

- 가능한 한 limit를 적절히 조절하여 한 번에 필요한 데이터만 가져온다.
- 커서 기반 페이징이 제공되면 offset보다 커서 사용을 권장 (일관된 데이터 스냅샷).
- 공개 API라도 호출 빈도가 많아지면 차단당할 수 있으므로 exponential backoff를 구현.
- 읽기 전용 데이터는 로컬 캐시(예: 1분 TTL)로 중복 호출을 줄이면 실무에서 안정적.

---

## 보안 및 개인정보

- 주문 제출(쓰기) 엔드포인트와 키 관리는 반드시 안전한 환경변수로 관리.
- 공개 프로필에 노출된 주소/닉네임을 저장할 때 개인정보 정책을 고려.

## 활용 팁

- 실시간 데이터가 필요하면 [[WebSocket-실시간데이터]] 문서와 연계하여 오더북/트레이드 스트림을 병행 사용
- 트레이더 분석을 위해 [[리더보드-트레이더-데이터]]의 프로필 엔드포인트를 활용
- Copytrade 전략 문서([[Copytrade-전략분석]])에서 제안한 지표와 결합하여 알파 시그널 생성

## 관련 문서

- [[Polymarket 개요]] — 플랫폼 구조 연계
- [[WebSocket-실시간데이터]] — 동기화 포인트
- [[리더보드-트레이더-데이터]] — 트레이더 메트릭 연계
- [[Copytrade-전략분석]] — copytrade 데이터 결합 팁
