---
id: legacy_wiki_polymarket_aa7ff7
title: Polymarket 개요
type: concept
status: draft
created_at: '2026-04-09T14:10:09Z'
last_updated: '2026-04-09T14:10:09Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_wiki_polymarket_md_aa7ff7f8
tags:
- concept
- internal
---

# Polymarket 개요

## Summary

<!-- para: para_001 -->
> Polymarket와 예측 시장의 핵심 구조 및 copytrade 관점에서의 주요 고려사항을 정리합니다.

## Key Facts

<!-- para: para_002 -->
Polymarket은 사건 결과에 베팅하는 예측시장(prediction market) 플랫폼입니다. 각 마켓은 Yes/No 또는 다중 아웃컴(outcome)을 가지며, 가격은 해당 결과의 암묵적 확률을 반영합니다.

<!-- para: para_003 -->
- CLOB(중앙 주문장): 지정가 주문으로 시장에 유동성을 제공. 복잡한 체결 규칙과 리베이트/수수료 정책이 적용될 수 있어 고빈도 추종자에게 유리하거나 불리할 수 있음(리베이트 존재 시 유리).

## Details

<!-- para: para_004 -->
실행 비용은 여러 요소로 구성됩니다:
- 플랫폼 수수료(스프레드/거래 수수료)
- 슬리피지(시장 충격)
- 가스비(온체인 Split/Merge/Redemption)
- 환전/브리지 비용(사용자 자산이 여러 체인에 분산된 경우)

예시: 1% 수수료, 예상 슬리피지 0.3%, 가스비 트랜잭션당 $0.50인 상황에서 100달러 규모 포지션을 10회 분할 추종하면 총 비용은 대략:

- 수수료 합계: 100 * 1% * 10 = $10
- 슬리피지 합계(대략): 100 * 0.3% * 10 = $3
- 가스비: $0.50 * 10 = $5
- 총계 약: $18 → 포지션별 수익률을 갉아먹음

따라서 소액·다수 포지션을 반복 추종할 때는 비용 구조를 반드시 모델링해야 합니다(관련: [[전략/Copytrade/실행-비용]], [[전략/Copytrade/추종-실행-속도-최적화]]).

<!-- para: para_005 -->
- 대상 선정: 리더보드·포지션·승률 등 계량지표로 후보를 선별하되, 과거 성과의 표본오차와 조작 가능성을 고려(자세한 선별 기준은 [[개념/Copytrade]] 참조). - 포지션 사이징: 자본 대비 가중치를 계산해 거래당 비용을 상쇄하고도 의미있는 기대수익을 확보할 수 있도록 설정. - 실행 속도 최적화: 추종 지연(follow-execution delay)은 성과에 큰 영향을 줌.

<!-- para: para_006 -->
- 기본 이벤트/마켓 조회:

```bash
curl -s "https://gamma-api.polymarket.com/events?limit=5&active=true"
```

- 간단한 Python 예제(마켓 제목 출력):

```python
import requests
resp = requests.get("https://gamma-api.polymarket.com/markets?limit=1", timeout=5)
resp.raise_for_status()
data = resp.json()
if isinstance(data, list) and len(data) > 0:
    m = data[0]
    print("market id:", m.get('id'))
    print("title:", m.get('title'))
else:
    print("no market data")
```

- 데이터 팁: 리더보드와 트레이드/포지션 API를 교차 분석해 트레이더의 거래주기, 평균 포지션 크기, 승률 등을 산출하면 선별 품질을 높일 수 있음(관련: [[트레이더/리더보드/데이터]], [[데이터/수집-파이프라인]]).

<!-- para: para_007 -->
Polymarket은 두 가지 마켓 구조를 지원합니다: **CTF 기반 마켓**과 **Negative Risk(Neg-Risk) 마켓**. Neg-Risk는 다중 결과 이벤트(예: 대선 후보 3인 이상)에서资本 효율적으로 포지션을 구성하는 메커니즘입니다.

## Open Questions

<!-- para: para_008 -->
curl -s "https://gamma-api.polymarket.com/events?limit=5&active=true"

<!-- para: para_009 -->
resp = requests.get("https://gamma-api.polymarket.com/markets?limit=1", timeout=5)

## Related Pages

<!-- para: para_010 -->
Source summary: source_summary_src_wiki_polymarket_md_aa7ff7f8
