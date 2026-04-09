---
id: source_summary_src_wiki_polymarket_md_fd0553d1
title: 'Source Summary: Polymarket 개요 — 심화'
type: source_summary
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T14:10:09Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: high
related_pages:
- legacy_wiki_polymarket_fd0553
tags:
- internal
- internal
---

# Source Summary: Polymarket 개요 — 심화

## Summary

<!-- para: para_001 -->
> Polymarket의 핵심 구성요소와 실무에서 copytrade에 활용하는 방법을 예제와 함께 설명합니다.

## Key Facts

<!-- para: para_002 -->
Polymarket은 Gamma API(마켓/이벤트), Data API(포지션/트레이드), CLOB(오더북)으로 구성되며, copytrade 전략은 리더보드·실시간 데이터·오더북 신호의 결합으로 설계한다.

<!-- para: para_003 -->
- 이벤트(event) → 마켓(market) → 결과(resolution)의 흐름
- 주요 인터페이스:
  - Gamma API: 마켓/이벤트 목록, 마켓 메타데이터
  - Data API: 트레이드·포지션 조회
  - CLOB: 주문장(오더북) 조회 및 일부 체결 정보

## Details

<!-- para: para_004 -->
예시: 활성 마켓 20개를 가져오는 간단한 curl 요청

```bash
curl -s "https://gamma-api.polymarket.com/markets?limit=20" \
  -H "Accept: application/json"
```

응답에서 얻을 수 있는 주요 필드:
- id: 마켓 식별자
- title: 마켓 제목
- category: 카테고리(예: 정치, 스포츠)
- state: active / resolved

<!-- para: para_005 -->
리더보드에서 지갑 주소를 찾았을 때, 해당 주소의 공개 프로필/포지션을 확인하는 예:

```bash
curl -s "https://gamma-api.polymarket.com/profiles/0x..." \
  -H "Accept: application/json"
```

이 데이터를 통해 해당 트레이더의 선호 시장(예: 크립토 vs 정치), 평균 포지션 크기, 청산 패턴 등을 추출해 copytrade 후보로 평가한다.

<!-- para: para_006 -->
아래 예제는 개념적 예시로, 실제 엔드포인트/토픽은 플랫폼 문서(`[[기술/WebSocket-실시간데이터]]`)를 확인한다. ```javascript
// Node.js 예시 (표준 WebSocket)
const WebSocket = require('ws');
const ws = new WebSocket('wss://gamma-socket.polymarket.com');

ws.on('open', () => {
  // 마켓 업데이트 구독 (예시 토픽)
  ws.send(JSON.stringify({ action: 'subscribe', channel: 'market:12345' }));
});

ws.on('message', (msg) => {
  const data = JSON.parse(msg);
  // 가격 변화나 오더북 변화 감지 → 알람/자동 추종 로직에 연결
  console.log(data);
});
```

> 주의: 인증이 필요한 채널은 API 키/토큰이 필요할 수 있다. 인증 채널은 `User Channel (Authenticated)`에 해당하므로 자동화 시 키 노출에 유의한다.

<!-- para: para_007 -->
1. 신뢰성: 리더보드 상위의 장기간 활동(예: 3개월 이상) 여부 확인 — `[[트레이더/리더보드/데이터]]` 참조
2. 실행 가능성: 해당 트레이더의 포지션 크기와 자신의 계정으로 재현 가능 여부
3.

## Open Questions

<!-- para: para_008 -->
curl -s "https://gamma-api.polymarket.com/markets?limit=20" \
