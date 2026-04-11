---
id: legacy_wiki_copytrade_bb61e6
title: 심리적 편향(Behavioral Bias) 분석
type: concept
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-11T11:43:38Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 4
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://aitoolsbee.com/ko/news/ai-%ED%8E%B8%ED%96%A5-%EA%B0%90%EC%82%AC-2026%EB%85%84-%EA%B8%B0%EC%97%85-%EA%B3%A0%EC%9A%A9-%EC%9D%98%EC%82%AC%EA%B2%B0%EC%A0%95%EC%9D%98-%ED%95%B5%EC%8B%AC-%EA%B3%BC%EC%A0%9C/
- url: https://developers.google.com/machine-learning/crash-course/fairness/types-of-bias?hl=ko
- url: https://psychology-money.com/111
- url: https://newllmskll.com/entry/%ED%99%95%EC%A6%9D%ED%8E%B8%ED%96%A5%EA%B3%BC-%EC%84%A0%ED%83%9D%EB%85%B8%EC%B6%9C-%EC%8B%AC%EB%A6%AC-%EC%8B%A4%ED%97%98-%EB%B9%84%EA%B5%90-%EC%9D%B8%EC%A7%80%ED%8E%B8%ED%96%A5-%EC%8B%A4%ED%97%98%EB%B6%84%EC%84%9D-%EC%9D%B4%EB%A1%A0%EC%A0%95%EB%A6%AC
cluster: Copytrade
doc_role: analysis
---
# 심리적 편향(Behavioral Bias) 분석

## 요약

<!-- para: para_001 -->
> Copytrade 전략 관점에서 트레이더의 반복적 오차를 식별하고 리스크(또는 알파)를 관리하기 위한 분석 가이드

<!-- para: para_002 -->
본 문서는 Polymarket에서 활동하는 트레이더들, 특히 리더보드 상위 트레이더를 대상으로 관찰되는 주요 심리적 편향(behavioral biases)을 정리하고, 이를 Copytrade 전략에 어떻게 적용하거나 방어할지 설명합니다. 트레이더의 반복적 행동은 따라하기(복사) 전략에 유리한 신호가 될 수 있지만, 동일한 편향이 누적되면 시스템적 리스크로 연결됩니다.

<!-- para: para_003 -->
- **확증 편향(Confirmation Bias)**: 트레이더가 초기 가설을 지지하는 정보만 과대평가하는 경향. 장기적으론 포지션 편향을 초래.

<!-- para: para_004 -->
폴리마켓의 온체인 데이터는 트레이더의 편향을 객관적으로 탐지하는 데 활용될 수 있다. - **손실회피 탐지**: 포지션이 손실 영역으로 진입한 후, 마감 24시간 전까지 청산하지 않은 비율이 60% 이상이면 손실회피 신호. 반면 수익 포지션은 평균 48시간 이내에 청산하는 패턴이 관찰되면 "손실은 붙잡고 수익은 일찍 자른다"는 전형적 편향.

<!-- para: para_005 -->
1. 편향 프로파일링: 트레이더의 과거 포지션과 포지션 회전율, 평균 보유기간을 분석하여 편향 지표를 만듭니다. (예: 평균 보유기간이 비정상적으로 길면 손실회피 가능성)

<!-- para: para_006 -->
- 예시 지표: 평균 포지션 지속시간, 포지션 사이즈 분포, 최근 10건의 승률 편차, 평균 손절 시점(설정 대비 실제)
- 활용 예: Theo 트레이더 프로필과 교차분석하여 Theo의 포지션 지속시간이 짧고 빠른 스캘핑 성향이면, 레버리지 노출을 줄이는 규칙 적용
- 편향 점수 시스템: 각 편향 유형에 0~10 점수를 부여. 총 편향 점수 25+인 트레이더는 팔로우 제한 또는 사이징 50% 감액 적용. [[Copytrade 데이터 수집 가이드]]과 연동 가능.

<!-- para: para_007 -->
- [[Copytrade 데이터 수집 가이드]] — 전략 전반과의 연계
- [[Copytrade 데이터 수집 가이드]] — 팔로우 대상 선정 기준
- [[Copytrade 데이터 수집 가이드]] — 편향 기반 리스크 완화 기법
- [[Copytrade 데이터 수집 가이드]] — 편향 점수를 통합한 트레이더 평가 모델

## 세부 내용

<!-- para: para_008 -->
행동편향의 심리학 - 왜 우리는 비합리적인 선택을 할까? 본문 바로가기

행동편향의 심리학 - 왜 우리는 비합리적인 선택을 할까?

<!-- para: para_009 -->
공정성: 편향의 유형

|Machine Learning | Google for Developers

ML 입문을 위한 교육 과정

<!-- para: para_010 -->
확증편향과 선택노출 심리 실험 비교 (인지편향, 실험분석, 이론정리)

<!-- para: para_011 -->
AI 편향 감사, 2026년 기업 고용 의사결정의 핵심 과제 - AI툴즈비

AI 편향 감사, 2026년 기업 고용 의사결정의 핵심 과제

Fisher Phillips는 2026년 채용과 평가, 리스크 예측에서 알고리즘 차별 위험 대응을 촉구했다.
