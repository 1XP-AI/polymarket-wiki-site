---
id: legacy_raw_fetched_2026_04_05_polymarket_markets_a295cb
title: Polymarket 질문 원본 스냅샷
type: concept
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-11T12:21:39Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 0
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_데이터
- legacy_raw_00_index_ec3366
- legacy_wiki_clob_064e27
- legacy_wiki_copytrade_698574
- legacy_wiki_index_925404
- legacy_wiki_index_aa489a
- legacy_wiki_polymarket_2026_04_05_d5da53
tags:
- concept
sources: []
cluster: 데이터
cluster_group: 자료
doc_role: snapshot
---
# Polymarket 질문 원본 스냅샷

## 요약

<!-- para: para_001 -->
이 문서는 Polymarket 질문/마켓 목록 API 응답의 원형을 보존한 스냅샷을 사람이 읽기 쉽게 정리한 페이지다. 실제 원본 응답에는 질문 문구, slug, 마감 시각, 카테고리, 거래량, 유동성, 결과 토큰, 연결 이벤트 정보가 대량으로 들어 있다.

<!-- para: para_002 -->
실무적으로 자주 보는 핵심 필드는 `question`, `slug`, `endDate`, `category`, `outcomes`, `volume`, `active`, `closed`다. 위키에서는 대용량 JSON 전체를 노출하기보다, 어떤 필드가 들어 있고 무엇을 확인할 수 있는지 요약하는 편이 더 적절하다.

<!-- para: para_003 -->
예시 기록은 핵심 내용만 간단히 정리해 두면 전체 내용을 빠르게 파악하는 데 도움이 됩니다.

질문: "Will Joe Biden get Coronavirus before the election?"
슬러그: "will-joe-biden-get-coronavirus-before-the-election"
