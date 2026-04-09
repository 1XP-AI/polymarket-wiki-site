---
id: legacy_raw_06_websocket_506430
title: WebSocket & 실시간 데이터
type: concept
status: draft
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-09T15:11:57Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 2
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_websocket_175ba8
tags:
- concept
- internal
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
