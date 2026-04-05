---
title: "Polymarket API 예제 (샘플)"
category: "api"
created: "2026-04-05"
source: "raw/02-API-레퍼런스.md"
related:
  - "[[Polymarket API 레퍼런스]]"
  - "[[Polymarket 개요]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[CLOB]]"
---

# Polymarket API 예제 (샘플)

> 공개 Polymarket REST API 호출 예제와 응답 예시

## 내용

아래 예제는 인증이 필요 없는 공개 엔드포인트 호출 샘플이다. 실제 호출 시 rate limit을 고려하고, 프로덕션에서는 재시도와 오류 처리를 추가해야 한다.

### 마켓 목록 요청

```bash
curl -s "https://gamma-api.polymarket.com/markets?limit=5"
```

샘플 응답(요약):

```json
{
  "markets": [
    {
      "id": "mkt_1",
      "question": "Will X happen?",
      "status": "open",
      "volume": 1234.56
    },
    {
      "id": "mkt_2",
      "question": "Will Y happen?",
      "status": "open",
      "volume": 987.65
    }
  ]
}
```

### 이벤트(활성 이벤트) 조회

```bash
curl -s "https://gamma-api.polymarket.com/events?limit=10&active=true"
```

### 리더보드(보상) 예시

```bash
curl -s "https://clob.polymarket.com/rewards/leaderboard"
```

## 참고

- 실제 JSON 구조는 엔드포인트와 버전에 따라 다르므로, 응답의 top-level 필드를 확인하고 필요한 항목만 파싱하세요.
- 수집 스크립트는 응답을 로컬 파일(raw/fetched/YYYY-MM-DD-...)로 저장하고, _fetch-log.md에 기록합니다.

## 관련 문서

- [[Polymarket API 레퍼런스]] — 엔드포인트 설명
- [[실시간데이터]] — WebSocket 연계
