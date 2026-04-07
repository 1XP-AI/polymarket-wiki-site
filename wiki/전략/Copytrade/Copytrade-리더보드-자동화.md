---
title: "Copytrade-리더보드-자동화"
category: "strategy"
created: "2026-04-05"
source: "generated/auto"
sources:
  - https://polymarket.com/leaderboard?period=monthly
  - https://data.polymarket.com/leaderboard
  - https://gamma-api.polymarket.com/markets
  - https://docs.polymarket.com/api
related:
  - "[[전략/Copytrade/Copytrade-리더보드-심화]]"
  - "[[전략/Copytrade/팔로우-선별]]"
  - "[[전략/Copytrade/자동화-플로우]]"
---

# Copytrade-리더보드-자동화

> 리더보드 기반 트레이더 선별과 자동화 파이프라인 설계 가이드

## 내용

이 문서는 Polymarket 리더보드 데이터를 이용해 copytrade 후보를 자동으로 선별하고, 자동화된 워크플로우로 후보를 검증하는 방법을 설명한다. 목표는 리더보드에서 식별된 트레이더를 정량적/정성적으로 평가해 팔로우 가치가 높은 대상만 추출하는 파이프라인을 구축하는 것이다.

핵심 단계:
1. 데이터 수집: 리더보드 API로 상위 트레이더 목록과 포지션 스냅샷을 정기 수집한다. (raw/fetched/에 저장)
2. 정량 지표 산출: 승률, ROI 추정, 평균 포지션 홀딩 기간, 베팅 빈도, 슬리피지 영향 등 지표를 계산한다.
3. 정성 필터: 트레이더의 소셜 존재감(트윗 빈도, 전략 공개 여부), 과거 큰 변동시의 행동 일관성 등을 평가한다.
4. 리스크 평가: 포트폴리오로 팔로우할 때 발생할 최대 드로우다운(시뮬레이션), 평균 손실폭, 상관관계 등을 측정한다.
5. 후보 점수화 & 컷오프: 지표에 가중치를 두어 점수를 합산하고 임계값을 적용해 후보를 최종 선별한다.
6. 자동화 워크플로우: 새 트레이더 발견 → 프로필 생성([[트레이더/새로운-트레이더/프로필-템플릿]]) → 백테스트 태스크 예약 → 결과에 따라 팔로우 권고 또는 보류.

## 체크리스트 (간단)
- [ ] raw/sources.md에 리더보드 API 엔드포인트 등록
- [ ] 수집 스크립트로 daily snapshot 자동 저장
- [ ] 정량 지표 계산 스크립트(승률, ROI, freq) 작성
- [ ] 소셜 스크레이핑 결과를 정성 지표로 통합
- [ ] 데시보드/알림: 새 후보 발생 시 알림 발송

## 관련 문서
- [[전략/Copytrade/Copytrade-리더보드-심화]] — 심층 분석 방법과 지표 정의
- [[전략/Copytrade/팔로우-선별]] — 팔로우 가치 평가의 정책적 가이드
- [[전략/Copytrade/자동화-플로우]] — Copytrade 자동화 설계 (sim 0.7403)


---
작성일: 2026-04-05
