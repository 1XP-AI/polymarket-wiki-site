---
title: "INDEX 요약: 확장 메모"
category: "개념"
created: "2026-04-05"
sources:
  - url: "raw/00-INDEX.md"
    added: "2026-04-05"
  - url: "https://www.polymarket.com"
    added: "2026-04-05"
  - url: "https://polymarket.gitbook.io"
    added: "2026-04-07"
  - url: "https://docs.polymarket.com/overview"
    added: "2026-04-07"
related:
  - "[[개념/INDEX-요약]]"
  - "[[개념/프로그램-개요]]"
  - "[[_index]]"
---

# INDEX 요약: 확장 메모

> INDEX 요약 문서에 대한 보충 설명과 위키 확장 시 우선순위 체크리스트

## 보충 내용

이 메모는 기존 `wiki/개념/INDEX-요약.md`의 확장을 보완하기 위해 생성되었습니다. 주요 목적은 raw/의 시드 문서들을 wiki/의 카테고리로 매핑하는 과정에서 자주 발생하는 판단 기준을 기록하는 것입니다.

## 우선순위 체크리스트

1. raw/에 새 시드가 추가되면 우선 `마켓`/`전략`/`기술`/`트레이더` 중 적합한 카테고리로 매핑
2. 시드 문서의 핵심 용어가 `wiki/_registry.md`에 존재하는지 확인 — 없으면 추가
3. 시드가 API 형태이면 `wiki/기술/API/`로, 실시간 데이터면 `wiki/기술/WebSocket-실시간데이터`로 분류
4. 리더보드/트레이더 관련 시드이면 `wiki/트레이더/` 아래 프로필 템플릿을 채우거나 새 프로필 파일 생성

## 카테고리 매핑 판단 기준

### 기술(Technology) 관련 시드
- CLOB, Order Book, API, SDK, WebSocket → `wiki/기술/`
- 온체인 컨트랙트, CTF, NegRiskAdapter → `wiki/기술/`
- py-clob-client, TypeScript/Python SDK → `wiki/기술/API/`

### 전략(Strategy) 관련 시드
- Copytrade, Leaderboard 분석, 리스크 관리 → `wiki/전략/`
- 마켓메이커, 리베이트 → `wiki/전략/마켓메이커/`
- 백테스트, 사이징, 필터링 → `wiki/전략/Copytrade/`

### 개론(Concept) 관련 시드
- 플랫폼 개요, CTF 개념, Negative Risk → `wiki/개념/`
- 프로그램 구조, 사이클 규칙 → `wiki/개념/`

### 트레이더(Trader) 관련 시드
- 개별 트레이더 프로필 → `wiki/트레이더/{트레이더명}.md`
- 리더보드 데이터 분석 → `wiki/트레이더/리더보드/`

### 마켓(Market) 관련 시드
- 정치, 스포츠, 크립토 등 카테고리별 마켓 → `wiki/마켓/`

## 품질 기준

### frontmatter 요구사항
- `title`, `category`, `created`, `sources:` 모두 필수
- `sources:` 가 비어있으면 truth_score 0 → 반드시 채워야 함
- `related:` 배열은 문서 간 교차 연결을 위해 최소 2개 권장

### 중복 방지
- 파일명 중복 체크: `find wiki/ -name '파일명.md'`
- 의미론적 중복: `_similar.json`의 유사도 > 0.7인 문서 확인

## 사이클 작업 기록 가이드

| 작업 유형 | 코드 | 결과 기록 위치 |
|-----------|------|---------------|
| 문서 심화 | Deepen | results.tsv + wiki/log.md |
| 새 문서 생성 | Expand | results.tsv + wiki/log.md |
| 연결 강화 | Link | results.tsv + wiki/log.md |
| 외부 데이터 수집 | Fetch | results.tsv + raw/fetched/ |

## 참고

- 이 문서는 위키 내부 보조 문서로, INDEX-요약의 세부 운영 지침을 제공합니다. 원본 INDEX-요약을 대체하지 않으며, 주로 작업자(에이전트)의 판단 보조용으로 사용됩니다.
- INDEX-요약과의 차별점: 이 문서는 매핑 기준, 품질 기준, 작업 기록 방법 등 운영 레시피를 포함합니다.
