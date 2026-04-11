---
id: legacy_raw_fetched_2026_04_05_fetch_polymarket_f95e6d
title: '수집 원본: Polymarket snapshot — 2026-04-05'
type: concept
status: verified
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-11T12:23:57Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 0
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_copytrade_4d0fc3
tags:
- concept
cluster: Copytrade
cluster_group: 자료
doc_role: concept
---
# 수집 원본: Polymarket snapshot — 2026-04-05

## 요약

<!-- para: para_001 -->
Polymarket의 `markets` 엔드포인트에 `limit=50`을 적용해 활성 마켓의 현재 상태를 확인했다. 응답에는 여러 binary market이 포함되어 있었고, 각 마켓의 `id`, `description`, `status`도 함께 확인할 수 있었다.

출처:
- https://gamma-api.polymarket.com/markets?limit=50
- https://gamma-api.polymarket.com/events?limit=20&active=true
- DuckDuckGo 검색어: "polymarket copytrade"
