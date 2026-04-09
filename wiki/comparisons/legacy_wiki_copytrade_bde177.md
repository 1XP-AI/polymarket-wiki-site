---
id: legacy_wiki_copytrade_bde177
title: 딜레이(지연) 분석 및 슬리피지 대응
type: comparison
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
- source_summary_src_wiki_copytrade_md_bde17783
tags:
- comparison
- internal
---

# 딜레이(지연) 분석 및 슬리피지 대응

## Summary

<!-- para: para_001 -->
> 카피트레이드에서 감지-진입 사이의 시간 지연(Latency)과 그로 인한 슬리피지(Slippage)를 측정하고 완화하는 방법.

## Key Facts

<!-- para: para_002 -->
카피트레이드는 다른 트레이더의 거래를 감지한 뒤 동일 방향으로 진입한다. 이때 감지부터 주문 생성·체결까지 생기는 시간 지연(딜레이, Latency)은 예상 가격과 실제 체결 가격 사이의 차이(슬리피지)를 발생시킨다.

<!-- para: para_003 -->
1. 감지-전송 지연: 이벤트 감지 시각 vs 주문 전송 시각
2.

## Details

<!-- para: para_004 -->
- 네트워크 지연 (네트워크 RTT)
- API 응답 지연 및 레이턴시 변동
- 주문 매칭 지연 (마켓 유동성 부족)
- 온체인 컨펌 지연(온체인 경로를 사용하는 경우)

<!-- para: para_005 -->
1. 진입 규모 조절: 카피 대상 포지션 대비 작은 비율로 먼저 진입하여 슬리피지 노출을 줄임
2. 슬리피지 모델링: 과거 감지-체결 딜레이 분포를 학습하여 기대 슬리피지 예측
3.

<!-- para: para_006 -->
```

<!-- para: para_007 -->
on_trade_event(event):
    detected_ts = now()
    detected_price = event.price
    order_id = submit_order(market=event.market, side=event.side, size=scale(event.size))
    sent_ts = now()
    fill = wait_for_fill(order_id)
    filled_ts = fill.timestamp
    filled_price = fill.price
    delay = filled_ts - detected_ts
    slippage = filled_price - detected_price if side == 'buy' else detected_price - filled_price
    record_metric(trader=event.trader, delay=delay, slippage=slippage)
```

## Open Questions

<!-- para: para_008 -->
Pending review.

## Related Pages

<!-- para: para_009 -->
Source summary: source_summary_src_wiki_copytrade_md_bde17783
