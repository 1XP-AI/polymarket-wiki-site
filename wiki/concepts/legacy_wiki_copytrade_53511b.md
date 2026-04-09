---
id: legacy_wiki_copytrade_53511b
title: 'Copytrade: 리더보드 활용'
type: concept
status: draft
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-09T14:10:11Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_copytrade_md_53511b22
tags:
- concept
- internal
---

# Copytrade: 리더보드 활용

## Summary

<!-- para: para_001 -->
> 한 줄 요약: 리더보드 데이터를 정량적 지표로 가공해 유망한 카피 대상(트레이더)을 선별하고, 위험을 통제하는 절차를 제시한다.

## Key Facts

<!-- para: para_002 -->
리더보드는 Polymarket에서 활동이 증명된 트레이더 풀을 제공한다. 이 문서는 리더보드의 공개 필드(순위, 수익, 거래량, 거래 빈도 등)를 기반으로 copytrade 후보를 평가하는 방법론을 제안한다.

<!-- para: para_003 -->
- 순위(rank): 장기적으로 높은 순위에 머문 트레이더 우선
- 누적 수익(profit): 높은 절대 수익과 안정적 수익 흐름을 확인
- 거래량(volume): 지나치게 낮은 거래량은 신호로서 약함
- 거래 빈도와 일관성: 일관된 활동은 전략 재현 가능성 증가
- 포지션 지속성: 빠른 진입·청산 반복은 추종 시 슬ippage 위험
- 마켓 분산성: 여러 마켓에 분산 투자하는 트레이더는 리스크 관리 능력 시사

## Details

<!-- para: para_004 -->
1. 리더보드(weekly/monthly)를 스냅샷으로 수집한다. ([[트레이더/리더보드/데이터]])
2.

<!-- para: para_005 -->
- 최소 거래량: 1,000 USDC 이상(지난 30일)
- 최소 거래 빈도: 주 1회 이상
- 최대 포지션 집중도: 특정 마켓에 50% 초과 보유 시 리스크 경고

<!-- para: para_006 -->
- 데이터 지연: 리더보드·포지션 API의 지연/미반영 문제
- 행위자 식별 어려움: 같은 지갑이 여러 계정을 사용할 가능성
- 과거 수익은 미래 성과를 보장하지 않음

<!-- para: para_007 -->
사례: 2026-03월 상위 50 스냅샷에서 상위 12명을 선별한 뒤, 각 트레이더의 평균 포지션 지속시간과 마켓 분산성을 분석했다. 그 결과 A트레이더는 높은 승률을 보였으나 단일 마켓 집중도가 70%로 높아 리스크 허용치 초과로 제외되었고, B트레이더는 중간 수익·중간 거래량이었으나 다양한 마켓에 분산되어 샘플 추종 대상에 포함되었다. 실제 소규모 롤아웃(각 트레이더당 전체 자본의 1%씩)에서 누적 손실 한도에 도달한 사례는 없었으나, 리더보드 업데이트 지연으로 인한 포지션 불일치가 관찰되어 모니터링 규칙을 강화했다.

## Open Questions

<!-- para: para_008 -->
Pending review.

## Related Pages

<!-- para: para_009 -->
Source summary: source_summary_src_wiki_copytrade_md_53511b22
