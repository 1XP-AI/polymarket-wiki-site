---
title: "CLOB"
category: "concept"
created: "2026-04-05"
source: "raw/01-Polymarket-개요.md"
related:
  - "[[Polymarket 개요]]"
  - "[[Copytrade 전략분석]]"
  - "[[API 레퍼런스]]"
  - "[[리더보드-데이터]]"
---

# CLOB (Central Limit Order Book)

> 한 줄 요약: CLOB는 중앙지정가주문장으로, Bid/Ask 방식의 오더북 매칭을 의미합니다.

## 내용

CLOB는 주문이 가격-수량 형태로 쌓이고, 매칭 엔진이 호가를 교차시켜 체결을 발생시키는 구조입니다. Polymarket의 CLOB는 읽기용 API가 공개되어 있으며, maker에는 리베이트가 존재할 수 있습니다. 스프레드·체결량·슬리피지 관리가 중요한 개념입니다.

원본: raw/01-Polymarket-개요.md

## 관련 문서

- [[Polymarket 개요]] — Polymarket의 전체 구조와 CLOB의 위치 설명
- [[Copytrade 전략분석]] — CLOB 특성이 Copytrade 실행리스크(슬리피지, 시장충격)에 미치는 영향
- [[API-레퍼런스]] — CLOB 읽기·모니터링을 위한 엔드포인트 참조
- [[리더보드-데이터]] — 리더보드 트레이더의 대규모 주문이 오더북에 미치는 사례 분석
- [[Polymarket 개요]] — 교차참조 보강
