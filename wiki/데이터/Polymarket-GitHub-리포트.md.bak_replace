---
title: "Polymarket GitHub 리포트"
category: "data"
created: "2026-04-05"
source: "raw/fetched/2026-04-05-github-polymarket.md"
related:
  - "[[API-레퍼런스]]"
  - "[[리더보드-트레이더-데이터]]"
---

# Polymarket GitHub 리포트

> Polymarket 관련 공개 GitHub 저장소의 구조와 주요 프로젝트 요약 — copytrade 파이프라인 관점에서 수집·분석

## 개요

이 문서는 raw/fetched/2026-04-05-github-polymarket.md에서 수집한 GitHub 검색 결과를 요약합니다. 목적은 Polymarket 및 관련 오픈소스 프로젝트(데이터 파이프라인, 시뮬레이터, 봇 등)가 copytrade 전략 구현에 어떻게 기여할 수 있는지를 평가하는 것입니다. 특히 데이터 수집, 리더보드 파싱, 시뮬레이션 어댑터, 자동화 스크립트 관점에서 유용한 저장소를 선별했습니다.

## 수집 방법

- GitHub API로 `polymarket` 키워드 및 관련 조직/프로젝트를 검색
- README와 주요 코드(스크립트, Dockerfile, CI)를 스캔하여 기능 분류
- copytrade 관련 모듈(leaderboard 파싱, trade stream, simulation adapter 등)을 우선적으로 식별

## 주요 발견

1. 데이터 파이프라인
   - 일부 저장소는 Polymarket API/비공식 엔드포인트를 대상으로 한 데이터 수집 스크립트를 포함합니다. cron/airflow 기반 스케줄러로 변환 가능하여 raw/fetched/에 저장되는 데이터 소스로 활용할 수 있습니다.

2. 리더보드/프로필 파서
   - 리더보드와 프로필 JSON을 파싱하는 유틸리티들이 발견되었습니다. 이들은 트레이더 선별 파이프라인(트레이더 특성 추출, 승률/거래빈도 계산)에 곧바로 재사용할 수 있습니다.

3. 시뮬레이션/백테스트 도구
   - 간단한 시뮬레이터(거래 이벤트를 입력으로 받아 PnL을 계산하는 모듈)가 있어 Signal Foundry의 SimulationAdapter와 결합해 빠른 PoC를 만들 수 있습니다.

4. 자동화 봇 및 WebSocket 클라이언트
   - 시장 데이터 스트리밍용 WebSocket 클라이언트 예제가 있어 실시간 감지 파이프라인 구현 시 참조 가능합니다. 다만 인증/RateLimit 처리 로직은 프로젝트마다 상이합니다.

5. 문서화 수준
   - 저장소마다 문서 품질이 큰 편차가 있습니다. README에 설치/사용법을 상세히 적은 프로젝트는 파이프라인 통합이 쉬우나, 일부는 주석/테스트가 부족합니다.

## copytrade 적용 관점의 권장 리포지토리 유형

- 리더보드 파서: 트레이더 메타데이터 자동 추출용
- 포지션/트레이드 로그 수집기: 포지션 스냅샷과 체결 로그 보존
- 시뮬레이터: Signal Foundry의 SimulationAdapter와 병합 가능한 구현
- WebSocket/Stream 클라이언트: 실시간 거래 감지용

## 리스크/주의사항

- 일부 프로젝트는 비공식 API 사용으로 rate limit/정책 변경에 민감합니다.
- 라이선스 확인 필요(상업적 사용 제한 가능성).
- 외부 코드를 그대로 실행하지 말고, 로컬 샌드박스에서 코드 리뷰 후 적용할 것.

## 적용 예시 (간단 체크리스트)

- [ ] 리더보드 파서로 상위 100명 메타데이터 수집 자동화
- [ ] 발견된 시뮬레이터 코드를 SimulationAdapter로 포팅해 백테스트 실행
- [ ] WebSocket 클라이언트를 테스트 환경에서 실시간 스트리밍 검증
- [ ] 라이선스 및 보안(의존성) 스캔

## 관련 문서

- [[API-레퍼런스]] — Polymarket API 엔드포인트 참고
- [[리더보드-트레이더-데이터]] — 리더보드 데이터 구조 및 사용법


(문서 작성: 2026-04-05, 원본: raw/fetched/2026-04-05-github-polymarket.md)