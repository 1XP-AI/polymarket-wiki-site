---
id: source_summary_src_raw_06_websocket_md_50643061
title: 'Source Summary: WebSocket & 실시간 데이터'
type: source_summary
status: verified
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-09T14:10:08Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: high
related_pages:
- legacy_raw_06_websocket_506430
tags:
- internal
- internal
---

# Source Summary: WebSocket & 실시간 데이터

## Summary

<!-- para: para_001 -->
> 출처: docs.polymarket.com WebSocket (2026-04-04 수집)

## Key Facts

<!-- para: para_002 -->
Polymarket은 실시간 데이터 스트리밍을 위해 여러 WebSocket 채널을 제공한다.

<!-- para: para_003 -->
- 인증 불필요
- 실시간 오더북, 가격, 마켓 변경 데이터
- 구독할 마켓(토큰 ID)을 지정

## Details

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

## Open Questions

<!-- para: para_008 -->
- `/trades?address={wallet}` 를 주기적으로 호출
