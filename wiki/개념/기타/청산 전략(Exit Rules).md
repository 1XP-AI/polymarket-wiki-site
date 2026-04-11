---
id: legacy_wiki_copytrade_3f7013
title: 청산 전략(Exit Rules)
type: concept
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-11T16:12:37Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 4
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://viewpoint.pwc.com/dt/gx/en/pwc/industry/industry_INT/industry_INT/real_estate__1_INT/Applying-IFRS-for-the-real-est/5-Real-estate-structures-and-tax-considerations/51-Consolidation/512-Definition-of/5123-Exit-strategy.html
- url: https://www.imidaily.com/europe/germanys-overlooked-exit-rule-men-aged-17-to-45-now-need-bundeswehr-permission-to-leave/
- url: https://portal.mexem.com/ko/trading/exit-strategy.php
- url: https://www.thegoodreview.com.au/2026/03/trust-company-exit-%EC%A0%84%EB%9E%B5-%EC%99%84%EC%A0%84-%EA%B0%80%EC%9D%B4%EB%93%9C-2026/
cluster: Copytrade
doc_role: concept
---
# 청산 전략(Exit Rules)

## 요약

<!-- para: para_001 -->
> 한 줄 요약: Copytrade에서 추종한 포지션의 손절·목표·자동 중단 규칙을 체계화하여 리스크를 통제하는 실전 가이드입니다.

<!-- para: para_002 -->
Copytrade는 타인의 포지션을 복제하는 특성상 진입보다 청산(Exit) 규칙이 더 중요합니다. 청산 규칙은 손절(stop-loss), 부분 청산(scale-out), 이익 실현(take-profit), 그리고 추종 중단(follow-stop)으로 구성되어야 합니다.

<!-- para: para_003 -->
- 포지션별 최대 손실 한도(MDD per position)를 미리 정한다 (예: 카피비율 기준 -5%).
- 시장 유동성과 슬리피지를 고려해 스탑 주문과 시장가 주문의 조합을 사용한다.

<!-- para: para_004 -->
1) 손절(Stop-loss): 진입 가격 대비 -6% 도달 시 지정가로 부분(50%) 청산, -10% 도달 시 전부 청산. 2) 이익 실현(Take-profit): +12% 달성 시 30% 부분 청산, +25% 달성 시 추가 청산. 3) 트레이더 성과 기반 추종 중단(Follow-stop): 해당 트레이더의 30일 누적 수익률이 -8% 이하로 내려가면 신규 진입 중단 및 보유 포지션을 지정된 비율(예: 30%)로 축소.

<!-- para: para_005 -->
- 주문 지연(latency)과 슬리피지를 줄이기 위해 WebSocket 이벤트 기반으로 트리거하고, 제출 시 가격 한도(limit)과 허용 슬리피지 범위를 함께 검증한다.
- 백테스트를 통해 각 손절·이익 실현 임계값의 기대 성과(Sharpe, Win-rate, MDD)를 검증한다.
- 여러 트레이더를 팔로우하는 경우 포지션 사이즈를 동적 재조정(리밸런싱)하여 포트폴리오 수준의 손실 한도를 유지한다.

<!-- para: para_006 -->
- 신규 트레이더 A를 1:100 비율로 복제. 진입 후 -7% 하락 발생 → 자동으로 50% 청산(지정가), 이후 추가 하락 시 전체 청산. 트레이더 A의 30일 누적손실이 -12%로 떨어지면 추종 중단 규칙 발동.

<!-- para: para_007 -->
- [[Copytrade 데이터 수집 가이드]] — 포지션 크기 및 청산 타이밍의 연계
- [[Copytrade 데이터 수집 가이드]] — 포트폴리오 레벨 리스크 한도 설정
- [[Copytrade 데이터 수집 가이드]] — 트레이더 성과 기반 중단 규칙

## 열린 질문

- Copytrade에서 손절(-6%, -10%)과 이익 실현(+12%, +25%) 임계값을 어떻게 조합해야 Sharpe, 승률, 최대낙폭(MDD) 기준의 기대 성과가 가장 안정적으로 개선되는지 백테스트로 검증할 수 있는가?
- WebSocket 이벤트 기반 트리거와 limit 주문, 시장가 주문의 조합이 주문 지연(latency)과 슬리피지를 얼마나 줄이는지, 유동성 수준별로 비교 측정할 수 있는가?
- 트레이더 30일 누적 수익률이 -8% 이하일 때 신규 진입 중단과 보유 포지션 30% 축소를 적용하는 follow-stop 규칙이 장기적으로 포트폴리오 손실 한도를 얼마나 줄이는가?

## 세부 내용

<!-- para: para_008 -->
Trust & Company Exit 전략 완전 가이드 2026

더굿리뷰 – The Good Review

온라인 광고, SEO, 웹사이트, 여행, 맛집, 호주, 시드니, 전화번호, 교민업소, 리뷰의 모든 것

<!-- para: para_009 -->
정치, 경제 및 기후 예측 계약 실시간 확인 -

개인, 공동 명의 또는 퇴직

<!-- para: para_010 -->
5.1.2.3. Exit strategy
Latest updates
Latest updates
What's new on Viewpoint?

<!-- para: para_011 -->
독일에서는 17세에서 45세 사이의 남성이 출국할 때 Bundeswehr의 허가가 필요하다는 점이 잘 알려지지 않았다.
