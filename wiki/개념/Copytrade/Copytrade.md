---
id: legacy_wiki_copytrade_4d0fc3
title: Copytrade
type: concept
status: verified
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T16:46:07Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 4
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_raw_00_index_ec3366
- legacy_wiki_copytrade_c6dea0
- legacy_wiki_index_925404
tags:
- concept
sources:
- url: https://www.forexbrokers.com/guides/social-copy-trading
- url: https://www.copytrade.net/
- url: https://errante.com/wp-content/uploads/2024/02/Errante-CopyTrading-Manual.pdf
- url: https://crosstrade.io/trade-copier
---
# Copytrade

## 요약

<!-- para: para_001 -->
> 리더보드 상위 트레이더를 따라 거래하는 전략의 개념, 데이터 수집, 실행 구조, 운영 리스크를 정리한 문서

<!-- para: para_002 -->
Copytrade는 특정 트레이더의 포지션 변화나 체결 신호를 추종해 자신의 계정에서도 유사한 포지션을 자동 또는 반자동으로 재현하는 방식이다. Polymarket에서는 리더보드 데이터, 공개 프로필, 포지션 스냅샷, 체결 내역을 조합해 추종 대상을 선별하고 복제 전략을 설계할 수 있다.

<!-- para: para_003 -->
Polymarket copytrade 구축에서 기본 수집 흐름은 리더보드 조회 -> 트레이더 프로필 확인 -> 현재 포지션 확인 -> 과거 체결 분석 순서다.

| 목적 | 엔드포인트 | 핵심 파라미터 |
| --- | --- | --- |
| 리더보드 조회 | `GET https://data-api.polymarket.com/v1/leaderboard` | `window=daily|weekly|monthly`, `limit`, `offset` |
| 트레이더 프로필 | `GET https://gamma-api.polymarket.com/public-profile?address={wallet}` | `address` |
| 현재 포지션 | `GET https://data-api.polymarket.com/positions?address={wallet}` | `address` |
| 과거 체결 | `GET https://data-api.polymarket.com/trades?address={wallet}` | `address` |

<!-- para: para_004 -->
리더보드 데이터는 수익률 기준 상위 트레이더를 찾는 출발점이다. 기간별 성과를 비교해 일간 급등형과 장기 일관형을 구분할 수 있고, 이후 프로필 API로 실제 지갑 주소와 공개 지표를 확인한다.

<!-- para: para_005 -->
포지션 API는 현재 보유 중인 Yes/No 토큰, 마켓별 익스포저, 평균 진입가를 재구성하는 데 유용하다. Copytrade에서는 이 스냅샷을 기준점으로 삼아 내 계정과 추종 대상 간 편차를 계산한다.

<!-- para: para_006 -->
트레이드 API는 체결 시각, 수량, 방향을 제공하므로 추종 전략의 반응 속도와 슬리피지 영향을 분석할 수 있다. 실시간 추종은 체결 스트림과 폴링을 함께 사용해야 안정적이다.

<!-- para: para_007 -->
실행 단계에서는 신호의 지연, 최소 주문 단위, 마켓 유동성, Neg-Risk 여부를 함께 고려해야 한다. 리더보드 성과가 좋아 보여도 진입 시점이 늦으면 동일한 수익률을 재현하지 못할 수 있다.

<!-- para: para_008 -->
운영 지표로는 누적 수익률보다 최대 드로우다운, 포지션 집중도, 시장 간 상관관계, 평균 보유 시간, 손실 후 회복 속도가 더 중요하다. 추종 대상을 바꿔야 하는 시점을 정하는 데도 이 지표들이 쓰인다.

<!-- para: para_009 -->
리스크 관리 기준은 일별 손실 한도, 단일 트레이더 최대 비중, 동일 이벤트군 중복 노출, 슬리피지 한도, API 장애 시 fail-safe 동작으로 정리하는 편이 좋다.

<!-- para: para_010 -->
결론적으로 Copytrade는 단순히 "잘하는 사람 따라 사기"가 아니라, 데이터 수집 파이프라인과 비중 배분 규칙, 리스크 차단 조건을 함께 설계해야 유지 가능한 전략이 된다.

## 외부 도구와 운영 사례

<!-- para: para_011 -->
CopyTrade는 복수 브로커와 플랫폼에서 주문 복제를 지원하는 상용 서비스로 자신을 소개한다. 핵심 제품은 로컬 복제, 클라우드 복제, 시그널 마켓플레이스, 화이트라벨 구성으로 나뉘며, 마스터 계정과 팔로워 계정 연결 및 전략 배포를 중심 기능으로 제시한다.

<!-- para: para_012 -->
ForexBrokers.com의 2026년 복사 거래 가이드는 eToro, Vantage, AvaTrade, Pepperstone, IC Markets, Tickmill, Exness, FXCM을 비교하며, 복사 거래에서는 브로커 신뢰도와 플랫폼 제약, 최소 예치금, 지원 자산 범위를 함께 봐야 한다고 정리한다.

<!-- para: para_013 -->
Errante의 CopyTrading 매뉴얼 PDF는 카피트레이딩 서비스의 계정 연결 절차, 전략 구독 흐름, 주문 복제 방식, 위험 고지와 사용자 책임 범위를 설명하는 운영 문서다. 사용자용 위키에는 PDF 원문 바이너리를 그대로 싣지 않고 핵심 내용만 남기는 편이 적절하다.

<!-- para: para_014 -->
CrossTrade의 Trade Copier 페이지는 NinjaTrader 계정 간 주문 복제를 위한 상용 도구를 설명한다. 주문 방향 반전, 계약 수 비율 조정, 심볼 치환, 재동기화, 장애 복구 같은 기능을 강조하며, 실제 copytrade 운영에서는 이런 "복제 엔진" 계층이 별도 제품으로 존재할 수 있음을 보여준다.
