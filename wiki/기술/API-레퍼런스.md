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
  - "[[CLOB]]"
  - "[[API-예제-샘플]]"
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

## 실무 스니펫: 오더북과 리더보드 결합(심화 예제)

다음 예제는 리더보드에서 상위 트레이더의 지갑을 가져와 해당 트레이더가 보유한 포지션이 관심 마켓에서 관측되는지 확인하고, 해당 마켓의 오더북 깊이를 함께 조회해 copytrade 실행 가능성을 평가하는 간단한 파이프라인입니다.

### 파이썬 예제 (requests)

```py
# 실무 수준의 간단한 파이프라인 예제입니다.
# 특징: 세션 재사용, 타임아웃 설정, 재시도(Retry) + 백오프, 간단한 rate-limit 대응
import time
import requests
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry

BASE_GAMMA = 'https://gamma-api.polymarket.com'
BASE_CLOB = 'https://clob.polymarket.com'
BASE_DATA = 'https://data-api.polymarket.com'

# 세션 설정: 재시도 전략과 커넥션 풀 재사용
session = requests.Session()
retries = Retry(
    total=5,
    backoff_factor=0.5,
    status_forcelist=(429, 500, 502, 503, 504),
    allowed_methods=("GET", "POST")
)
adapter = HTTPAdapter(max_retries=retries, pool_maxsize=10)
session.mount('https://', adapter)
session.headers.update({'Accept': 'application/json', 'User-Agent': 'autowiki/1.0'})

DEFAULT_TIMEOUT = (3, 10)  # (connect_timeout, read_timeout)

def safe_get(url, params=None, timeout=DEFAULT_TIMEOUT):
    try:
        r = session.get(url, params=params, timeout=timeout)
        # 429(Too Many Requests)에 대해서는 백오프 후 재시도 로직을 추가로 수행할 수 있음
        if r.status_code == 429:
            # 간단한 rate-limit 대응: Retry-After 헤더가 있으면 기다림
            wait = int(r.headers.get('Retry-After', '1'))
            time.sleep(wait)
            r = session.get(url, params=params, timeout=timeout)
        r.raise_for_status()
        return r.json()
    except requests.RequestException as e:
        # 로깅/지표 집계 후 None 반환
        print('network error', url, e)
        return None

def fetch_leaderboard(top=10):
    url = f"{BASE_DATA}/leaderboard"
    return safe_get(url, params={'limit': top}) or {}

def fetch_profile(address):
    url = f"{BASE_GAMMA}/profiles/{address}"
    return safe_get(url) or {}

def fetch_orderbook(market_id):
    url = f"{BASE_CLOB}/orderbook"
    return safe_get(url, params={'market_id': market_id}) or {}

# 간단한 결합 로직 (실무 팁 포함)
# - 병렬화: concurrent.futures를 사용하여 프로파일/오더북 호출 병렬화 권장
# - 캐시: 동일 market_id 반복 호출을 피하기 위해 메모리 캐시(예: TTL cache) 적용
# - 관찰: 각 요청의 latency, status_code를 모니터링

leaders = fetch_leaderboard(5).get('results', [])
for l in leaders:
    addr = l.get('address')
    profile = fetch_profile(addr)
    # profile에서 관심 마켓 id를 추출하는 로직을 작성
    for pos in profile.get('positions', []):
        market_id = pos.get('market_id')
        ob = fetch_orderbook(market_id)
        bids = ob.get('bids', [])
        asks = ob.get('asks', [])
        top_bid = bids[0] if bids else [0, 0]
        top_ask = asks[0] if asks else [0, 0]
        print(addr, market_id, 'bid', top_bid, 'ask', top_ask)

# 실무 권고 요약:
# 1) 민감 정보(키)는 코드에 하드코딩 금지
# 2) 네트워크 예외 처리 및 재시도, 타임아웃 설정 필수
# 3) rate-limit 발생 시 Retry-After를 존중하거나 exponential backoff 적용
# 4) 병렬 호출 시 rate-limit과 API 제공자의 이용 약관을 준수
```

이 스니펫은 개념 증명 수준이며, 실제 운영에서는 병렬화, 캐시, 재시도(backoff), 타임아웃과 rate-limit 제어를 추가해야 합니다.

### TypeScript 예제 (node-fetch)

```ts
import fetch from 'node-fetch'

const BASE_GAMMA = 'https://gamma-api.polymarket.com'
const BASE_CLOB = 'https://clob.polymarket.com'
const BASE_DATA = 'https://data-api.polymarket.com'

async function fetchLeaderboard(limit = 10) {
  const r = await fetch(`${BASE_DATA}/leaderboard?limit=${limit}`)
  if (!r.ok) throw new Error(`${r.status}`)
  return r.json()
}

async function fetchOrderbook(marketId: string) {
  const r = await fetch(`${BASE_CLOB}/orderbook?market_id=${marketId}`)
  return r.json()
}

(async () => {
  const leaders = await fetchLeaderboard(5)
  for (const l of leaders.results || []) {
    const addr = l.address
    // profile/positions 조회 로직 생략
    // 각 포지션의 market_id에 대해 fetchOrderbook 호출
  }
})()
```

- 운영 팁: 민감한 키는 절대 코드에 하드코딩하지 말고 안전한 시크릿 매니저를 사용하라. 읽기 전용 엔드포인트도 과도한 호출 시 차단될 수 있으므로 적절한 캐시와 rate control을 설계한다.

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
- [[API-예제-샘플]]
