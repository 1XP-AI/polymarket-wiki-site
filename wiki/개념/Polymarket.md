---
title: "Polymarket 개요"
category: "concept"
created: "2026-04-05"
source: "raw/01-Polymarket-개요.md"
related:
  - "[[API-레퍼런스]]"
  - "[[CLOB]]"
  - "[[Negative-Risk]]"
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

## 관련 문서

- [[API-레퍼런스]] — API 엔드포인트 및 사용법
- [[CLOB]] — 주문장 구조 및 스코어링 개념
- [[Negative-Risk]] — 다중 결과 이벤트의 자본 효율성 설명
