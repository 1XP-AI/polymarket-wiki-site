---
title: "Polymarket 개요"
category: "market"
created: "2026-04-05"
source: "raw/01-Polymarket-개요.md"
related:
  - "[[API-레퍼런스]]"
  - "[[Copytrade-전략분석]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[CLOB]]"
---

# Polymarket 개요

> Polymarket의 핵심 구조와 운영 메커니즘 요약

## 내용

Polymarket은 Polygon 기반의 대형 예측시장 플랫폼으로, 이벤트와 마켓 구조로 구성된다. 각 이벤트는 하나의 질문(예: ‘2026 대선 승자’)이며, 이벤트 내 마켓은 개별 결과 옵션(예: ‘후보 A 승’)을 나타낸다. 가격은 0.00–1.00 범위로 확률을 표현하며, CLOB(오더북) 시스템을 통해 매수(Bid)/매도(Ask)가 매칭된다.

주요 리소스는 Gamma API(마켓/이벤트/프로필), Data API(포지션·트레이드·리더보드), CLOB API(오더북·주문)로 분리되어 있다. 포지션은 Yes/No 토큰 쌍으로 발행되며, 결과에 따라 $1.00 또는 $0.00로 정산된다. Maker는 리베이트를 받을 수 있고, Taker는 수수료가 부과된다.

## 관련 문서

- [[API-레퍼런스]] — Polymarket의 API 엔드포인트 정리
- [[Copytrade-전략분석]] — 플랫폼 상에서의 카피트레이드 전략
- [[리더보드-트레이더-데이터]] — 트레이더 데이터 및 리더보드 정보
