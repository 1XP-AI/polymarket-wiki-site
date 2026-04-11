---
id: legacy_wiki_copytrade_1f98b0
title: 리스크 모니터링(Copytrade)
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-11T16:39:57Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- concept_copytrade
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_4d0fc3
- legacy_wiki_copytrade_59552d
tags:
- concept
sources:
- url: https://www.newswire.co.kr/newsRead.php?no=1028295
- url: https://www.copytrade.net/
- url: https://errante.com/wp-content/uploads/2024/02/Errante-CopyTrading-Manual.pdf
- url: https://keepamericaaffordable.com/%EC%8A%B9%EB%B6%80%EC%A1%B0%EC%9E%91-%EC%9E%90%EC%82%B0-%EC%9C%A0%EC%9E%85-%EC%B0%A8%EB%8B%A8/
- url: https://fss.or.kr/
cluster: Copytrade
cluster_group: 리스크
doc_role: analysis
---
# 리스크 모니터링(Copytrade)

## 요약

<!-- para: para_001 -->
> 한 줄 요약: Copytrade 포트폴리오의 실시간·주기적 리스크 지표를 정의하고 모니터링 절차를 제시한다.

<!-- para: para_002 -->
Copytrade 운영에서 리스크 모니터링은 단순 손실 추적을 넘어서, 트레이더별·마켓별·전략별로 위험 노출을 정량화하고 이상 징후를 조기에 탐지하는 체계다. 본 문서는 Polymarket에서 팔로우(복제)하는 트레이더의 활동을 관찰해 다음 항목을 지속적으로 계산하도록 권장한다.

<!-- para: para_003 -->
1) 포지션 집중도가 40%를 넘는 트레이더 발견 → 자동으로 팔로우 비중을 축소하거나 손실 트리거를 단계적으로 적용
2) 특정 마켓에서 예상 슬리피지가 평소보다 2배 증가 → 해당 마켓의 신규 진입을 일시 중단
3) 리더보드 급상승 트레이더가 다수 포지션을 취함 → 해당 트레이더의 과거 승률/청산 기록을 조회하고 가중치 재계산

<!-- para: para_004 -->
- raw API에서 포지션/마켓 데이터를 정규화하여 DB에 저장
- 지표 산출 스크립트(정의된 수식 포함)를 자동화하여 일일 보고 생성
- 알림 임계값(슬랙/웹훅) 설정: 경고/심각 단계 구분
- 모니터링 대시보드: 트레이더별 리스크 스코어 시각화

<!-- para: para_005 -->
상위 N개 포지션에 할당된 자본 비중을 측정한다. python

```python
def concentration_index(positions, top_n=5):
```

"""허핀달-허쉬만 지수(HHI) 기반 집중도 계산"""

<!-- para: para_006 -->
트레이더의 주문 시점과 팔로워의 복제 주문 시점 차이. Polymarket의 경우 시장이 빠르게 움직이므로 지연이 수익률에 직접적 영향을 준다. python

```python
def measure_execution_delay(trader_timestamp, follower_timestamp, market_snapshot):
    """
    trader_timestamp: 트레이더가 포지션을 연 시간 (UTC)
    follower_timestamp: 팔로워가 동일 포지션을 복제한 시간 (UTC)
    market_snapshot: 두 시점 사이의 마켓 가격 스냅샷 리스트
```

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

## 세부 내용

<!-- para: para_007 -->
승부조작 의심 자산 유입 원천 차단 및 관리자의 리스크 모니터링 공수 제거

승부조작 의심 자산 유입의 위험성과 관리의 중요성

<!-- para: para_008 -->
CopyTrade는 복사 거래를 활용해 수익을 높이려는 사용자와 계정 관리자를 위해 설계된 기능으로, 복사 거래 운영에 필요한 주요 요소를 한곳에서 다룰 수 있도록 구성되어 있습니다.

<!-- para: para_009 -->
원문 PDF 바이너리 덤프는 사용자용 위키에서 제거했다. 해당 자료는 카피트레이딩 서비스 설명서와 위험 고지, 주문 복제 방식 같은 운영 정보를 담은 PDF다.

<!-- para: para_010 -->
익스피리언 모델 리스크 관리 어시스턴트, 2026 BIG 혁신상 수상 - 뉴스와이어

익스피리언 모델 리스크 관리 어시스턴트, 2026 BIG 혁신상 수상

글로벌 금융기관의 규제 문서화에 맞춰 신속한 모델 혁신 지원하는 익스피리언 AI 역량 강조

<!-- para: para_011 -->
불법사금융 이자부담을 계산해보세요 (불법사금융 이자율 계산기)
