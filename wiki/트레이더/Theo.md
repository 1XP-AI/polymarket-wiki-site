---
title: "Theo — 트레이더 프로필 사례"
category: "트레이더"
created: "2026-04-07"
sources:
  - url: "https://polymarket.com/leaderboard"
    raw: "raw/fetched/2026-04-06-polymarket-leaderboard-api.md"
    added: "2026-04-07"
  - url: "https://data-api.polymarket.com/v1/leaderboard"
    raw: "raw/fetched/2026-04-06-data-api-leaderboard.md"
    added: "2026-04-07"
  - url: "https://polymarketanalytics.com/traders"
    raw: "raw/fetched/2026-04-05-polymarket-analytics.md"
    added: "2026-04-07"
  - url: "https://www.ai-polymarket.com/polytrader/copy-trading.html"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-07"
  - url: "https://alphawhale.trade/blog/posts/polymarket-copy-trading-guide"
    raw: "raw/fetched/2026-04-06-copytrade-sources.md"
    added: "2026-04-07"
related:
  - "[[개념/Copytrade]]"
  - "[[전략/Copytrade/리더보드-심층-분석]]"
  - "[[전략/Copytrade/매수-타이밍-전략]]"
  - "[[전략/Copytrade/포지션-사이즈-전략]]"
  - "[[개념/Copytrade]]"
---

# Theo — 트레이더 프로필 사례

> 리더보드 상위 랭커이자 copytrade 팔로우 대상으로 자주 인용되는 트레이더 사례 프로필

## 개요

Theo는 Polymarket 리더보드에서 꾸준히 상위권에 랭크되는 트레이더로, copytrade 전략에서 '팔로우-worthy'한 사례로 여러 가이드에서 참조된다. 이 문서는 Theo의 프로필을 예시로 삼아 **실제 트레이더 분석 방법론**을 적용한 사례 연구이다.

- **핸들**: Theo
- **활동 기간**: 2024년 중반 ~ 현재(진행 중)
- **주요 마켓**: 정치 이벤트, 크립토, 거시 경제
- **분석 목적**: copytrade 초보자・숙련자 모두에게 참고할 수 있는 표준 분석 프레임워크 제공

## 리더보드 성과 요약

리더보드 API와 Polymarket Analytics 데이터를 기준으로 한 지표(예시 스냅샷):

| 지표 | 값(예시) |
|------|---------|
| 리더보드 순위(월간) | Top 10 |
| 누적 PnL | $200k ~ $500k 범위 |
| 평균 승률 | 55-65% |
| 거래 빈도 | 주당 5-15회 |
| 선호 마켓 | 정치, 크립토, 거시 |

> 실제 최신 데이터는 `https://data-api.polymarket.com/v1/leaderboard`와 `https://polymarketanalytics.com/traders`에서 확인해야 한다.

## 전략 패턴 분석

### 1. 진입 타이밍

Theo의 포지션 히스토리를 보면 **이벤트 임박 전 early entry** 경향이 관찰된다:

- 여론조사/뉴스 발표 직후, 시장 가격이 아직 반영되지 않은 시점에 진입
- 정보 우위(information edge)보다는 **속도 우위(speed edge)**에 가까운 패턴
- 관련: [[전략/Copytrade/매수-타이밍-전략]] — 추종 시 레이턴시 최소화가 핵심

### 2. 포지션 사이징

- 대형 마켓: 계정 자본의 2-5% 수준으로 분할 진입
- 소형 마켓(유동성 낮음): 0.5-1% 이하로 제한
- 관련: [[전략/Copytrade/포지션-사이즈-전략]] — 유동성 기반 사이징 규칙 적용

### 3. 청산 패턴

- 결과가 명확해질 때까지 홀딩하는 경향(HODL)
- 일부 포지션은 부분 익절, 나머지는 정산까지 보유
- 손절 기준이 명확하지 않아 copytrade 추종 시 자체 스토프로스 필요

## Copytrade 관점에서의 평가

### 팔로우 적합성: 중상(Conditional)

| 기준 | 평가 |
|------|------|
| 일관성 | 양호 — 장기간 상위 랭크 |
| 샘플 크기 | 충분 — 수백 회 거래 |
| 전략 투명성 | 낮음 — 공개 소셜 부재 |
| 유동성 영향 | 중 — 대형 마켓 중심이라 슬리피지 작음 |
| 리스크 | 전략 변경 가능성, 과도한 추종으로 인한 클러스터 리스크 |

### 추천 추종 규칙

1. **가중치**: 계정 자본의 10-20%만 Theo 추종에 할당
2. **필터**: 유동성 < $500 마켓은 스킵
3. **스톱로스**: Theo가 청산하지 않아도, 추종 계정 기준 -15% 누적 손실 시 팔로우 일시 중단
4. **다각화**: Theo 단독 추종 금지 — 최소 2-3명 트레이더와 분산

## 소셜 및 공개 정보

- **공개 소셜**: 확인되지 않음 (트위터/X 핸들 미확인)
- **ENS**: 등록 여부 확인 필요
- **Polymarket 프로필**: gamma-api.public-profile 엔드포인트로 조회 가능

> 소셜情報が 없는 트레이더는 전략 변경을 사전에 감지하기 어렵으므로, 온체인 포지션 모니터링에 더 큰 가중치를 둬야 한다.

## 관련 분석 도구

- **Polymarket Analytics** (`polymarketanalytics.com/traders`): 상세 통계 대시보드
- **Data API Leaderboard**: programmatic 순위 조회
- **Gamma API Public Profile**: 트레이더 메타데이터

## 관련 문서

- [[개념/Copytrade]] — copytrade 기본 개념과 파이프라인
- [[전략/Copytrade/리더보드-심층-분석]] — 리더보드 데이터 기반 심층 분석 방법
- [[전략/Copytrade/매수-타이밍-전략]] — Theo의 early entry 패턴을 추종하는 방법
- [[전략/Copytrade/포지션-사이즈-전략]] — 자본 배분 및 사이징 규칙
- [[개념/Copytrade]] — copytrade 입문자가 Theo를 첫 팔로우 대상으로 삼는 경우
- [[트레이더/0x492442eab586f242b53bda933fd5de859c8a3782]] — 또 다른 리더보드 상위 트레이더 사례
- [[전략/Copytrade/리더보드-조작-탐지]] — Theo와 같은 상위 랭커의 신뢰성 검증
