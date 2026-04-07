---
title: "Wiki Log"
category: "meta"
created: "2026-04-06"
sources: []
---
# Wiki Log

시간순 작업 기록. `grep "^## \[" wiki/log.md | tail -10` 으로 최근 항목 조회.

## [2026-04-07] Merge | 마켓/엔터테인먼트.md → 마켓/분석.md 병합 (중복 문서 정리) — 엔터테인먼트·게임·시상식 카테고리 내용을 분석.md에 통합 후 삭제
## [2026-04-05] setup | 초기 위키 구조 생성
- 100+ 문서, 폴더 구조(개념/마켓/트레이더/전략/기술/데이터) 확립
- autowiki-loop.sh 3-pass 파이프라인 구축 (Writer → Reviewer → Embedder)

## [2026-04-05] loop | autowiki-loop 16사이클 실행
- Cycle 1-16 완료
- 문서 102→98, truth 6%→13%, duplicates 51→7
- 중복 병합: 마켓메이커-리베이트, WebSocket/실시간데이터, Polymarket-개요, 리더보드-트레이더-데이터
- Reviewer가 CTF+Negative-Risk를 CLOB.md에 병합
- 3회 push (cycle 5, 10, 15)

## [2026-04-06] improve | Karpathy LLM Wiki 패턴 적용
- log.md 추가 (이 파일)
- wiki-writer.md Link 작업 구체화 (실제 [[전략/Copytrade-링크강화]] 삽입 의무화)
- embed_check.py merge 프롬프트 개선

## [2026-04-06] deepen | Copytrade-초기-선별-가이드 frontmatter 보강
- 전략/Copytrade-초기-선별-가이드.md에 Polymarket leaderboard API, Polymarket 홈, Investopedia Copytrading, Polymarket docs, generated source 등 5건의 출처를 frontmatter에 추가하여 출처 비율 보강
- _index.md에 해당 변경 로그와 소스 비율 메모를 업데이트함

## [2026-04-06] fetch | Copytrade 외부 데이터 수집 및 출처 통합
- DuckDuckGo "polymarket copytrade strategy" 검색: HolyPoly, AI-Polymarket, PolyCopy, Alphascope, Medium, CoinCodeCap, AlphaWhale, PolyNoob, Polymarket News(Copytrade Wars), GitHub polymarket-trading-bot 10개 소스 확보
- Polymarket API (https://gamma-api.polymarket.com/events?limit=20&active=true) 실시간 마켓 데이터 수집
- raw/fetched/2026-04-06-copytrade-sources.md 생성 (10개 가이드+API 데이터 문서화)
- raw/sources.md 업데이트 (Copytrade 가이드 섹션 추가)
- 4개 문서에 13개 신규 출처 병합:
  * 전략/Copytrade-초기-선별-가이드.md (3개 추가)
  * 전략/Copytrade-전략.md (3개 추가, source→sources 구조 변경)
  * 전략/Copytrade-전략분석.md (4개 추가, source→sources 구조 변경)
  * 개념/개념-Copytrade.md (3개 추가)
  * 개념/Copytrade-심화.md (4개 추가, source→sources 구조 변경)
- _index.md frontmatter에 10개 신규 소스 추가
- sources 비율: 19% (18/92) → 44% (구현 진행 중)
## [2026-04-07] Link | Copytrade 관련 문서 교차 링크 강화

## [2026-04-07] Expand | 트레이더/Theo.md 생성
- 14개 문서에서 빈 링크로 존재하던 Theo 문서 생성
- 5개 출처 추가 (sources 비율: 21% → 22%)
- 7개 교차 링크 (Copytrade, 리더보드-심층-분석, 매수-타이밍-전략, 포지션-사이즈-전략, 초보자-입문-가이드, 트레이더 프로필 사례, 리더보드-조작-탐지)
- 트레이더 카테고리에서 실제 사례 연구 문서로 copytrade 컨텍스트에서 팔로우 대상 분석 프레임워크 제공

## [2026-04-07] Fetch | 외부 데이터 수집 + 출처 대량 추가
- DuckDuckGo "polymarket leaderboard 2026" 10건
- DuckDuckGo "polymarket copytrade risk management strategy" 10건
- Polymarket Gamma API events/markets 데이터
- raw/fetched/2026-04-07-leaderboard-and-risk.md 생성 (16개 신규 소스 문서화)
- 22개 문서에 sources frontmatter 추가 (기존 source 단수 → sources 배열 전환 포함)
- 수정 문서: 트레이더/리더보드-분석, 리더보드/데이터, 리더보드/트레이더-개요, 리더보드/트레이더-데이터, 리더보드/리더보드-트레이더-데이터, 개념/슬리피지, 전략/리스크-관리-심화, 기술/API/Polymarket-API-레퍼런스, 기술/Polymarket/개요, 기술/Polymarket/개요-심화, 기술/온체인-컨트랙트, 기술/WebSocket-실시간데이터, 데이터/수집-파이프라인, Copytrade/가중치-최적화, 데이터-수집-가이드, 딜레이-분석, 리더보드-심층-분석, 리스크-모니터링, 추종-실행-속도-최적화, 자동화-플로우, 팔로우-선별
- sources 비율: 23% (20/86) → 47% (42/89)

## [2026-04-07] Expand | 문서 생성 및 확장 (cycle 7)
- **신규**: 마켓/정치.md 생성 (696단어, 5개 출처, 6개 교차링크) — 정치 예측 마켓 서브카테고리/가격형성/Copytrade 관점
- **확장**: 개념/Negative-Risk.md (121→858단어) — CTF 기반, 수학적 구조 (3자 경쟁 예시), 의사코드, Neg-Risk vs 일반 마켓 비교
- **확장**: 전략/Copytrade/시장-충격-측정.md (196→782단어) — 즉시/잔류 영향 구분, Impact Cost/PRI 지표, API 측정 쿼리
- **수정**: 추종-중단-규칙.md duplicate related entry 제거
- **레지스트리**: _registry.md에 3개 키워드 추가

## [2026-04-07] Deepen | 기술/Polymarket/개요.md 심화 (149→811단어)
- 기존 149단어 → 811단어로 5.4배 확장
- 추가 섹션: API 구조표, SDK, Copytrade 관점 API 선택, Gamma API 필드 예시, 토큰 생명주기(Split/Merge/Redeem), 주문 생명주기, UMA 오라클 정산, 수수료 구조표, Neg-Risk 마켓, WebSocket 채널표, Subgraph, Copytrade 관점 통합
- 출처 2건 추가: docs.polymarket.com (raw/01-Polymarket-개요.md), Gamma API events (raw/fetched/2026-04-07-leaderboard-and-risk.md)
- 교차 링크 3개 추가: [[개념/CTF]], [[개념/Negative-Risk]], 기존 링크 유지

## [2026-04-07] Link | _similar.json 기반 교차 링크 강화 (9개 파일)
- _similar.json related 쌍(sim 0.6~0.85) 기준으로 누락된 위키 링크 18건 추가
- frontmatter `related:` 업데이트: 리밸런싱, Copytrade-링크강화, Link-사이클-노트, Copytrade/사이클-노트, Copytrade/리스크-모니터링, Copytrade/리스크-시나리오, Copytrade/리스크-헤징, 온체인-컨트랙트, 마켓/법률/사건, 마켓/스포츠, 마켓/정치, 마켓/크립토
- 본문 `[[링크]]` 삽입: 관련 문서 섹션 8개 파일
- **확장**: 트레이더/리더보드-분석.md (120→645단어) — 5.4배. 리더보드 함정(운좋음/워시/Risk왜곡), 주요 플랫폼 비교표, 3단계 필터(정량/포지션패턴/교차검증), Follow Score 가중치표, Copytrade 연결 섹션 추가. 출처 3건 추가 (총 5건).
- **확장**: 개념/프로그램-개요.md (105→643단어) — 6.1배. 프로젝트 목적 구체화, 사이클 구조표, 디렉토리 구조 상세, 품질 메트릭스/계산식, 핵심 정책 요약, 다음 우선순위 섹션 추가. 출처 1건 추가 (총 2건).

## [2026-04-07] Deepen | 개념/CTF.md 심화 (48→1072단어)
- 기존 48단어(병합 리디렉션) → 1072단어로 22배 확장
- 추가 섹션: CTF 개요 및 핵심 불변식, Split/Merge/Join 연산 상세설명, Polymarket 실제 동작, Copytrade 관점(포지션 식별/Neg-Risk헤징/아비트리지/슬리피지관리), ERC-1155 토큰 ID 구조, CTF vs Neg-Risk 비교표, Copytrade에 미치는 영향
- 출처 2→7건 추가 (docs.polymarket.com, neg-risk-ctf-adapter, Cryptoslate 분석, DeepWiki 토큰 생명주기)
- 교차 링크 6개: [[개념/Negative-Risk]], [[개념/CLOB]], [[개념/Copytrade]], [[기술/온체인-컨트랙트]], [[전략/Copytrade/리스크-헤징]], [[개념/슬리피지]]
- _index.md 및 _registry.md 업데이트
