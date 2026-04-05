---
title: "WebSocket 실시간데이터"
category: "infrastructure"
created: "2026-04-05"
source: "raw/06-WebSocket-실시간데이터.md"
related:
  - "[[API 레퍼런스]]"
  - "[[Polymarket 개요]]"
---

# WebSocket 실시간데이터

> 한 줄 요약: Market/User/Sports 등 채널을 통한 실시간 오더북·트레이드 스트림 사용법과 주의점을 정리합니다.

## 내용

Polymarket의 실시간 데이터는 WebSocket을 통해 제공됩니다. Market 채널은 공개 오더북·가격 변동을 스트리밍하고, User 채널은 인증된 유저의 개인 이벤트를 전송합니다. Rate limit과 재접속 전략, 메시지 포맷(예: 주문/체결 이벤트)과 간단한 파싱 예제를 포함합니다.

원본: raw/06-WebSocket-실시간데이터.md
