---
id: source_summary_src_wiki_copytrade_md_2ce18d7f
title: 'Source Summary: 리스크 알림 규칙'
type: source_summary
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T14:10:10Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: high
related_pages:
- legacy_wiki_copytrade_2ce18d
tags:
- internal
- internal
---

# Source Summary: 리스크 알림 규칙

## Summary

<!-- para: para_001 -->
> 한 줄 요약: Copytrade 운영 중 위험 상태 발생 시 자동으로 알림을 트리거하고 대응하는 규칙 모음

## Key Facts

<!-- para: para_002 -->
Copytrade는 여러 트레이더를 동시에 추종할 때 누적 리스크가 빠르게 증가할 수 있다. 이 문서는 운영자가 실시간으로 인지하고 조치할 수 있도록 설계된 알림 규칙을 정리한다.

<!-- para: para_003 -->
- 알림은 취소 가능한 자동화(예: 임시 추종 중지)와 사람 개입을 연계한다. - 각 경보는 raw 데이터 또는 Polymarket API에서 검증 가능한 근거를 포함해야 한다.

## Details

<!-- para: para_004 -->
- 포트폴리오 손실(%): (현재 포트폴리오 가치 - 기준 가치) / 기준 가치 * 100
- 단일 트레이더 집중(%): 트레이더별 노출액 / 포트폴리오 총노출액 * 100
- 예상 슬리피지(%): 주문 규모 대비 시장 깊이에 따른 추정 체결가 손실
- API 지연(ms): 최종 응답 타임스탬프 차이

메트릭은 가능한 경우 동일한 샘플링 주기(예: 1분)로 집계하고, 알림 결정은 롤링 윈도우(예: 5분, 1시간) 기준으로 평가한다.

<!-- para: para_005 -->
- Debounce/Throttle: 동일 경보가 5분 내 3회 발생해야 '진짜' 이벤트로 승격
- Escalation: P1 경보가 15분 내 해결되지 않으면 P0로 에스컬레이션
- 그룹화: 동일 마켓/트레이더 관련 이벤트는 1개 요약 알림으로 묶어 노이즈 감소

<!-- para: para_006 -->
- ALERT PortfolioLoss
  IF portfolio_loss_percent < -3
  FOR 2m
  LABELS {severity="P0"}
  ANNOTATIONS {summary="Portfolio loss exceeded -3%"}

이 규칙은 Prometheus/Grafana Alerting, Alertmanager와 같은 툴에 적합하며, 알림 라우팅과 지속시간(hold, repeat)을 Alertmanager에서 정의한다.

<!-- para: para_007 -->
{
  "alert": "PortfolioLoss",
  "severity": "P0",
  "value": -3.4,
  "timestamp": "2026-04-06T12:34:56Z",
  "evidence": {
    "portfolio_snapshot": "...",
    "leaderboard_snapshot": "...",
    "api_timestamps": ["..."]
  }
}

운영자는 페이로드에서 즉시 원인(어떤 트레이더, 어떤 마켓, 관련 주문)을 파악할 수 있어야 한다.

## Open Questions

<!-- para: para_008 -->
No open questions extracted.
