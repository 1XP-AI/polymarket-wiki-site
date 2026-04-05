---
title: "Polymarket API 레퍼런스 요약"
category: "infrastructure"
created: "2026-04-05"
source: "raw/02-API-레퍼런스.md"
related:
  - "[[Polymarket 개요]]"
  - "[[CLOB]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[Polymarket-이벤트-스냅샷-2026-04-05]]"
---

# Polymarket API 레퍼런스 요약

> Gamma API, Data API, CLOB API의 핵심 엔드포인트 요약

## 내용

- Gamma API: 이벤트, 마켓, 프로필, 검색 등을 제공(공개)
- Data API: 포지션, 트레이드, 리더보드 등 상세 데이터
- CLOB API: 오더북, 주문, 체결 데이터(읽기: 공개)

간단한 호출 예:

```
GET https://gamma-api.polymarket.com/events?limit=20&active=true
```

## 관련 문서

- [[Polymarket 개요]]

## 참조

[^1]: raw/02-API-레퍼런스.md
