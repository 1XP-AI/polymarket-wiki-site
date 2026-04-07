---
title: "WebSocket 실시간데이터"
category: "infrastructure"
created: "2026-04-05"
sources:
  - url: "https://gamma-api.polymarket.com/events?limit=20&active=true"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
related:
  - "[[기술/API/Polymarket-API-레퍼런스]]"
  - "[[개념/Polymarket]]"
  - "[[기술/웹소켓/실시간데이터]]"
  - "[[데이터/Polymarket-GitHub-리포트]]"
---

# WebSocket 실시간데이터

> 한 줄 요약: Market/User/Sports 등 채널을 통한 실시간 오더북·트레이드 스트림 사용법과 주의점을 정리합니다.

## 내용

Polymarket의 실시간 데이터는 WebSocket을 통해 제공됩니다. Market 채널은 공개 오더북·가격 변동을 스트리밍하고, User 채널은 인증된 유저의 개인 이벤트를 전송합니다. Rate limit과 재접속 전략, 메시지 포맷(예: 주문/체결 이벤트)과 간단한 파싱 예제를 포함합니다.

원본: raw/06-WebSocket-실시간데이터.md

[[기술/웹소켓/실시간데이터]] 문서에서 WebSocket의 폴링·수집 구조를 함께 확인하라.
