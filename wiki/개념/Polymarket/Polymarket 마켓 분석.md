---
id: legacy_wiki_c2a67b
title: Polymarket 마켓 분석
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: 2026-04-18T16:05:00Z
as_of: 2026-04-18
owners:
- wiki-system
source_count: 2
sources:
- url: file://raw/01-Polymarket-개요.md
evidence_coverage: 1.0
confidence: medium
tags:
- concept
cluster: Polymarket
doc_role: analysis
cluster_group: 마켓 구조/거래 메커니즘
---

## 요약

> Polymarket 마켓 분석은 가격, 확률, 오더북, 결과 정산이 서로 어떻게 연결되는지 해석하는 분석 문서다.

이 문서는 개별 마켓을 단순한 카테고리 목록으로 보는 대신, 가격 해석과 체결 구조 관점에서 읽는 방법을 정리한다.
핵심은 예측 시장 가격을 확률로 읽고, Yes/No 토큰과 CLOB 오더북이 그 가격을 어떻게 형성하는지 이해하는 것이다.

## 핵심 주장

- Polymarket 마켓 가격은 사건 발생 확률에 대한 시장의 현재 합의를 압축해서 보여 준다.
- 가격이 $0.50 근처에 머문다는 것은 시장이 해당 결과를 거의 반반 확률로 보고 있다는 뜻이다.
- Yes 토큰과 No 토큰은 동일 사건의 양쪽 포지션을 표현하며, 각 가격은 오더북에서 매수·매도 호가가 부딪히며 결정된다.
- 단일 사건형 마켓은 보통 binary 구조를 가지지만, 범위형 또는 다중 결과형 마켓은 결과 해석과 포지션 관리가 더 복잡해진다.
- 마켓 분석의 핵심은 카테고리 자체보다 가격이 어떤 정보, 유동성, 만기 구조를 반영하고 있는지 읽는 데 있다.

## 관련 엔티티

- `market-structure`: 마켓 구조
- `orderbook`: CLOB
- `token-model`: Yes/No 토큰

## 참고 근거

- file://raw/01-Polymarket-개요.md

## 관련 문서

[[Polymarket 개요]], [[정치 예측 마켓]], [[법률/사건 예측 마켓]], [[크립토 예측 마켓]], [[마켓 메이커 & 리베이트 프로그램]]
