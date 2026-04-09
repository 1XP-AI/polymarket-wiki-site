---
id: legacy_wiki_copytrade_1f98b0
title: 리스크 모니터링(Copytrade)
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
- source_summary_src_wiki_copytrade_md_1f98b023
tags:
- concept
- internal
---

# 리스크 모니터링(Copytrade)

## 요약

<!-- para: para_001 -->
> 한 줄 요약: Copytrade 포트폴리오의 실시간·주기적 리스크 지표를 정의하고 모니터링 절차를 제시한다.

## 핵심 사실

<!-- para: para_002 -->
Copytrade 운영에서 리스크 모니터링은 단순 손실 추적을 넘어서, 트레이더별·마켓별·전략별로 위험 노출을 정량화하고 이상 징후를 조기에 탐지하는 체계다. 본 문서는 Polymarket에서 팔로우(복제)하는 트레이더의 활동을 관찰해 다음 항목을 지속적으로 계산하도록 권장한다.

<!-- para: para_003 -->
1) 포지션 집중도가 40%를 넘는 트레이더 발견 → 자동으로 팔로우 비중을 축소하거나 손실 트리거를 단계적으로 적용
2) 특정 마켓에서 예상 슬리피지가 평소보다 2배 증가 → 해당 마켓의 신규 진입을 일시 중단
3) 리더보드 급상승 트레이더가 다수 포지션을 취함 → 해당 트레이더의 과거 승률/청산 기록을 조회하고 가중치 재계산

## 세부 내용

<!-- para: para_004 -->
- raw API에서 포지션/마켓 데이터를 정규화하여 DB에 저장
- 지표 산출 스크립트(정의된 수식 포함)를 자동화하여 일일 보고 생성
- 알림 임계값(슬랙/웹훅) 설정: 경고/심각 단계 구분
- 모니터링 대시보드: 트레이더별 리스크 스코어 시각화

<!-- para: para_005 -->
상위 N개 포지션에 할당된 자본 비중을 측정한다. ```python
def concentration_index(positions, top_n=5):
    """허핀달-허쉬만 지수(HHI) 기반 집중도 계산"""
    if not positions:
        return 0
    total = sum(p['size_usd'] for p in positions)
    if total == 0:
        return 0
    shares = sorted([p['size_usd'] / total for p in positions], reverse=True)
    top_n_sum = sum(shares[:top_n])
    hhi = sum(s ** 2 for s in shares)
    return {"top_n_concentration": top_n_sum, "hhi": hhi}

<!-- para: para_006 -->
```

<!-- para: para_007 -->
트레이더의 주문 시점과 팔로워의 복제 주문 시점 차이. Polymarket의 경우 시장이 빠르게 움직이므로 지연이 수익률에 직접적 영향을 준다. ```python
def measure_execution_delay(trader_timestamp, follower_timestamp, market_snapshot):
    """
    trader_timestamp: 트레이더가 포지션을 연 시간 (UTC)
    follower_timestamp: 팔로워가 동일 포지션을 복제한 시간 (UTC)
    market_snapshot: 두 시점 사이의 마켓 가격 스냅샷 리스트

반환: 지연(초), 슬리피지(%), 예상 PnL 손실
    """
    delay_sec = (follower_timestamp - trader_timestamp).total_seconds()
    price_at_trade = market_snapshot[0]['price']
    price_at_copy = market_snapshot[-1]['price']
    slippage_pct = abs(price_at_copy - price_at_trade) / price_at_trade * 100
    return {
        "delay_seconds": delay_sec,
        "slippage_pct": slippage_pct,
        "critical": delay_sec > 30 or slippage_pct > 2.0
    }
```

## 열린 질문

<!-- para: para_008 -->
Pending review.

## 관련 페이지

<!-- para: para_009 -->
소스 요약: source_summary_src_wiki_copytrade_md_1f98b023
