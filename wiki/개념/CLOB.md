---
title: "CLOB"
category: "concept"
created: "2026-04-05"
source: "raw/01-Polymarket-개요.md"
related:
  - "[[Polymarket-개요]]"
  - "[[API-레퍼런스]]"
---

# CLOB (Central Limit Order Book)

> 한 줄 요약: 중앙지정가주문장(Central Limit Order Book) 구조와 주문 생명주기.

## 내용

CLOB는 Bid/Ask로 구성된 오더북으로, 주문 생성→스코어링→매칭→체결→정산 순으로 진행된다. 가격은 0~1 범위로 확률을 나타내며, 스프레드와 오더북 깊이가 유동성 지표가 된다.
