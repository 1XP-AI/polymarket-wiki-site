---
id: legacy_wiki_copytrade_59552d
title: Copytrade 리스크 관리
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-10T15:39:11Z'
as_of: '2026-04-10'
owners:
- wiki-system
source_count: 2
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_copytrade
- legacy_raw_03_copytrade_c17abe
- legacy_wiki_copytrade_01e411
- legacy_wiki_copytrade_1f98b0
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_506e4c
- legacy_wiki_copytrade_c6dea0
- legacy_wiki_copytrade_e81931
tags:
- concept
sources:
- url: https://copytrade.co.kr/
- url: https://help.polymarket.com/en/articles/13364163-geographic-restrictions
cluster: Copytrade
cluster_group: 리스크
doc_role: analysis
---
# Copytrade 리스크 관리

## 요약

<!-- para: para_001 -->
> Copytrade에서 가장 자주 발생하는 손실 요인과, 추종 전략을 멈추거나 축소해야 하는 기준을 정리한 문서

<!-- para: para_002 -->
Copytrade의 핵심 리스크는 "원 트레이더가 틀릴 수 있다"는 단순한 문제보다, 같은 전략을 내가 같은 조건으로 재현할 수 없다는 데 있다. 진입 시점 차이, 시장 유동성, 비중 차이, 추종 지연이 겹치면 원본 전략과 전혀 다른 손익 곡선이 만들어진다.

## 주요 리스크

<!-- para: para_003 -->
첫 번째는 추종 대상 리스크다. 리더보드 상위권이라도 특정 이벤트에 과도하게 집중하거나, 공개 정보로 설명하기 어려운 대형 포지션을 자주 잡는 계정은 장기 팔로우 대상으로 부적합할 수 있다.

<!-- para: para_004 -->
두 번째는 실행 리스크다. 원 트레이더가 들어간 가격과 내가 따라가는 가격이 다르면 같은 방향을 잡아도 기대 수익이 크게 줄어든다. 특히 유동성이 얕은 마켓에서는 체결 속도보다 슬리피지 관리가 더 중요하다.

<!-- para: para_005 -->
세 번째는 사이징 리스크다. 리더의 포지션 규모를 그대로 복제할 수 없고, 계정 크기가 다르면 손실 허용 한도도 다르다. 따라서 copytrade는 언제나 "비중 축소 규칙"이 전제되어야 한다.

<!-- para: para_006 -->
네 번째는 운영 리스크다. API 장애, 지연된 체결, 데이터 누락, 잘못된 시그널 해석이 반복되면 전략 자체가 아니라 운영 계층에서 손실이 발생한다.

## 운영 규칙

<!-- para: para_007 -->
실무 규칙은 보통 네 가지로 묶는다. 단일 트레이더 최대 노출 상한, 단일 이벤트군 최대 노출 상한, 허용 슬리피지 한도, 일정 손실 이상에서의 추종 중단이다.

<!-- para: para_008 -->
예를 들어 "단일 트레이더 15% 초과 금지", "단일 이벤트군 20% 초과 금지", "예상 슬리피지 1% 초과 시 사이즈 축소", "7일 누적 손실 -5% 이하 시 추종 중지" 같은 규칙은 단순하지만 효과적이다.

## 제도와 접근 제한

<!-- para: para_009 -->
Polymarket 사용 가능 여부는 지역 제한과 규제 상태의 영향을 받는다. 따라서 copytrade 운영자는 전략 성과뿐 아니라 플랫폼 접근 가능 지역, 계정 제한, 거래 가능 상태를 함께 확인해야 한다. 이 문서는 세부 국가 목록을 나열하기보다, "접근 제한이 운영 리스크"라는 점을 기억하기 위한 가이드로 보는 편이 좋다.

## 관련 문서
