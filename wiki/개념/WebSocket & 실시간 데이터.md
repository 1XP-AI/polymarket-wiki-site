---
id: legacy_raw_06_websocket_506430
title: WebSocket & 실시간 데이터
type: concept
status: draft
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-09T14:57:50Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 2
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_websocket_175ba8
- source_summary_src_raw_06_websocket_md_50643061
- source_summary_src_wiki_websocket_md_175ba89f
tags:
- concept
- internal
---

# WebSocket & 실시간 데이터

## 요약

<!-- para: para_001 -->
> 출처: docs.polymarket.com WebSocket (2026-04-04 수집)

## 핵심 사실

<!-- para: para_002 -->
Polymarket은 실시간 데이터 스트리밍을 위해 여러 WebSocket 채널을 제공한다.

<!-- para: para_003 -->
- 인증 불필요
- 실시간 오더북, 가격, 마켓 변경 데이터
- 구독할 마켓(토큰 ID)을 지정

## 세부 내용

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

## 열린 질문

<!-- para: para_008 -->
- `/trades?address={wallet}` 를 주기적으로 호출

## 관련 페이지

<!-- para: para_009 -->
소스 요약: source_summary_src_raw_06_websocket_md_50643061

<!-- para: para_001 -->
`WebSocket 실시간 데이터` 문서의 핵심 내용을 `WebSocket & 실시간 데이터`에 병합했다. 요약: > 한 줄 요약: Market/User/Sports/RTDS 채널을 통한 실시간 오더북·트레이드 스트림 사용법, 재접속 전략, Copytrade 지연 최소화 패턴.

## 핵심 사실 Polymarket은 4가지 WebSocket 채널을 제공하며, 용도와 인증 요구사항이 다르다. | 채널 | 인증 | 용도 |
|------|------|------|
| Market | 불필요 | 공개 오더북·가격·거래 실시간 스트림 |
| User | L2 Auth 필요 | 개인 주문/체결/포지션 이벤트 |
| Sports | 불필요 | 스포츠 경기 스코어·상태 업데이트 |
| RTDS | 불필요 | 외부 데이터(크립토 시세, 주가, 코멘트) |
