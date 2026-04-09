---
id: legacy_wiki_copytrade_4d0fc3
title: Copytrade
type: concept
status: draft
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T14:10:09Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_copytrade_md_4d0fc319
tags:
- concept
- internal
---

# Copytrade

## Summary

<!-- para: para_001 -->
> 리더보드 트레이더를 따라 거래하는 전략 — 개념, 계량적 평가, 백테스트, 실행, 모니터링을 아우르는 통합 문서

## Key Facts

<!-- para: para_002 -->
Copytrade는 리더보드 상의 검증된 트레이더를 추종해 그들의 포지션 변화를 자동으로 복제하는 전략이다. 이 문서는 카피트레이드의 개념적 기반과 계량적 평가 지표, 백테스트 설계, 실행·슬리피지 고려, 운영 모니터링 체크리스트 및 구현 템플릿을 제시한다.

<!-- para: para_003 -->
```
GET https://data-api.polymarket.com/v1/leaderboard
파라미터: window=all|daily|weekly|monthly, limit, offset
```

- 수익률 기준 트레이더 순위
- 트레이더 지갑 주소 획득 가능
- 기간별 필터링 (전체/일간/주간/월간)

## Details

<!-- para: para_004 -->
```
GET https://gamma-api.polymarket.com/public-profile?address={wallet}
```

- 프로필 정보, 거래 통계

<!-- para: para_005 -->
```
GET https://data-api.polymarket.com/positions?address={wallet}
```

- 현재 보유 포지션 전체 조회
- 마켓별 토큰 수량, 방향 (Yes/No)

<!-- para: para_006 -->
```
GET https://data-api.polymarket.com/trades?address={wallet}
```

- 과거 거래 기록
- 체결 가격, 수량, 시간, 방향

<!-- para: para_007 -->
- Market Channel로 특정 마켓의 거래 실시간 수신
- 특정 트레이더의 거래를 필터링하려면 trades 폴링 또는 온체인 이벤트 구독

## Open Questions

<!-- para: para_008 -->
GET https://gamma-api.polymarket.com/public-profile?address={wallet}

<!-- para: para_009 -->
GET https://data-api.polymarket.com/positions?address={wallet}

<!-- para: para_010 -->
GET https://data-api.polymarket.com/trades?address={wallet}

## Related Pages

<!-- para: para_011 -->
Source summary: source_summary_src_wiki_copytrade_md_4d0fc319
