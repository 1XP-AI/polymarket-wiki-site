---
id: legacy_wiki_copytrade_3f7013
title: 청산 전략(Exit Rules)
type: concept
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-09T15:09:33Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_copytrade_copytrade_5e34e9
tags:
- concept
---
# 청산 전략(Exit Rules)

## 요약

<!-- para: para_001 -->
> 한 줄 요약: Copytrade에서 추종한 포지션의 손절·목표·자동 중단 규칙을 체계화하여 리스크를 통제하는 실전 가이드입니다.

<!-- para: para_002 -->
Copytrade는 타인의 포지션을 복제하는 특성상 진입보다 청산(Exit) 규칙이 더 중요합니다. 청산 규칙은 손절(stop-loss), 부분 청산(scale-out), 이익 실현(take-profit), 그리고 추종 중단(follow-stop)으로 구성되어야 합니다.

<!-- para: para_003 -->
- 포지션별 최대 손실 한도(MDD per position)를 미리 정한다 (예: 카피비율 기준 -5%). - 시장 유동성과 슬리피지를 고려해 스탑 주문과 시장가 주문의 조합을 사용한다.

<!-- para: para_004 -->
1) 손절(Stop-loss): 진입 가격 대비 -6% 도달 시 지정가로 부분(50%) 청산, -10% 도달 시 전부 청산. 2) 이익 실현(Take-profit): +12% 달성 시 30% 부분 청산, +25% 달성 시 추가 청산. 3) 트레이더 성과 기반 추종 중단(Follow-stop): 해당 트레이더의 30일 누적 수익률이 -8% 이하로 내려가면 신규 진입 중단 및 보유 포지션을 지정된 비율(예: 30%)로 축소.

<!-- para: para_005 -->
- 주문 지연(latency)과 슬리피지를 줄이기 위해 WebSocket 이벤트 기반으로 트리거하고, 제출 시 가격 한도(limit)과 허용 슬리피지 범위를 함께 검증한다. - 백테스트를 통해 각 손절·이익 실현 임계값의 기대 성과(Sharpe, Win-rate, MDD)를 검증한다. - 여러 트레이더를 팔로우하는 경우 포지션 사이즈를 동적 재조정(리밸런싱)하여 포트폴리오 수준의 손실 한도를 유지한다.

<!-- para: para_006 -->
- 신규 트레이더 A를 1:100 비율로 복제. 진입 후 -7% 하락 발생 → 자동으로 50% 청산(지정가), 이후 추가 하락 시 전체 청산. 트레이더 A의 30일 누적손실이 -12%로 떨어지면 추종 중단 규칙 발동.

<!-- para: para_007 -->
- [[전략/Copytrade/포지션-사이즈-전략]] — 포지션 크기 및 청산 타이밍의 연계
- [[전략/Copytrade/리스크-관리]] — 포트폴리오 레벨 리스크 한도 설정
- [[전략/Copytrade/추종-중단-규칙]] — 트레이더 성과 기반 중단 규칙
