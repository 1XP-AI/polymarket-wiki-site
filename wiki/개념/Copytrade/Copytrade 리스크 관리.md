---
id: legacy_wiki_copytrade_59552d
title: Copytrade 리스크 관리
type: concept
status: verified
created_at: '2026-04-09T14:10:10Z'
last_updated: '2026-04-09T23:19:48Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages: []
tags:
- concept
sources:
- url: https://miraclehub.tistory.com/entry/%ED%88%AC%EC%9E%90-%EB%A6%AC%EC%8A%A4%ED%81%AC-%EA%B4%80%EB%A6%AC-%EB%B0%A9%EB%B2%952026-2%EC%9B%94-%EA%B8%B0%EC%A4%80
- url: https://www.copytrade.net/documentation
- url: https://copytrade.co.kr/
- url: https://help.polymarket.com/en/articles/13364163-geographic-restrictions
- url: https://errante.com/wp-content/uploads/2024/02/Errante-CopyTrading-Manual.pdf
---
# Copytrade 리스크 관리

## 요약

<!-- para: para_001 -->
> Copytrade(카피트레이드)에서 따라 거래할 때의 주요 리스크와 실무적 관리 방안 정리

<!-- para: para_002 -->
Copytrade는 다른 트레이더의 포지션과 행보를 따라가는 전략으로, 알파를 얻는 동시에 추종자(팔로워)로서 고유한 리스크가 존재한다. 본 문서에서는 기존 항목을 보강하고 실무에서 바로 적용 가능한 예시와 모니터링 규칙을 추가한다.

<!-- para: para_003 -->
- 문제: 리더보드 상위 트레이더가 일시적 이벤트, 내부정보, 혹은 감정적 거래로 비합리적 포지션을 취할 수 있음. - 대응:
  - 트레이더의 행동 패턴(평균 보유기간, 손절/익절 빈도, 이벤트 중심 거래 여부)을 정량화하여 "신뢰 점수(Trust Score)"를 부여한다.

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

## 세부 내용

<!-- para: para_008 -->
Polymarket Help Center의 지리적 제한 안내 문서로, 규제 요건과 국제 제재 준수를 이유로 Polymarket이 이용 불가한 국가·지역을 설명한다. 33개 국가가 전면 차단되며, 캐나다 Ontario와 우크라이나의 Crimea, Donetsk, Luhansk 같은 일부 지역도 제한된다. 예시로 Ontario에서는 거래와 입금이 불가하고, Italy에서는 거래가 제한되며, Germany에서는 거래가 금지되지만 기존 포지션은 시장 정산까지 보유할 수 있다. 또한 Singapore, Poland, Thailand, Taiwan은 close-only 상태로 설명되며, 여행 중인 사용자는 물리적 위치 기준으로 비제한 지역에 있으면 거래할 수 있다고 안내한다. 차단 사유로는 OFAC 제재, 추가 규제 제한, 현지 금융·도박·예측시장 법규, AML 및 KYC 요구사항을 든다.

<!-- para: para_009 -->
카피트레이딩 & FX 자동매매 플랫폼 — copytrade.co.kr

FX마진, 아직도 밤새워 차트 보시나요? 이제 카피트레이딩으로 전문가 매매를 그대로 복제하세요.

<!-- para: para_010 -->
Documentation - Comprehensive Guide for Copy Trading Success

What is CopyTrade? CopyTrade is a platform for copy (mirror) trading.

<!-- para: para_011 -->
미라클허브 님의 블로그
홈
태그
방명록
금융•보험(카드, 대출, 투자) 정보
투자 리스크 관리 방법(2026 .2월 기준)
정보공유마당
2026. 2.

<!-- para: para_012 -->
원문 PDF 바이너리 덤프는 사용자용 위키에서 제거했다. 해당 자료는 카피트레이딩 서비스 설명서와 위험 고지, 주문 복제 방식 같은 운영 정보를 담은 PDF다.
