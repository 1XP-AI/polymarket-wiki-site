---
id: legacy_raw_03_copytrade_c17abe
title: Polymarket Copytrade 전략 분석
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
- source_summary_src_raw_03_copytrade_md_c17abe9e
tags:
- concept
- internal
---

# Polymarket Copytrade 전략 분석

## 요약

<!-- para: para_001 -->
> 출처: Polymarket API 구조 분석 + Signal Foundry 설계 (2026-04-04)

## 핵심 사실

<!-- para: para_002 -->
다른 트레이더의 거래를 **실시간으로 감지하고 따라하는** 전략. Polymarket에서는 공개 API를 통해 누구의 포지션이든 조회 가능하므로, copytrade가 기술적으로 가능하다.

<!-- para: para_003 -->
```
GET https://data-api.polymarket.com/v1/leaderboard
파라미터: window=all|daily|weekly|monthly, limit, offset
```

- 수익률 기준 트레이더 순위
- 트레이더 지갑 주소 획득 가능
- 기간별 필터링 (전체/일간/주간/월간)

## 세부 내용

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
```
GET https://data-api.polymarket.com/activity?address={wallet}
```

- 최근 활동 (거래, 포지션 변경 등)

## 열린 질문

<!-- para: para_008 -->
GET https://gamma-api.polymarket.com/public-profile?address={wallet}

<!-- para: para_009 -->
GET https://data-api.polymarket.com/positions?address={wallet}

<!-- para: para_010 -->
GET https://data-api.polymarket.com/trades?address={wallet}

## 관련 페이지

<!-- para: para_011 -->
소스 요약: source_summary_src_raw_03_copytrade_md_c17abe9e
