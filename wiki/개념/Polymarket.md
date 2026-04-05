---

title: "Polymarket 개요"
category: "concept"
created: "2026-04-05"
related:
  - "[[API-레퍼런스]]"
  - "[[CLOB]]"
  - "[[Negative-Risk]]"
  - "[[Polymarket-이벤트-스냍샷-2026-04-05]]"
  - "[[Copytrade-심화]]"
  - "[[리더보드]]"
  - "[[크립토]]"
  - "[[실행-비용]]"
sources:
  - url: "https://gamma-api.polymarket.com/events"
    added: "2026-04-05"
---

# Polymarket 개요

> Polymarket은 Polygon 기반의 주요 예측시장 플랫폼으로, 이벤트/마켓/오더북을 제공한다.

## 한 줄 요약

Polymarket은 이벤트별 결과에 베팅하는 예측시장으로 CLOB(중앙지정가주문장)를 통해 거래가 이루어지고, Yes/No 토큰을 사용해 결과를 정산한다.

## 핵심 내용

- 플랫폼 구조: Gamma API, Data API, CLOB API(읽기: Public, 쓰기: 인증 필요)
- 자산/체인: Polygon, 결제 토큰 USDC.e
- 주문 생명주기: 생성 → 오더북 등록 → 매칭 → 체결 → 정산
- 특이점: Maker rebate(메이커 리베이트), Negative Risk 마켓(자본 효율적 거래)

## 예제: 이벤트 목록 API 호출

아래 예제는 Gamma API로 활성 이벤트(마켓) 목록을 가져오는 간단한 curl 호출 예시이다.

```bash
# 최근 활성 이벤트 20개 조회 (예시)
curl -s "https://gamma-api.polymarket.com/events?limit=20&active=true" -H "Accept: application/json" -m 5
```

응답(요약):
- events 배열에 각 이벤트(마켓) 객체가 포함됨
- 각 이벤트는 id, title, description, markets 등의 필드를 가짐
- 실제 호출 시 rate limit과 응답 스키마 변동에 주의

간단한 파이썬 예제(요청 후 첫 마켓 제목 출력):

```python
import requests
r = requests.get("https://gamma-api.polymarket.com/events?limit=1&active=true", timeout=5)
data = r.json()
first = data.get("events", [{}])[0]
print(first.get("title"))
```

## 관련 문서

- [[API-레퍼런스]] — API 엔드포인트 및 사용법
- [[CLOB]] — 주문장 구조 및 스코어링 개념
- [[Negative-Risk]] — 다중 결과 이벤트의 자본 효율성 설명
- [[Polymarket-이벤트-스냅샷-2026-04-05]] — 최근 수집 스냅샷과 비교

