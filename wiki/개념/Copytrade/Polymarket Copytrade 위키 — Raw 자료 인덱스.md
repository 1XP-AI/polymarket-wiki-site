---
id: legacy_raw_00_index_ec3366
title: Polymarket Copytrade 위키 — Raw 자료 인덱스
type: concept
status: verified
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-10T03:10:00Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 4
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_05_badd78
- legacy_raw_06_websocket_506430
- legacy_raw_07_48e6ec
- legacy_raw_fetched_2026_04_05_polymarket_markets_a295cb
- legacy_wiki_7acc18
- legacy_wiki_api_polymarket_api_62ef40
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_eff435
- legacy_wiki_polymarket_cd5a08
tags:
- concept
sources:
- url: https://www.polycopytrade.net/documentation.php
- url: https://github.com/jhcdx9999/polymarket-copy-trade
- url: https://deepwiki.com/jhcdx9999/polymarket-copy-trade
- url: https://docs.polymarket.com/
---
# Polymarket Copytrade 위키 — Raw 자료 인덱스

## 요약

<!-- para: para_001 -->
이 문서는 Copytrade 관련 raw 자료를 어떤 축으로 수집했고, 각 자료가 현재 위키의 어떤 문서 묶음으로 이어졌는지 정리한 인덱스다. 원문 덤프 자체를 나열하기보다, 어떤 자료가 설계 문서이고 어떤 자료가 실행 가이드인지 구분해 보여주는 용도로 사용한다.

## 수집 범위

<!-- para: para_002 -->
- **공식 문서 축**: Polymarket Docs의 개요, API, WebSocket, 마켓 구조 문서
- **구현 사례 축**: GitHub 공개 저장소와 DeepWiki 요약을 통한 봇 구조 파악
- **운영 가이드 축**: Copytrade 서비스 문서와 설정 가이드를 통한 사용자 플로우 확인

<!-- para: para_003 -->
현재 위키에서 이 인덱스를 기준으로 연결되는 핵심 문서는 [[Polymarket 개요]], [[Polymarket API 레퍼런스]], [[Copytrade]], [[Copytrade 데이터 수집 가이드]], [[Copytrade 자동화 플로우]], [[WebSocket & 실시간 데이터]]다. 인덱스 페이지 자체는 전체 원문을 복사해 두는 곳이 아니라, 어떤 raw 묶음이 어느 문서군으로 해석됐는지 추적하는 안내판 역할을 맡는다.

## raw 자료를 읽는 순서

<!-- para: para_004 -->
가장 먼저 볼 자료는 Polymarket 공식 문서와 API 문서다. 여기서 마켓 구조, 이벤트/마켓 조회, WebSocket, 주문 관련 기본 용어를 맞춰 둬야 이후 Copytrade 설계 문서를 읽을 때 개념이 흔들리지 않는다.

<!-- para: para_005 -->
그다음 GitHub 구현 사례와 DeepWiki 요약을 보면 실제 자동화 파이프라인이 어떤 모듈로 나뉘는지 빠르게 파악할 수 있다. 이 단계에서는 "정확한 복제"보다 "어떤 데이터와 이벤트를 어디서 받아오는가"를 중심으로 보는 편이 낫다.

<!-- para: para_006 -->
마지막으로 Copytrade 서비스 문서를 보면 사용자 입장에서 필요한 설정 흐름과 운영 기능을 확인할 수 있다. 계정 연결, 추종 대상 선택, 위험 제한, 구독 모델 같은 요소는 구현 문서보다 서비스 문서에서 더 분명하게 드러난다.
