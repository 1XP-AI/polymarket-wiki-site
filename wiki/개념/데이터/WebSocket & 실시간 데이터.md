---
id: legacy_raw_06_websocket_506430
title: WebSocket & 실시간 데이터
type: concept
status: verified
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-11T16:12:37Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 4
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_데이터
- legacy_raw_00_index_ec3366
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_6a6853
tags:
- concept
sources:
- url: https://uvicorn.dev/release-notes/
- url: https://websocket.org/reference/websocket-api
- url: https://yinternational.co.kr/websocket-%EC%8B%A4%EC%8B%9C%EA%B0%84-%ED%86%B5%EC%8B%A0%EC%9D%98-%EB%AA%A8%EB%93%A0-%EA%B2%83-http%EC%99%80%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%99%80-%ED%99%9C%EC%9A%A9-%EC%82%AC%EB%A1%80/
- url: https://developer.mozilla.org/ko/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications
cluster: 데이터
cluster_group: 실시간/파이프라인
doc_role: data-reference
---
# WebSocket & 실시간 데이터

## 요약

<!-- para: para_001 -->
> 출처: docs.polymarket.com WebSocket (2026-04-04 수집)

<!-- para: para_002 -->
Polymarket은 실시간 데이터 스트리밍을 위해 여러 WebSocket 채널을 제공한다.

<!-- para: para_003 -->
- 인증 불필요
- 실시간 오더북, 가격, 마켓 변경 데이터
- 구독할 마켓(토큰 ID)을 지정

<!-- para: para_004 -->
- 오더북 업데이트 (bid/ask 변경)
- 가격 변경
- 거래 체결
- 마켓 상태 변경

<!-- para: para_005 -->
- L2 Auth 필요
- 자신의 주문/거래 업데이트
- 주문 상태 변경 (생성, 매칭, 체결, 취소)
- 포지션 변경

<!-- para: para_006 -->
- 스포츠 경기 실시간 스코어
- 게임 상태 업데이트

<!-- para: para_007 -->
- 코멘트 스트리밍
- 크립토 가격
- 주가 (equity prices)

<!-- para: para_008 -->
- `/trades?address={wallet}` 를 주기적으로 호출

## 추가 내용

<!-- para: para_009 -->
Polymarket은 4가지 WebSocket 채널을 제공하며, 용도와 인증 요구사항이 다르다.

|채널 | 인증 | 용도 |
|------|------|------|
| Market | 불필요 | 공개 오더북·가격·거래 실시간 스트림 |
| User | L2 Auth 필요 | 개인 주문/체결/포지션 이벤트 |
| Sports | 불필요 | 스포츠 경기 스코어·상태 업데이트 |
| RTDS | 불필요 | 외부 데이터(크립토 시세, 주가, 코멘트) |

## 열린 질문

- Polymarket의 Market, User, Sports, RTDS WebSocket 채널은 각각 어떤 이벤트를 어떤 지연 특성으로 제공하며, 토큰 ID 또는 wallet 기준 구독 설계는 어떻게 달라지는가?
- L2 Auth가 필요한 User 채널은 어떤 인증 절차와 권한 범위를 요구하며, 주문 생성·매칭·체결·취소·포지션 변경 이벤트는 어떤 순서와 필드로 수신되는가?
- 실시간 오더북과 가격 변화를 WebSocket으로 처리할 때, 재연결·중복 이벤트·순서 역전·상태 동기화 문제를 어떻게 방지하고 복구하는가?

## 세부 내용

<!-- para: para_010 -->
WebSocket 실시간 통신의 모든 것, HTTP와의 차이와 활용 사례 - Y Information
콘텐츠로 바로가기
메뉴
닫기
여러분의 일상에 작지만 소중한 변화를 드리고자 합니다. 이곳에서 발견하는 정보가 조금이나마 도움이 되기를 바랍니다.

<!-- para: para_011 -->
WebSocket vs SSE vs HTTP

📖 Once Upon a Socket

<!-- para: para_012 -->
Control flow & error handing

Using the Web animation API

<!-- para: para_013 -->
websockets-sansio에 대해 WebSocket keepalive ping을 구현합니다.

이제 Uvicorn을 종료해도 됩니다. @pamelafox의 신호를 받았습니다. Ctrl+C를 47번이나 눌러 주신 덕분에 문제를 확인했고, 이를 수정해 준 @tiangolo에게도 감사드립니다.
