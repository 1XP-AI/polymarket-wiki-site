---
title: "API-예제-샘플"
category: "infrastructure"
created: "2026-04-05"
source: "auto"
related:
  - "[[API 레퍼런스]]"
  - "[[리더보드-데이터]]"
---

# API-예제-샘플

> 한 줄 요약: Polymarket API 호출 예제와 응답 파싱, 재시도/타임아웃 처리 샘플을 제공한다.

## 내용

아래 예제는 Polymarket의 공개 API에서 이벤트, 마켓, 리더보드 데이터를 신뢰성 있게 수집하는 방법을 보여준다. curl, Python requests, Node.js fetch 예제를 포함한다. 수집된 원시 응답은 raw/fetched/에 파일로 저장하여 재검증 가능하게 한다.

## 예제 요약

- curl: 간단한 호출과 jq 파싱
- Python: requests + Retry 설정, 응답 검사, 로컬 파일 저장
- Node.js: fetch 사용 예제

## 예제 코드

### curl (간단 호출)

- 리더보드 상위 10명 가져오기

```bash
curl -s "https://clob.polymarket.com/rewards/leaderboard?limit=10" | jq '.'
```

- 활성 이벤트 목록

```bash
curl -s "https://gamma-api.polymarket.com/events?limit=20&active=true" | jq '.events'
```

### Python (requests)

```python
import requests
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry
import json
from datetime import datetime

session = requests.Session()
retries = Retry(total=3, backoff_factor=0.5, status_forcelist=[429,500,502,503,504])
session.mount('https://', HTTPAdapter(max_retries=retries))

def fetch_and_store(url, outpath):
    resp = session.get(url, timeout=6)
    resp.raise_for_status()
    data = resp.json()
    with open(outpath, 'w', encoding='utf-8') as f:
        json.dump({'fetched': str(datetime.utcnow()), 'url': url, 'data': data}, f, ensure_ascii=False, indent=2)
    return data

if __name__ == '__main__':
    url = "https://gamma-api.polymarket.com/events?limit=20&active=true"
    data = fetch_and_store(url, 'raw/fetched/2026-04-05-polymarket-events.md')
    print('events:', len(data.get('events', [])))
```

설명: 세션 재사용과 Retry를 통해 안정성을 높이고, 원시 응답을 raw/fetched/에 저장하여 재검증을 가능하게 한다.

### Node.js (fetch)

```js
import fs from 'fs';
import fetch from 'node-fetch';

export async function fetchMarkets(limit = 50) {
  const url = `https://gamma-api.polymarket.com/markets?limit=${limit}`;
  const res = await fetch(url, { timeout: 5000 });
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const data = await res.json();
  fs.writeFileSync(`raw/fetched/${new Date().toISOString().slice(0,10)}-markets.json`, JSON.stringify({fetched: new Date().toISOString(), url, data}, null, 2));
  return data.markets || data;
}

fetchMarkets(20).then(m => console.log(m.length)).catch(console.error);
```

## 권장사항

- 호출 빈도는 rate limit을 고려해 throttling 한다.
- 중요한 데이터(리더보드 스냅샷 등)는 원시 파일로 보관한다.
- 응답 스키마 변경에 대비해 필드 접근은 방어적으로 처리한다.

## 관련 문서

- [[API 레퍼런스]]
- [[리더보드-데이터]]

## 참조

[^1]: https://gamma-api.polymarket.com/events — events 엔드포인트 (raw/fetched/2026-04-05-polymarket-events.md 스냅샷)
[^2]: https://gamma-api.polymarket.com/markets — markets 엔드포인트
