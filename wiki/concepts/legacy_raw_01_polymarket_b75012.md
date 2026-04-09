---
id: legacy_raw_01_polymarket_b75012
title: Polymarket 개요
type: concept
status: draft
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-09T14:10:08Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_raw_01_polymarket_md_b7501253
tags:
- concept
- internal
---

# Polymarket 개요

## Summary

<!-- para: para_001 -->
> 출처: docs.polymarket.com (2026-04-04 수집)

## Key Facts

<!-- para: para_002 -->
Polymarket은 **세계 최대의 예측 시장(Prediction Market)** 플랫폼이다. 사용자가 실제 세계 이벤트의 결과에 베팅할 수 있으며, Polygon 블록체인 위에서 운영된다.

<!-- para: para_003 -->
| API | Base URL | 용도 | 인증 |
|-----|----------|------|------|
| **Gamma API** | `gamma-api.polymarket.com` | 마켓/이벤트/프로필/검색 | 불필요 (Public) |
| **Data API** | `data-api.polymarket.com` | 포지션/트레이드/활동/리더보드 | 불필요 (Public) |
| **CLOB API** | `clob.polymarket.com` | 오더북/가격/주문/거래 | 읽기: Public / 쓰기: L1/L2 Auth |

## Details

<!-- para: para_004 -->
- TypeScript: `@polymarket/clob-client`
- Python: `py-clob-client`
- Rust: `polymarket-rs`

<!-- para: para_005 -->
- **이벤트**: 하나의 질문/주제 (예: "2024 미국 대선 승자는?")
- **마켓**: 이벤트 내 개별 결과 옵션 (예: "트럼프 당선" / "바이든 당선")
- 하나의 이벤트에 여러 마켓이 존재

<!-- para: para_006 -->
- 가격 범위: $0.00 ~ $1.00 (확률을 나타냄)
- $0.60 = 60% 확률이라는 시장 합의
- **CLOB (Central Limit Order Book)**: P2P 매칭 방식
- Bid(매수)와 Ask(매도)가 오더북에 쌓임
- Spread = Best Ask - Best Bid

<!-- para: para_007 -->
- 베팅 시 **CTF (Conditional Token Framework)** 토큰을 받음
- Yes 토큰 / No 토큰 쌍으로 존재
- 결과가 맞으면 $1.00으로 정산, 틀리면 $0.00
- USDC.e를 Split → Yes/No 토큰 쌍
- Yes/No 쌍을 Merge → USDC.e 복원
- 승리 토큰을 Redeem → USDC.e 수령

## Open Questions

<!-- para: para_008 -->
- **이벤트**: 하나의 질문/주제 (예: "2024 미국 대선 승자는?")

## Related Pages

<!-- para: para_009 -->
Source summary: source_summary_src_raw_01_polymarket_md_b7501253
