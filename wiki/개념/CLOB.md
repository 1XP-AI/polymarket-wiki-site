---
title: "CLOB"
category: "concept"
created: "2026-04-05"
source: "raw/01-Polymarket-개요.md"
related:
  - "[[Polymarket-개요]]"
  - "[[API-레퍼런스]]"
  - "[[Copytrade-전략분석]]"
---

# CLOB (Central Limit Order Book)

> 한 줄 요약: 중앙지정가주문장(Central Limit Order Book) 구조와 주문 생명주기.

## 내용

CLOB는 Bid/Ask로 구성된 오더북으로, 주문 생성→스코어링→매칭→체결→정산 순으로 진행된다. 가격은 0~1 범위로 확률을 나타내며, 스프레드와 오더북 깊이가 유동성 지표가 된다.

Polymarket의 CLOB는 Polygon 네트워크 위에서 운영된다[^1]. 주문은 REST API를 통해 제출할 수 있다[^2].

## 참조

[^1]: https://gamma-api.polymarket.com/events — "Polymarket Events API" (2026-04-05 확인)
[^2]: raw/02-API-레퍼런스.md — API 엔드포인트 상세
