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
  - "[[CTF]]"
  - "[[Negative-Risk]]"
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

## Merged content: 개념/CTF.md

# CTF (Conditional Token Framework)

> 한 줄 요약: 결과 기반 Yes/No 토큰 쌍을 생성·관리하는 프레임워크입니다.

CTF는 한 이벤트의 결과에 따라 조건부 토큰을 발행하는 구조입니다. 사용자는 USDC.e를 Split하여 Yes/No 토큰을 받고, 결과에 따라 승리 토큰을 Redeem해 USDC.e를 회수합니다. Merge, Split, Redeem 등의 온체인 흐름과 예시를 포함합니다.

## Merged content: 개념/Negative-Risk.md

# Negative-Risk (네거티브 리스크)

> 한 줄 요약: 다중 결과 이벤트에서 자본 효율적으로 포지션을 구성해 리스크를 음수로 만드는 전략적 접근입니다.

Negative-Risk는 여러 결과 중 특정 결과에만 Yes를 걸고 나머지 No를 합성해 자본 효율을 높이는 기법을 뜻합니다. 다중 결과 구조에서 헤지·아비트리지 형태로 사용되며, 예시와 계산법을 제공합니다. 실무에서는 슬리피지, 수수료, 마켓 유동성 한계를 반드시 고려해야 합니다.


(끝)
