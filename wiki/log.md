# Wiki Log

시간순 작업 기록. `grep "^## \[" wiki/log.md | tail -10` 으로 최근 항목 조회.

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
- wiki-writer.md Link 작업 구체화 (실제 [[교차링크]] 삽입 의무화)
- embed_check.py merge 프롬프트 개선

## [2026-04-06] deepen | Copytrade-초기-선별-가이드 frontmatter 보강
- 전략/Copytrade-초기-선별-가이드.md에 Polymarket leaderboard API, Polymarket 홈, Investopedia Copytrading, Polymarket docs, generated source 등 5건의 출처를 frontmatter에 추가하여 출처 비율 보강
- _index.md에 해당 변경 로그와 소스 비율 메모를 업데이트함
