---
id: legacy_raw_03_copytrade_c17abe
title: Polymarket Copytrade 전략 분석
type: concept
status: verified
created_at: '2026-04-09T14:10:08Z'
last_updated: 2026-04-18T16:05:00Z
as_of: 2026-04-18
owners:
- wiki-system
source_count: 3
sources:
- url: file://raw/03-Copytrade-전략분석.md
- url: file://raw/internal/src_raw_03_copytrade_md_c17abe9e/content.md
- url: https://docs.polymarket.com/trading/orders/create
evidence_coverage: 1.0
confidence: medium
tags:
- concept
cluster: Copytrade
doc_role: analysis
cluster_group: 실행
---

## 요약

> Polymarket Copytrade 전략 분석은 리더보드 선별부터 주문 실행과 포지션 관리까지 전체 추종 파이프라인을 분석하는 문서다.

이 문서는 단일 주문 타입 설명보다, 상위 트레이더 탐지와 실제 추종 실행 사이를 어떻게 연결할지에 초점을 둔다.
핵심은 데이터 수집, 신호 판정, 주문 생성, 사후 포지션 관리가 하나의 운영 루프로 맞물려 있다는 점이다.

## 핵심 주장

- Copytrade 파이프라인은 먼저 리더보드에서 상위 트레이더를 선별하고, 그들의 포지션과 활동을 지속적으로 모니터링하는 단계부터 시작한다.
- 새로운 거래가 감지되면 동일 마켓과 동일 방향으로 추종 주문을 생성하고, 이후 익절·손절·청산까지 포함해 포지션 관리를 이어간다.
- 실행 레이어에서는 시장가 주문과 maker 주문의 비용 차이, 체결 지연, 슬리피지를 함께 고려해야 한다.
- FOK와 FAK 같은 주문 타입 규칙은 추종 신호를 실제 체결로 바꿀 때 부분 체결과 체결 실패를 어떻게 다룰지 결정하는 핵심 제약이다.
- 전략 분석의 목적은 단일 API 엔드포인트 나열이 아니라, 신호 탐지와 주문 실행 사이의 latency·비용·리스크를 정량화하는 데 있다.

## 관련 엔티티

- `workflow`: Copytrade 실행
- `risk`: latency
- `risk`: slippage

## 참고 근거

- file://raw/03-Copytrade-전략분석.md
- file://raw/internal/src_raw_03_copytrade_md_c17abe9e/content.md
- https://docs.polymarket.com/trading/orders/create

## 관련 문서

[[Copytrade 실행]], [[Copytrade 데이터 수집 가이드]], [[Copytrade 자동화 플로우]], [[Copytrade 포지션 리밸런싱 가이드]], [[추종 신호 필터링]], [[추종 실행 속도 최적화]]
