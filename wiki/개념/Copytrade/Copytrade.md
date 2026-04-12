---
id: legacy_wiki_copytrade_4d0fc3
title: Copytrade
type: concept
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-12T06:13:48Z'
as_of: '2026-04-10'
owners:
- wiki-system
source_count: 2
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_00_index_ec3366
- legacy_raw_03_copytrade_c17abe
- legacy_raw_05_badd78
- legacy_raw_fetched_2026_04_05_fetch_polymarket_f95e6d
- legacy_raw_fetched_2026_04_05_leaderboard_monthly_43010c
- legacy_raw_fetched_2026_04_06_copytrade_sources_5404e6
- legacy_wiki_0x492442eab586f242b53bda933fd5de859c8a3782_e83e3b
- legacy_wiki_104389
- legacy_wiki_4526f6
- legacy_wiki_88f80c
- legacy_wiki_96e938
- legacy_wiki_copytrade_01e411
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_1f98b0
- legacy_wiki_copytrade_27d56b
- legacy_wiki_copytrade_2ce18d
- legacy_wiki_copytrade_37aa3c
- legacy_wiki_copytrade_506e4c
- legacy_wiki_copytrade_511614
- legacy_wiki_copytrade_59552d
- legacy_wiki_copytrade_698574
- legacy_wiki_copytrade_ac0967
- legacy_wiki_copytrade_bb99a4
- legacy_wiki_copytrade_bde177
- legacy_wiki_copytrade_bf1303
- legacy_wiki_copytrade_bfb3cf
- legacy_wiki_copytrade_c6dea0
- legacy_wiki_copytrade_copytrade_4b2b9f
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_d6deb5
- legacy_wiki_copytrade_e140b9
- legacy_wiki_copytrade_e2e01c
- legacy_wiki_copytrade_e81931
- legacy_wiki_copytrade_eff435
- legacy_wiki_index_925404
- legacy_wiki_polymarket_2026_04_05_d5da53
- legacy_wiki_theo_e3e7fe
tags:
- concept
sources:
- url: https://www.copytrade.net/
- url: https://github.com/warproxxx/poly_data
cluster: Copytrade
doc_role: hub
---
## 요약

<!-- para: para_001 -->
> Polymarket에서 상위 트레이더의 포지션과 체결 패턴을 관찰해 추종 전략으로 전환하는 방법을 정리한 허브 문서

<!-- para: para_002 -->
Copytrade는 리더보드 탐색, 트레이더 프로필 해석, 포지션 재현, 리스크 차단, 운영 자동화를 하나의 루프로 묶는 전략이다. 이 허브는 하위 문서를 역할별로 정리해 어디서부터 읽어야 하는지 안내한다.

<!-- para: para_003 -->
처음 읽는 경우에는 리더보드 데이터와 프로필 분석부터 보고, 실제 운영이 목적이면 자동화 플로우와 리스크 관리 문서를 이어서 읽는 편이 좋다.

## 문서 지도

<!-- para: para_004 -->
이 문서군은 `리더보드`, `프로필`, `실행`, `리스크`, `자료` 다섯 그룹으로 나뉜다. 각 그룹은 같은 주제를 반복하는 대신 역할이 다른 문서를 묶어 탐색성을 높이는 것을 목표로 한다.

## 리더보드/트레이더 탐색

<!-- para: para_005 -->
리더보드/트레이더 탐색 문서군: [[Copytrade 리더보드 심화]], [[Copytrade 알파 지표 선별]], [[데이터 기반 트레이더 선별]], [[리더보드 & 트레이더 데이터]], [[리더보드 데이터]], [[리더보드 분석]], [[리더보드 알파 탐지]], [[리더보드 조작 탐지]]

<!-- para: para_006 -->
리더보드 문서군은 후보 발굴과 스코어링에 집중한다. 순위표 자체보다 어떤 거래 습관이 순위를 만들었는지를 읽는 단계다.

## 프로필 분석

<!-- para: para_007 -->
프로필 분석 문서군: [[0x492442eab586f242b53bda933fd5de859c8a3782 트레이더 프로필]], [[Theo — 트레이더 프로필 사례]], [[트레이더 프로필 분석]], [[트레이더 프로필 템플릿]]

<!-- para: para_008 -->
프로필 문서군은 개별 트레이더를 팔로우 대상으로 평가하는 데 초점을 둔다. 템플릿, 사례, 평가 기준이 함께 연결되어야 의미가 있다.

<!-- para: para_009 -->
평가 기준: 트레이더 프로필 분석 / 템플릿: 트레이더 프로필 템플릿 / 사례: 0x492442eab586f242b53bda933fd5de859c8a3782 트레이더 프로필, Theo — 트레이더 프로필 사례

## 실행/운영

<!-- para: para_010 -->
실행/운영 문서군: [[Copytrade 데이터 수집 가이드]], [[Copytrade 자동화 플로우]], [[Copytrade 포지션 리밸런싱 가이드]], [[Polymarket Copytrade 전략 분석]], [[데이터 수집 파이프라인]], [[실행 비용(Execution Cost) — Copytrade 고려사항]], [[추종 신호 필터링]], [[추종 실행 속도 최적화]], [[추종 중단 규칙]], [[팔로우 선별]], [[팔로우 스코어링 모델]]

<!-- para: para_011 -->
실행 문서군은 데이터 수집, 신호 필터링, 자동화, 리밸런싱처럼 실제 포지션 반영 로직을 다룬다.

<!-- para: para_012 -->
실행 가이드: Copytrade 데이터 수집 가이드, Copytrade 자동화 플로우, Copytrade 포지션 리밸런싱 가이드, 추종 신호 필터링, 추종 실행 속도 최적화, 추종 중단 규칙, 팔로우 선별, 팔로우 스코어링 모델

## 리스크 관리

<!-- para: para_013 -->
리스크 관리 문서군: [[Copytrade 리스크 관리]], [[Copytrade 성능 모니터링]], [[딜레이(지연) 분석 및 슬리피지 대응]], [[리스크 모니터링(Copytrade)]], [[리스크 시나리오]], [[리스크 알림 규칙]], [[성과 분석 지표 (Copytrade 성능 메트릭)]]

<!-- para: para_014 -->
리스크 문서군은 손실 한도, 모니터링, 비용, 중단 규칙처럼 전략을 멈추거나 축소하는 기준을 모은다.

## 시점성 문서와 자료

<!-- para: para_015 -->
시점성 문서와 자료 문서군: [[2026-04-06 Copytrade 외부 소스 수집]], [[Copytrade 링크 강화]], [[Polymarket Copytrade 위키 — Raw 자료 인덱스]], [[Polymarket 리더보드 스냅샷 (2026-04-05 01:00)]], [[Polymarket 이벤트 스냅샷 (2026-04-05)]], [[수집 원본: Polymarket snapshot — 2026-04-05]]

<!-- para: para_016 -->
이 그룹은 스냅샷, 외부 소스 수집, raw 인덱스처럼 참고용 자료를 보관한다. 개념 설명보다 근거 확인과 시점 추적에 가깝기 때문에 핵심 설명 문서와 분리해서 읽는 편이 낫다.

## 탐색 경로

<!-- para: para_017 -->
입문자는 `리더보드 데이터 -> 트레이더 프로필 분석 -> Copytrade 자동화 플로우 -> Copytrade 리스크 관리` 순서로 읽는 편이 무난하다.

<!-- para: para_018 -->
운영 점검 목적이라면 `Copytrade 포지션 리밸런싱 가이드 -> 추종 중단 규칙 -> 리스크 모니터링(Copytrade)` 순서가 더 실무적이다.

## 열린 질문

- Copytrade 문서군을 실제 운영 관점에서 연결할 때 빠진 절차나 제약은 무엇인가?
- Copytrade에서 아직 근거가 약한 핵심 운영 판단 기준은 무엇인가?

## 세부 내용

<!-- para: para_019 -->
trader_df
