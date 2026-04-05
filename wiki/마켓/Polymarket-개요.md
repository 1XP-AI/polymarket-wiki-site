---
title: "Polymarket 개요"
category: "market"
created: "2026-04-05"
source: "raw/01-Polymarket-개요.md"
related:
  - "[[API 레퍼런스]]"
  - "[[리더보드-데이터]]"
  - "[[Copytrade 전략분석]]"
---

# Polymarket 개요

> 한 줄 요약: Polymarket은 예측 시장 플랫폼으로, 사용자가 이벤트 결과에 베팅하여 가격(확률)을 형성한다.

## 내용

이 문서는 Polymarket 플랫폼의 구조와 주요 기능을 요약한다. Polymarket은 주문장부(central limit order book, CLOB)와 마켓 메이커 구조를 사용하며, 오픈 API를 통해 마켓 목록, 이벤트, 포지션 정보를 제공한다. 리더보드와 복사거래(copytrade) 기능은 트레이더 행동 분석과 전략 수립에 중요한 데이터를 제공한다. 본 문서는 copytrade 전략의 맥락에서 플랫폼의 핵심 메커니즘(거래 흐름, 수수료, 리더보드 기반 인센티브)을 설명한다.

### 주요 구성 요소

- 마켓 타입: binary(Yes/No), categorical 등
- 가격 형성: 주문장(CLOB) 기반 매칭 또는 자동화된 마켓메이커
- 유동성: 리베이트/보상 프로그램이 유동성 제공자 행동에 영향
- 데이터 접근: REST API 및 WebSocket을 통한 실시간/배치 데이터 제공

### 예제: 간단한 API 호출

다음은 현재 활성 이벤트 목록을 가져오는 예제입니다:

```bash
curl -s "https://gamma-api.polymarket.com/events?limit=20&active=true"
```

- 실무 팁: rate limit을 고려해 적절한 캐시와 백오프를 적용하세요.

### 플랫폼이 Copytrade에 주는 시사점

- 리더보드 기반 팔로우는 트레이더의 보상 구조(예: 리베이트)와 빈번한 리밸런싱에 민감합니다.
- 주문장 유동성이 낮으면 슬리피지와 실행비용이 커져 팔로우 전략의 수익성이 떨어질 수 있습니다.
- WebSocket으로 실시간 포지션 변화를 감시하면 추적 지연을 줄일 수 있습니다.

## 관련 문서

- [[API 레퍼런스]] — Polymarket API와 연계된 기술 문서
- [[리더보드-데이터]] — 트레이더 스냅샷과 리더보드 데이터 소스
- [[Copytrade 전략분석]] — 따라하기 전략의 개요와 리스크 분석
- [[CLOB]] — 주문장(central limit order book) 개념

## 참조

[^1]: raw/01-Polymarket-개요.md — 원본 시드 문서
[^2]: raw/fetched/2026-04-05-polymarket-markets.md — 마켓 스냅샷
