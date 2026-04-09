---
id: legacy_wiki_copytrade_e7d623
title: 매수 타이밍 심화
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
- source_summary_src_wiki_copytrade_md_e7d62341
tags:
- concept
- internal
---

# 매수 타이밍 심화

## Summary

<!-- para: para_001 -->
> Copytrade에서 복사 매매의 성과를 높이기 위한 매수(진입) 타이밍 규칙과 실전 예시를 제시합니다.

## Key Facts

<!-- para: para_002 -->
이 문서는 Polymarket에서 다른 트레이더를 팔로우할 때 '언제' 진입해야 하는지에 대한 심화 가이드입니다. 기본 원칙은 다음과 같습니다.

<!-- para: para_003 -->
- 규칙 A (빠른 추종): 리더보드 상위 5위 내 트레이더가 신규 포지션을 만들고 10분 내 거래량이 2배 이상 증가하면 1차 진입(포지션의 30%)
- 규칙 B (확증 기반): 동일 트레이더가 동일 마켓에 대해 2건 이상의 트랜잭션을 연속으로 실행하면 추가 진입
- 규칙 C (리스크-조정 진입): 슬리피지·수수료를 고려해 예상 비용이 총 포지션 리스크의 1% 미만이면 진입 감행

## Details

<!-- para: para_004 -->
- 분할 진입 예시: 포지션 목표 3단계(30% / 30% / 40%). 첫 진입은 신호 발생 직후, 두 번째는 신호 확인 후 15~60분, 마지막은 마켓 가격이 목표 확률 밴드에 도달했을 때.

<!-- para: para_005 -->
- 실행비용(수수료·슬리피지)을 항상 계산하여 작은 수익률 차이로 손실이 발생하지 않도록 한다. - 트레이더의 청산 주기와 마켓의 유동성(예: 거래 깊이)을 확인한다. - 자동화된 복사(봇) 적용 시 rate limit과 API 신뢰성을 점검한다.

<!-- para: para_006 -->
- [[전략/Copytrade/매수-타이밍-전략]] — 기초 규칙
- [[개념/Copytrade]] — 전략 전체 맥락
- [[전략/Copytrade/실행-비용]] — 비용 산정 방법
- [[개념/CLOB]] — 주문장부 개념과 가격 영향
- [[개념/슬리피지]] — 비용·실행 위험 설명
- [[마켓/Polymarket-이벤트-스냅샷-2026-04-05]] — 실전 마켓 사례
- [[트레이더/Theo]] — 트레이더 프로필 연결 (리더보드 기반 사례)
- [[트레이더/리더보드/데이터]] — 리더보드 신호 연동 가이드

## Open Questions

<!-- para: para_007 -->
Pending review.

## Related Pages

<!-- para: para_008 -->
Source summary: source_summary_src_wiki_copytrade_md_e7d62341
