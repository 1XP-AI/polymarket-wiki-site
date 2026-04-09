---
id: legacy_wiki_polymarket_cd5a08
title: Polymarket 개요
type: concept
status: draft
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T15:11:57Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_01_polymarket_b75012
- legacy_wiki_polymarket_aa7ff7
- legacy_wiki_polymarket_b06656
- legacy_wiki_polymarket_fd0553
tags:
- concept
- internal
---
# Polymarket 개요

## 요약

<!-- para: para_001 -->
> 한 줄 요약: Polymarket 플랫폼의 핵심 구조, 개념(이벤트/마켓/토큰)과 데이터/오더북 구성 요약.

<!-- para: para_002 -->
Polymarket은 **세계 최대의 예측시장(Prediction Market)** 플랫폼으로, Polygon 블록체인 위에서 운영된다. 사용자가 실제 세계 이벤트의 결과에 USDC.e를 사용하여 베팅하며, 모든 정산은 온체인에서 이루어진다.

<!-- para: para_003 -->
| API | Base URL | 용도 | 인증 |
|-----|----------|------|------|
| **Gamma API** | `gamma-api.polymarket.com` | 마켓/이벤트/프로필/검색 | 불필요 (Public) |
| **Data API** | `data-api.polymarket.com` | 포지션/트레이드/활동/리더보드 | 불필요 (Public) |
| **CLOB API** | `clob.polymarket.com` | 오더북/가격/주문/거래 | 읽기: Public / 쓰기: L1/L2 Auth |

<!-- para: para_004 -->
- TypeScript: `@polymarket/clob-client`
- Python: `py-clob-client`
- Rust: `polymarket-rs`

<!-- para: para_005 -->
- **트레이더 추적**: Data API (`/v1/leaderboard`)로 상위 지갑 확인 → Gamma API로 해당 지갑의 이벤트/마켓 매핑
- **실시간 복제**: CLOB API WebSocket으로 오더북 구독 → 주문 체결 감지
- **마켓 발견**: Gamma API의 `?active=true` 필터로 신규/활성 마켓 스캔

<!-- para: para_006 -->
- **이벤트**: 하나의 질문/주제 (예: "2024 미국 대선 승자는?")
- **마켓**: 이벤트 내 개별 결과 옵션 (예: "트럼프 당선" / "바이든 당선")
- 하나의 이벤트에 여러 마켓이 존재

Gamma API 응답에서 확인되는 주요 필드:

```json
{
  "id": "이벤트 UUID",
  "ticker": "이벤트 티커",
  "title": "Full title",
  "slug": "url-friendly_slug",
  "description": "설명",
  "volume": "누적 거래량",
  "liquidity": "현재 유동성",
  "resolutionSource": "결과 판정 출처"
}
```

<!-- para: para_007 -->
- 가격 범위: **$0.00 ~ $1.00** (확률을 나타냄)
- $0.60 = 60% 확률이라는 시장 합의
- **[[개념/CLOB]]** (Central Limit Order Book): P2P 매칭 방식
- Bid(매수)와 Ask(매도)가 호가로 쌓임
- **Spread** = Best Ask - Best Bid (호간 격차)

<!-- para: para_008 -->
- **마켓 발견**: Gamma API의 `?active=true` 필터로 신규/활성 마켓 스캔

<!-- para: para_009 -->
- **이벤트**: 하나의 질문/주제 (예: "2024 미국 대선 승자는?")

## 추가 내용

<!-- para: para_010 -->
Polymarket은 사건 결과에 베팅하는 예측시장(prediction market) 플랫폼입니다. 각 마켓은 Yes/No 또는 다중 아웃컴(outcome)을 가지며, 가격은 해당 결과의 암묵적 확률을 반영합니다.

<!-- para: para_011 -->
Polymarket은 **세계 최대의 예측 시장(Prediction Market)** 플랫폼이다. 사용자가 실제 세계 이벤트의 결과에 베팅할 수 있으며, Polygon 블록체인 위에서 운영된다.

<!-- para: para_012 -->
Polymarket은 이벤트별 결과에 베팅하는 예측시장으로 CLOB(중앙지정가주문장)를 통해 거래가 이루어지고, Yes/No 토큰을 사용해 결과를 정산한다.

<!-- para: para_013 -->
Polymarket은 Gamma API(마켓/이벤트), Data API(포지션/트레이드), CLOB(오더북)으로 구성되며, copytrade 전략은 리더보드·실시간 데이터·오더북 신호의 결합으로 설계한다.
