---
id: legacy_wiki_copytrade_59552d
title: Copytrade 리스크 관리
type: concept
status: draft
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T14:10:10Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_copytrade_md_59552dfc
tags:
- concept
- internal
---

# Copytrade 리스크 관리

## Summary

<!-- para: para_001 -->
> Copytrade(카피트레이드)에서 따라 거래할 때의 주요 리스크와 실무적 관리 방안 정리

## Key Facts

<!-- para: para_002 -->
Copytrade는 다른 트레이더의 포지션과 행보를 따라가는 전략으로, 알파를 얻는 동시에 추종자(팔로워)로서 고유한 리스크가 존재한다. 본 문서에서는 기존 항목을 보강하고 실무에서 바로 적용 가능한 예시와 모니터링 규칙을 추가한다.

<!-- para: para_003 -->
- 문제: 리더보드 상위 트레이더가 일시적 이벤트, 내부정보, 혹은 감정적 거래로 비합리적 포지션을 취할 수 있음. - 대응:
  - 트레이더의 행동 패턴(평균 보유기간, 손절/익절 빈도, 이벤트 중심 거래 여부)을 정량화하여 "신뢰 점수(Trust Score)"를 부여한다.

## Details

<!-- para: para_004 -->
- 문제: 팔로잉 시점의 가격·유동성 변화로 인해 추종 거래가 원 트레이더의 진입가와 다른 가격에 체결될 수 있음. - 대응:
  - 슬리피지 예상치 계산: 예상 슬리피지 = (예상체결볼륨 / 호가깊이) * 가격변동계수
  - 실무 예시: 목표 포지션 가치가 1000 USD이고, 호가 깊이로 즉시 소화 가능한 볼륨이 200 USD일 때 예상 슬리피지가 크면(예: >1%) 포지션을 0.25로 축소. - 운영 규칙: 시장 변동성(예: 1분 ATR)이나 거래량 급감 시 추종 보류, 허용 슬리피지 초과 시 재시도 대신 사이징 축소.

<!-- para: para_005 -->
- 문제: 원 트레이더의 포지션 사이즈가 팔로워의 위험 허용 한도를 초과할 수 있음. - 대응:
  - Scale-down 규칙 예시: follower_size_ratio = follower_equity / leader_equity
    - 적용 포지션 = leader_position * clamp(follower_size_ratio, 0.2, 0.5)
  - 손실-기반 사이징: 최대 허용 손실(예: 계좌의 2%)에 맞추어 포지션을 역산하여 제한. - 레버리지: 플랫폼과 규정에 따라 팔로워는 레버리지 사용을 금지하거나 별도 심사를 거쳐 허용.

<!-- para: para_006 -->
- 문제: 동일 트레이더를 과도하게 추종하면 포트폴리오가 특정 이벤트에 대해 과민해짐. - 대응:
  - 동일 트레이더 노출 상한(예: 총 자본의 10-15%) 설정. - 상관관계 기반 분산: 리더들의 전략·시장 노출을 메타데이터로 분류하여 비슷한 노출을 가진 리더들의 가중치를 제한.

<!-- para: para_007 -->
- 문제: Polymarket 등 예측시장 자체의 유동성 부족이나 API 변화로 거래가 어려워질 수 있음. - 대응:
  - 거래 전 목표 마켓의 유동성 지표(오더북 크기, 최근 거래량, 최근 체결 스프레드)를 확인. - 유동성 지표가 기준 이하이면 추종 차단.

## Open Questions

<!-- para: para_008 -->
Pending review.

## Related Pages

<!-- para: para_009 -->
Source summary: source_summary_src_wiki_copytrade_md_59552dfc
