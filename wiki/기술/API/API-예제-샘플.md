---
title: "Polymarket API 예제 (심화 샘플)"
category: "api"
created: "2026-04-05"
source: "raw/02-API-레퍼런스.md"
related:
  - "[[Polymarket API 레퍼런스]]"
  - "[[Polymarket 개요]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[CLOB]]"
---

# Polymarket API 예제 (심화 샘플)

> 공개 Polymarket REST API 호출 예제와 실제 운영에 필요한 세부 구현 샘플

## 개요

이 문서는 공개 엔드포인트에 대한 간단한 호출 예제뿐 아니라, 실전 사용을 위한
- 세션 재사용(Session),
- 재시도 및 백오프(Retry + Backoff),
- 응답 스키마 검증(schema validation),
- 리더보드와 마켓 데이터를 결합하는 간단한 워크플로우
등을 포함합니다. 프로덕션 코드에서는 적절한 로깅, 모니터링, rate-limit 대응을 반드시 추가하세요.

## 권장 패턴 요약

- 세션을 재사용하여 TCP 연결 오버헤드를 줄입니다.
- 실패 시 점진적 백오프를 사용해 rate limit과 네트워크 오류를 완화합니다.
- 응답 스키마를 단순히 검사해 예상 필드가 없을 경우 안전하게 건너뛰거나 경고를 냅니다.
- 리더보드에서 상위 트레이더를 가져와 각 트레이더가 활동한 마켓과 매칭하는 방식으로 연동합니다.

## Python 예제: requests + Retry

아래 예제는 requests.Session과 urllib3.util.retry를 사용해 재시도/백오프를 구현합니다.

```python
import requests
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry
import time

MARKETS_URL = "https://gamma-api.polymarket.com/markets?limit=10"
LEADERBOARD_URL = "https://clob.polymarket.com/rewards/leaderboard"

# 세션과 재시도 설정
session = requests.Session()
retries = Retry(total=5, backoff_factor=0.5, status_forcelist=(429, 502, 503, 504))
session.mount('https://', HTTPAdapter(max_retries=retries))

def fetch_json(url, timeout=10):
    try:
        r = session.get(url, timeout=timeout)
        r.raise_for_status()
        return r.json()
    except requests.HTTPError as e:
        print(f"HTTP error {e} for {url}")
    except requests.RequestException as e:
        print(f"Request failed {e} for {url}")
    return None

if __name__ == '__main__':
    markets = fetch_json(MARKETS_URL)
    lb = fetch_json(LEADERBOARD_URL)
    print(f"markets: {len(markets or [])}, leaderboard entries: {len(lb or [])}")
```

### 세부 설명
- backoff_factor가 0.5이면 첫 재시도는 0.5s, 다음은 1.0s, 2.0s ... 형태로 지연이 증가합니다.
- 429(Too Many Requests)과 같은 상태를 재시도 대상으로 포함해 rate-limit 일시적 충돌을 완화합니다.

## JSON 스키마 간단 검증 (예시)

간단한 스키마 검증을 통해 필수 필드 확인과 안전한 파싱을 수행할 수 있습니다. jsonschema 라이브러리를 권장합니다.

```python
from jsonschema import validate, ValidationError

market_schema = {
  "type": "object",
  "properties": {
    "markets": {"type": "array"}
  },
  "required": ["markets"]
}

try:
    validate(instance=markets, schema=market_schema)
except ValidationError:
    print("Unexpected markets schema; skipping processing")
```

## Bash + jq 예제: 리더보드 상위 트레이더의 프로필/포지션 조회

```bash
curl -s "https://clob.polymarket.com/rewards/leaderboard" | jq -r '.[0:5][] | .address' | while read addr; do
  curl -s "https://gamma-api.polymarket.com/profiles/$addr" | jq '{address: .address, positions: .positions}'
done
```

- 실제 API 필드명은 엔드포인트와 버전에 따라 다를 수 있으니, 결과 JSON을 먼저 확인하세요.

## 리더보드-마켓 연동 워크플로우 (간단한 예)

1. 리더보드 상위 N명 주소 수집
2. 각 주소의 프로필/포지션 조회
3. 포지션에 포함된 market_id로 마켓 정보를 조회하여 매칭
4. 트레이더별로 활동 마켓 요약(문맥: volume, 최근 트랜잭션 시간 등)

이 과정을 자동화하면, 누가 어떤 마켓에서 높은 영향력을 발휘하는지 파악할 수 있어 copytrade 대상 선별시 유용합니다.

## 운영상 주의사항

- Rate limit: 반복 호출 시 지연(예: sleep + backoff)을 반드시 추가하세요.
- 인증: 공개 엔드포인트는 인증 없이 접근 가능하지만, 더 민감한 엔드포인트는 API key가 필요할 수 있습니다.
- 스키마 변경: 응답 스키마가 바뀌면 파서가 실패하므로 schema validation과 로깅을 통해 빠르게 감지하세요.
- 개인정보: 공개되지 않은 지갑/개인 정보는 수집/공유하지 마세요.

## 관련 문서

- [[Polymarket API 레퍼런스]] — 엔드포인트 설명
- [[실시간데이터]] — WebSocket 연계
- [[리더보드-트레이더-데이터]] — 리더보드 데이터 구조 및 해석
- [[CLOB]] — 주문장부 관련 개념 및 용어

## 참조

[^1]: https://gamma-api.polymarket.com/markets?limit=10 — 마켓 목록 API (샘플 호출)
[^2]: https://clob.polymarket.com/rewards/leaderboard — 리더보드 엔드포인트 (샘플 호출)

