---
id: legacy_wiki_00_index_3809cd
title: 시드 인덱스
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
- source_summary_src_wiki_00_index_md_3809cdf9
tags:
- concept
- internal
---

# 시드 인덱스

## Summary

<!-- para: para_001 -->
> raw 디렉토리의 시드 문서 목록과 위키 변환 기준

## Key Facts

<!-- para: para_002 -->
raw/ 디렉토리는 외부에서 수집된 정제되지 않은 원본 데이터를 보관하는 곳입니다. 이 인덱스는 각 시드 문서가 어떤 주제인지, 위키의 어느 카테고리로 매핑되어야 하는지를 정의합니다.

<!-- para: para_003 -->
| 파일 | 주제 | 매핑 카테고리 | 설명 |
|------|------|--------------|------|
| `00-INDEX.md` | 시드 인덱스 | 개념 | 본 파일 — raw/ 시드 목록과 변환 기준 |
| `01-Polymarket-개요.md` | 플랫폼 개요 | 개념/Polymarket-개요 | Polymarket 구조, CLOB, CTF, 정산 |
| `02-API-레퍼런스.md` | API 레퍼런스 | 기술/API | Gamma, Data, CLOB API 엔드포인트 |
| `03-Copytrade-전략분석.md` | 카피트레이드 | 전략/Copytrade/ | 트레이더 선별→팔로우→모니터링 파이프라인 |
| `04-마켓메이커-리베이트.md` | Maker 리베이트 | 전략/마켓메이커/ | 유동성 제공자 리베이트 프로그램 |
| `05-리더보드-트레이더-데이터.md` | 리더보드 | 트레이더/리더보드/ | 트레이더 랭킹, PnL, 포지션 데이터 |
| `06-WebSocket-실시간데이터.md` | 실시간 데이터 | 기술/WebSocket | 가격·포지션 스트리밍 |
| `07-온체인-컨트랙트.md` | 온체인 컨트랙트 | 기술/온체인 | CTF, Split/Merge/Redeem 흐름 |

## Details

<!-- para: para_004 -->
1. **시드 → 위키**: raw/의 시드를 wiki/{카테고리}/로 변환하며, 원본은 유지
2. **중복 방지**: 새 파일 생성 전 기존 wiki/ 내에서 중복 확인
3.

<!-- para: para_005 -->
`raw/fetched/`는 각 Fetch 사이클에서 DuckDuckGo, Polymarket API 등으로 수집한 데이터의 스냅샷입니다. 파일명 규칙: `YYYY-MM-DD-주제.md`. Deepen 작업 시 이 파일들을 raw source로 인용합니다.

<!-- para: para_006 -->
- [[개변/INDEX-요약]] — 시드 매핑 가이드, 확장 권장 문서
- [[개념/INDEX-요약-추가]] — 우선순위 체크리스트, 카테고리 매핑 판단 기준
- [[개념/프로그램-개요]] — autowiki-mlx 프로젝트 전체 구조, 사이클 워크플로우
- [[데이터/수집-파이프라인]] — raw/fetched/ 수집 파이프라인 아키텍처

## Open Questions

<!-- para: para_007 -->
Pending review.

## Related Pages

<!-- para: para_008 -->
Source summary: source_summary_src_wiki_00_index_md_3809cdf9
