---
id: legacy_wiki_copytrade_bb61e6
title: 심리적 편향(Behavioral Bias) 분석
type: concept
status: draft
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-09T14:10:11Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_copytrade_md_bb61e608
tags:
- concept
- internal
---

# 심리적 편향(Behavioral Bias) 분석

## 요약

<!-- para: para_001 -->
> Copytrade 전략 관점에서 트레이더의 반복적 오차를 식별하고 리스크(또는 알파)를 관리하기 위한 분석 가이드

## 핵심 사실

<!-- para: para_002 -->
본 문서는 Polymarket에서 활동하는 트레이더들, 특히 리더보드 상위 트레이더를 대상으로 관찰되는 주요 심리적 편향(behavioral biases)을 정리하고, 이를 Copytrade 전략에 어떻게 적용하거나 방어할지 설명합니다. 트레이더의 반복적 행동은 따라하기(복사) 전략에 유리한 신호가 될 수 있지만, 동일한 편향이 누적되면 시스템적 리스크로 연결됩니다.

<!-- para: para_003 -->
- **확증 편향(Confirmation Bias)**: 트레이더가 초기 가설을 지지하는 정보만 과대평가하는 경향. 장기적으론 포지션 편향을 초래.

## 세부 내용

<!-- para: para_004 -->
폴리마켓의 온체인 데이터는 트레이더의 편향을 객관적으로 탐지하는 데 활용될 수 있다. - **손실회피 탐지**: 포지션이 손실 영역으로 진입한 후, 마감 24시간 전까지 청산하지 않은 비율이 60% 이상이면 손실회피 신호. 반면 수익 포지션은 평균 48시간 이내에 청산하는 패턴이 관찰되면 "손실은 붙잡고 수익은 일찍 자른다"는 전형적 편향.

<!-- para: para_005 -->
1. 편향 프로파일링: 트레이더의 과거 포지션과 포지션 회전율, 평균 보유기간을 분석하여 편향 지표를 만듭니다. (예: 평균 보유기간이 비정상적으로 길면 손실회피 가능성)
2.

<!-- para: para_006 -->
- 예시 지표: 평균 포지션 지속시간, 포지션 사이즈 분포, 최근 10건의 승률 편차, 평균 손절 시점(설정 대비 실제)
- 활용 예: Theo 트레이더 프로필과 교차분석하여 Theo의 포지션 지속시간이 짧고 빠른 스캘핑 성향이면, 레버리지 노출을 줄이는 규칙 적용
- 편향 점수 시스템: 각 편향 유형에 0~10 점수를 부여. 총 편향 점수 25+인 트레이더는 팔로우 제한 또는 사이징 50% 감액 적용. [[전략/Copytrade/팔로우-스코어링-모델]]과 연동 가능.

<!-- para: para_007 -->
- [[전략/Copytrade/자동화-플로우]] — 전략 전반과의 연계
- [[전략/Copytrade/팔로우-선별]] — 팔로우 대상 선정 기준
- [[전략/Copytrade/리스크-관리]] — 편향 기반 리스크 완화 기법
- [[전략/Copytrade/팔로우-스코어링-모델]] — 편향 점수를 통합한 트레이더 평가 모델

## 열린 질문

<!-- para: para_008 -->
Pending review.

## 관련 페이지

<!-- para: para_009 -->
소스 요약: source_summary_src_wiki_copytrade_md_bb61e608
