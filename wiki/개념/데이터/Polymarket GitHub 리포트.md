---
id: legacy_wiki_polymarket_github_2f7358
title: Polymarket GitHub 리포트
type: concept
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-11T16:12:37Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 2
evidence_coverage: 1.0
confidence: medium
related_pages: []
tags:
- concept
sources:
- url: https://github.com/polymarket
- url: https://raw/fetched/2026-04-05-github-polymarket.md
cluster: Copytrade
doc_role: concept
---
# Polymarket GitHub 리포트

## 요약

<!-- para: para_001 -->
> Polymarket 관련 공개 GitHub 저장소의 구조와 주요 프로젝트 요약 — copytrade 파이프라인 관점에서 수집·분석

<!-- para: para_002 -->
GitHub API를 사용해 `polymarket` 키워드와 관련 조직, 프로젝트를 검색합니다. 이어서 README와 핵심 코드, 예를 들어 스크립트, Dockerfile, CI 설정 등을 살펴 기능을 분류합니다. 이 과정에서는 특히 copytrade 관련 모듈, 예를 들면 leaderboard 파싱, trade stream, simulation adapter 등을 우선적으로 식별합니다.

<!-- para: para_003 -->
1. 데이터 파이프라인

<!-- para: para_004 -->
- 리더보드 파서: 트레이더 메타데이터 자동 추출용
- 포지션/트레이드 로그 수집기: 포지션 스냅샷과 체결 로그 보존
- 시뮬레이터: Signal Foundry의 SimulationAdapter와 병합 가능한 구현
- WebSocket/Stream 클라이언트: 실시간 거래 감지용

<!-- para: para_005 -->
- 일부 프로젝트는 비공식 API 사용으로 rate limit/정책 변경에 민감합니다.
- 라이선스 확인 필요(상업적 사용 제한 가능성).
- 외부 코드를 그대로 실행하지 말고, 로컬 샌드박스에서 코드 리뷰 후 적용할 것.

<!-- para: para_006 -->
- [ ] 리더보드 파서로 상위 100명 메타데이터 수집 자동화
- [ ] 발견된 시뮬레이터 코드를 SimulationAdapter로 포팅해 백테스트 실행
- [ ] WebSocket 클라이언트를 테스트 환경에서 실시간 스트리밍 검증
- [ ] 라이선스 및 보안(의존성) 스캔

## 열린 질문

- Polymarket 공개 GitHub 저장소 중 copytrade 파이프라인에 직접 활용 가능한 레포만 추려서, 리더보드 파서·trade stream·시뮬레이터·WebSocket 클라이언트가 각각 어느 저장소에 구현돼 있는지와 최신 커밋 기준 유지보수 상태를 확인할 수 있는가?
- `polymarket` 관련 GitHub 저장소들에서 비공식 API 의존 코드가 어떤 엔드포인트와 인증 방식에 붙어 있는지 조사하고, rate limit 또는 정책 변경에 취약한 부분이 어디인지 구체적으로 식별할 수 있는가?
- 상위 트레이더 메타데이터를 자동 수집하는 리더보드 파서 구현체를 찾아, 수집 필드, 업데이트 주기, 중복 제거 방식, 실패 재시도 로직이 어떻게 설계돼 있는지 검증할 수 있는가?
