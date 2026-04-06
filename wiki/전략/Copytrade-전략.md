---
title: "Copytrade 전략 분석"
category: "strategy"
created: "2026-04-05"
sources:
  - url: "raw/03-Copytrade-전략분석.md"
    raw: "raw/03-Copytrade-전략분석.md"
    added: "2026-04-05"
  - url: "https://www.holypoly.io/blog/how-to-copy-trade-polymarket"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-06"
  - url: "https://coincodecap.com/top-10-tools-to-copy-trade-polymarket-traders"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-06"
  - url: "https://news.polymarket.com/p/copytrade-wars"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-06"
related:
  - "[[Copytrade]]"
  - "[[리더보드-데이터]]"
  - "[[개념-CLOB]]"
---

# Copytrade 전략 분석

> 리더보드 기반 카피트레이드의 주요 전략과 리스크 관리 방안.

## 내용

성공적인 카피트레이드는 트레이더 선정(승률, 위험 프로필), 포지션 스케일링, 진입/청산 규칙, 손절(스톱로스) 전략을 포함합니다. 리더보드의 빈도(거래 빈도)와 포지션 사이즈를 분석하여 자동 복제 비율을 결정해야 합니다. 또한 CLOB 기반 주문집행의 슬리피지와 수수료를 시뮬레이션하는 것이 필수입니다.

## 관련 문서

- [[CLOB]] — 주문집행 이해
- [[리더보드-데이터]] — 트레이더 데이터 소스


<!-- MERGED from 기술/온체인/컨트랙트.md -->

# 온체인 컨트랙트

> 한 줄 요약: 폴리마켓의 온체인 토큰·정산 메커니즘과 서명/체결 흐름.

## 내용

Polymarket은 Polygon 체인 위에서 결과 정산과 토큰 수령을 처리한다. CTF 토큰의 Split/Merge, 승리 토큰 Redeem 과정은 온체인 트랜잭션으로 실행된다. 서명된 주문은 CLOB를 통해 제출되고 체결 시 온체인 정산이 이루어진다.

## 관련 문서

- [[CTF]] — CTF 토큰의 Split/Merge/Redeem 흐름
- [[온체인-ABI-예제]] — (초안) 샘플 ABI 및 호출 예제
- [[Copytrade]] — 온체인 데이터를 통한 포지션 검증


<!-- MERGED from 전략/마켓메이커-리베이트.md -->

# 마켓메이커 리베이트

> Maker 리베이트 프로그램과 오더북 기반 수수료/리베이트 메커니즘 설명

## 내용

Polymarket의 Maker는 오히려 리베이트를 받는 구조를 운영한다. 리베이트는 유동성을 제공하는 참여자에게 지급되어 오더북의 스프레드를 좁히고 거래 깊이를 증가시킨다. 마켓메이커가 고려할 항목: 스프레드 설정, 주문 깊이, 주문만료 정책, 체인상 가스 정책 및 리베이트 수령 조건.

리베이트 프로그램의 상세 조건(지급 기준, 기간, 최소 거래량 등)은 플랫폼 문서와 보상 프로그램 공지를 참조해 업데이트해야 한다. 예시 및 계산식(리베이트 예상 수익 계산)은 향후 심화 문서로 추가 예정.

## 영향

- 리베이트는 마켓 메이킹을 장려하여 스프레드를 줄이고 거래 비용을 낮춘다.
- Copytrade 관점에서 높은 Maker 활동을 보이는 트레이더의 전략은 유동성 제공 성향을 반영할 수 있다.

## 관련 문서

- [[Polymarket 개요]]
- [[API-레퍼런스]]
- [[CLOB]]


<!-- MERGED from 개념/개념-CTF.md -->

# CTF 개념

> CTF(Conditional/Collateralized Trading Framework 등 가정)를 간단히 설명

## 내용

CTF 관련 용어와 Copytrade에서의 의의, 리스크를 정리한다. 키워드: CTF 조건부 거래 담보 프레임워크 리스크 헤지 청산 규칙

## 관련 문서

- [[Copytrade-전략분석]] — CTF가 전략에 미치는 영향
