---
title: "Copytrade 성능 및 모니터링"
category: "strategy"
created: "2026-04-05"
source: "generated: cycle-0017"
sources:
  - url: "https://data.polymarket.com/leaderboard"
    added: "2026-04-07"
  - url: "https://docs.polymarket.com/api"
    added: "2026-04-07"
related:
  - "[[전략/Copytrade/리스크-관리]]"
  - "[[전략/Copytrade/포지션-사이즈-전략]]"
  - "[[알파-지표-선별]]"
---

# Copytrade 성능 및 모니터링

> Copytrade 포트폴리오와 팔로우 전략의 실시간/주기적 성능 지표를 정의하고 모니터링하는 방법론.

## 내용

이 문서는 Copytrade(팔로우 트레이딩) 실행에서 성능을 계측하고 모니터링하는 실무 항목을 정리한다. 목표는 팔로우 대상(트레이더) 선택과 리스크 관리가 실제 수익으로 이어지는지 판정할 수 있도록 지표와 경보를 설계하는 것이다.

주요 지표:

- 누적수익률(Cumulative Return): 특정 기간 동안의 복리 수익률
- 일별 수익(Profit per day): 변동성이 큰 마켓에서의 단기 성능 관찰
- 승률(Win rate): 체결된 베팅 중 수익을 낸 비율
- 평균베팅기간(Average holding time): 진입-청산 패턴 파악
- 최대손실(Max Drawdown): 리스크 한계 설정
- 샤프지수(Sharpe ratio): 위험조정수익성 평가
- 오더북 임팩트(Estimated market impact): 거래 규모에 따른 가격 영향 추정

모니터링 주기 및 경보:

- 실시간(초-분) 모니터링: 빠른 증감이 있는 마켓에서 WebSocket을 통해 가격·포지션 변화를 수집한다. 관련 문서: [[기술/WebSocket-실시간데이터]], [[기술/API/Polymarket-API-레퍼런스]].
- 일간 리포트: 일별 집계로 성능 추세, 승률, 평균 베팅기간을 검토.
- 임계치 기반 경보: 최대손실 초과, 승률 급락, 특정 트레이더의 포지션 집중 발생 시 알림 발송.

간단한 예시(의사코드):

- 매 시각: Polymarket API에서 팔로우한 트레이더의 포지션 스냅샷 수집
- 집계: 포지션별 P&L 계산 → 포트폴리오 누적 수익 업데이트
- 경보: Max Drawdown > threshold → 포지션 자동 축소 또는 팔로우 중단

## 적용 사례

- [[전략/Copytrade/리스크-관리]]의 리스크 한도와 연동하여 자동 리밸런싱 규칙을 설계한다.
- [[알파-지표-선별]]에서 제시한 신호들을 모니터링 지표로 채택해 백테스트와 실거래 모니터링을 병행한다.

## 관련 문서

- [[전략/Copytrade/리스크-관리]] — 리스크 한도, 헤징 기법
- [[전략/Copytrade/포지션-사이즈-전략]] — 포지션 사이즈 및 진입/청산 규칙
- [[알파-지표-선별]] — 트레이더 선별용 지표 세트
