---
title: "Polymarket 개요"
category: "market"
created: "2026-04-05"
source: "raw/01-Polymarket-개요.md"
related:
  - "[[API-레퍼런스]]"
  - "[[CLOB]]"
  - "[[Negative-Risk]]"
---

# Polymarket 개요

> 한 줄 요약: Polymarket 플랫폼 구조와 핵심 개념(이벤트·마켓·오더북·토큰)을 정리한다.

## 내용

(원본: raw/01-Polymarket-개요.md)
Polymarket은 Polygon 위에서 동작하는 예측 시장 플랫폼으로, Gamma API, Data API, CLOB API 등 주요 API를 통해 마켓과 이벤트, 오더북 정보를 제공한다. 가격은 0~1 범위로 확률을 나타내며 CLOB(중앙지정가주문장)를 통해 주문이 매칭된다. 포지션은 CTF(Conditional Token Framework) 토큰으로 표현되며, Yes/No 토큰 쌍의 생성/병합/분할로 유동성이 관리된다.

## 관련 문서

- [[API-레퍼런스]] — Polymarket의 Gamma/Data/CLOB API 설명
- [[CLOB]] — 주문장(오더북)과 주문 생명주기 자세히 설명
- [[Negative-Risk]] — Negative Risk 마켓 구조와 자본 효율성
