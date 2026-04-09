---
id: source_summary_src_wiki_polymarket_md_b0665680
title: 'Source Summary: Polymarket 개요'
type: source_summary
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T14:10:09Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: high
related_pages:
- legacy_wiki_polymarket_b06656
tags:
- internal
- internal
---

# Source Summary: Polymarket 개요

## Summary

<!-- para: para_001 -->
> Polymarket은 Polygon 기반의 주요 예측시장 플랫폼으로, 이벤트/마켓/오더북을 제공한다.

## Key Facts

<!-- para: para_002 -->
Polymarket은 이벤트별 결과에 베팅하는 예측시장으로 CLOB(중앙지정가주문장)를 통해 거래가 이루어지고, Yes/No 토큰을 사용해 결과를 정산한다.

<!-- para: para_003 -->
- 플랫폼 구성: Polymarket은 프론트엔드(웹 인터페이스), Gamma API(퍼블릭/프라이빗 엔드포인트), CLOB(오더북) 및 결제/정산 계층으로 구성된다. Gamma API는 마켓과 이벤트 데이터를 제공하며, 거래(쓰기) 동작은 인증된 엔드포인트 및 온체인 트랜잭션과 연동된다.

## Details

<!-- para: para_004 -->
- 정산과 결과 검증: 이벤트 결과는 외부 신뢰원(예: 공시 자료, 스포츠 결과, 법원 판결)과 연동되어 수동/반자동으로 정산된다. 정산 지연, 결과 분쟁, 또는 잘못된 오라클 입력은 사용자 자산 리스크로 직결된다. - 유동성·슬리피지: 시장 유동성이 낮은 마켓은 큰 체결 시 가격 왜곡(슬리피지)이 발생한다.

<!-- para: para_005 -->
- 주요 엔드포인트 예시

- 이벤트 리스트: https://gamma-api.polymarket.com/events
  - 마켓 스냅샷: https://gamma-api.polymarket.com/markets?limit=50

- 실무 팁: API 호출 시 rate limit, 페이로드 스키마 변경 가능성, 그리고 인증이 필요한 엔드포인트와 퍼블릭(읽기 전용) 엔드포인트를 구분하여 구현해야 한다.

<!-- para: para_006 -->
```python
import requests
r = requests.get("https://gamma-api.polymarket.com/events?limit=1&active=true", timeout=5)
data = r.json()
first = data.get("events", [{}])[0]
print(first.get("title"))
```

<!-- para: para_007 -->
- [[기술/API/Polymarket-API-레퍼런스]] — API 엔드포인트 및 사용법
- [[개념/CLOB]] — 주문장 구조 및 스코어링 개념
- [[개념/CTF]] — 다중 결과 이벤트의 자본 효율성 설명
- [[마켓/Polymarket-이벤트-스냅샷-2026-04-05]] — 최근 수집 스냅샷과 비교
- [[기술/API/Polymarket-API-레퍼런스]] — API 엔드포인트 상세

## Open Questions

<!-- para: para_008 -->
- 마켓 스냅샷: https://gamma-api.polymarket.com/markets?limit=50

<!-- para: para_009 -->
r = requests.get("https://gamma-api.polymarket.com/events?limit=1&active=true", timeout=5)
