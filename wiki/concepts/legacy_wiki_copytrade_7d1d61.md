---
id: legacy_wiki_copytrade_7d1d61
title: 리더보드 심층 분석
type: concept
status: draft
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T14:10:10Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_copytrade_md_7d1d6197
tags:
- concept
- internal
---

# 리더보드 심층 분석

## Summary

<!-- para: para_001 -->
> 리더보드 데이터를 기반으로 Polymarket에서 copytrade 대상으로서의 가치를 정량·정성 평가하는 방법론과 체크리스트를 제시한다.

## Key Facts

<!-- para: para_002 -->
이 문서는 리더보드(leaderboard) 상위 트레이더의 활동 데이터를 심층 분석하여, Copytrade(복사거래)의 후보를 선별하고 리스크를 발현 가능한 지점에서 사전에 완화하는 절차를 설명한다. 핵심은 단순 수익률만 보지 않고, 포지션 분포, 진입·청산 패턴, 시장 충격(Market Impact), 보유 기간, 히든 포지션(옵션 등) 가능성 등을 종합해 팔로우 가치를 평가하는 것이다.

<!-- para: para_003 -->
- Polymarket API의 리더보드 및 프로필 엔드포인트(예: gamma-api.polymarket.com)를 사용해 트레이더의 공개 포지션과 과거 거래 로그를 수집한다. (인증 필요 없이 접근 가능한 엔드포인트만 사용)
- 수집 파일은 `raw/fetched/`에 저장하고, 파일 헤더에 source/fetched/endpoint 정보를 남긴다.

## Details

<!-- para: para_004 -->
(중략)

<!-- para: para_005 -->
- 트레이더의 최근 90일 수익률이 안정적이며, 변동성이 지나치게 높지 않은가? — 예/아니오
- 포지션 사이즈가 팔로워 허용 범위 내인가(시장 충격을 초래하지 않는가)? - 진입·청산 신호가 문서화하거나 관찰 가능한 규칙을 따르는가?

<!-- para: para_006 -->
1. 리더보드 스냅샷 주기 수집(예: 6시간 단위)
2. 신규 상위 트레이더 발견 → `wiki/트레이더/{트레이더명}/프로필.md` 자동 생성(요약 템플릿)
3.

<!-- para: para_007 -->
- [[트레이더/리더보드/데이터]] — 원시 리더보드 데이터 스키마 및 수집 가이드
- [[전략/Copytrade/트레이더-프로필-분석]] — 트레이더 평가 및 검증 기준
- [[트레이더/Theo]] — 예시 트레이더 프로필 연결
- [[트레이더/리더보드-분석]] — 리더보드 기반 트레이더 분석 개요 및 선별 방법

## Open Questions

<!-- para: para_008 -->
- 트레이더의 최근 90일 수익률이 안정적이며, 변동성이 지나치게 높지 않은가? — 예/아니오

<!-- para: para_009 -->
- 포지션 사이즈가 팔로워 허용 범위 내인가(시장 충격을 초래하지 않는가)?

<!-- para: para_010 -->
- 진입·청산 신호가 문서화하거나 관찰 가능한 규칙을 따르는가?

## Related Pages

<!-- para: para_011 -->
Source summary: source_summary_src_wiki_copytrade_md_7d1d6197
