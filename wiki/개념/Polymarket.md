---

title: "Polymarket 개요"
category: "개념"
created: "2026-04-05"
sources:
  - url: "https://gamma-api.polymarket.com/events"
    raw: "raw/fetched/2026-04-05-polymarket-events.md"
    added: "2026-04-05"
  - url: "https://polymarket.com"
    raw: "raw/fetched/2026-04-06-polymarket-home.md"
    added: "2026-04-06"
  - url: "https://gamma-api.polymarket.com/markets?limit=50"
    raw: "raw/fetched/2026-04-05-polymarket-markets.md"
    added: "2026-04-05"
related:
  - "[[기술/API/Polymarket-API-레퍼런스]]"
  - "[[개념/CLOB]]"
  - "[[개념/CTF]]"
  - "[[마켓/Polymarket-이벤트-스냅샷-2026-04-05]]"
  - "[[개념/Copytrade]]"
  - "[[트레이더/새로운-트레이더/프로필-템플릿|리더보드]]"
  - "[[마켓/크립토]]"
  - "[[전략/Copytrade/실행-비용]]"
  - "[[기술/API/레퍼런스]]"
  - "[[기술/Polymarket/개요-심화]]"
---

# Polymarket 개요

> Polymarket은 Polygon 기반의 주요 예측시장 플랫폼으로, 이벤트/마켓/오더북을 제공한다.

## 한 줄 요약

Polymarket은 이벤트별 결과에 베팅하는 예측시장으로 CLOB(중앙지정가주문장)를 통해 거래가 이루어지고, Yes/No 토큰을 사용해 결과를 정산한다.

## 핵심 내용 (심화)

- 플랫폼 구성: Polymarket은 프론트엔드(웹 인터페이스), Gamma API(퍼블릭/프라이빗 엔드포인트), CLOB(오더북) 및 결제/정산 계층으로 구성된다. Gamma API는 마켓과 이벤트 데이터를 제공하며, 거래(쓰기) 동작은 인증된 엔드포인트 및 온체인 트랜잭션과 연동된다.

- 체인·자산: L2인 Polygon 네트워크를 사용하며 결제 토큰으로 USDC.e(번들러/브리지된 USDC)가 주로 사용된다. 이로 인해 트랜잭션 수수료와 체인 확장성에 영향을 받는다.

- 주문/매칭 모델: 주문은 Limit/Market 같은 전통적 오더 타입과는 다르게 예측시장 특유의 Yes/No 포지션으로 다뤄진다. 내부적으로 CLOB(중앙지정가주문장) 구조를 사용하여 스프레드, 메이커 리베이트, 스코어링 규칙을 통해 체결 우선순위를 관리한다.

- 마켓 유형: 단일결과(Yes/No), 다중선택형, 사건 기반 분류(법률·스포츠·크립토 등)를 지원하며, Negative-Risk(자본 효율적 포지션)같은 특수 구조가 존재한다.

## 운영·리스크 관점

- 정산과 결과 검증: 이벤트 결과는 외부 신뢰원(예: 공시 자료, 스포츠 결과, 법원 판결)과 연동되어 수동/반자동으로 정산된다. 정산 지연, 결과 분쟁, 또는 잘못된 오라클 입력은 사용자 자산 리스크로 직결된다.

- 유동성·슬리피지: 시장 유동성이 낮은 마켓은 큰 체결 시 가격 왜곡(슬리피지)이 발생한다. 폴리마켓의 메이커 리베이트 제도는 유동성 제공을 장려하지만, 리베이트 구조와 오더북 깊이를 이해해야 추종 전략에서 과도한 추종 비용을 피할 수 있다.

- 규제·법적 리스크: 법률 이벤트나 규제 민감 이슈는 플랫폼·사용자 모두에 추가적 리스크를 야기할 수 있다. 법률 이벤트의 경우 결과 확정까지 장기 지연이 발생할 수 있다.

## 개발자·데이터 접근

- 주요 엔드포인트 예시

  - 이벤트 리스트: https://gamma-api.polymarket.com/events
  - 마켓 스냅샷: https://gamma-api.polymarket.com/markets?limit=50

- 실무 팁: API 호출 시 rate limit, 페이로드 스키마 변경 가능성, 그리고 인증이 필요한 엔드포인트와 퍼블릭(읽기 전용) 엔드포인트를 구분하여 구현해야 한다.

## 예제: 간단한 API 사용 (파이썬)

```python
import requests
r = requests.get("https://gamma-api.polymarket.com/events?limit=1&active=true", timeout=5)
data = r.json()
first = data.get("events", [{}])[0]
print(first.get("title"))
```

## 관련 문서

- [[기술/API/Polymarket-API-레퍼런스]] — API 엔드포인트 및 사용법
- [[개념/CLOB]] — 주문장 구조 및 스코어링 개념
- [[개념/CTF]] — 다중 결과 이벤트의 자본 효율성 설명
- [[마켓/Polymarket-이벤트-스냅샷-2026-04-05]] — 최근 수집 스냅샷과 비교
- [[기술/API/레퍼런스]] — API 엔드포인트 상세


