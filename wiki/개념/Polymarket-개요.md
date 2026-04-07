---

title: "Polymarket 개요"
category: "개념"
created: "2026-04-05"
sources:
  - url: "https://gamma-api.polymarket.com/events"
    raw: "raw/fetched/2026-04-05-polymarket-events.md"
    added: "2026-04-05"
  - url: "https://gamma-api.polymarket.com/markets"
    raw: "raw/fetched/2026-04-05-polymarket-markets.md"
    added: "2026-04-05"
  - url: "https://polymarket.com/"
    raw: "raw/fetched/2026-04-05-polymarket-home.md"
    added: "2026-04-05"
  - url: "https://polymarket.com/faq"
    raw: "raw/fetched/2026-04-05-polymarket-faq.md"
    added: "2026-04-05"
  - url: "https://gamma-api.polymarket.com/leaderboard"
    raw: "raw/fetched/2026-04-05-polymarket-leaderboard-api.md"
    added: "2026-04-05"
related:
  - "[[전략/Copytrade/전략분석]]"
  - "[[Polymarket-API-레퍼런스]]"
  - "[[CLOB]]"
  - "[[리더보드-트레이더-데이터]]"
  - "[[Theo]]"
  - "[[기술/Polymarket/개요.md]]"
---

# Polymarket 개요

> Polymarket와 예측 시장의 핵심 구조 및 copytrade 관점에서의 주요 고려사항을 정리합니다.

## 플랫폼 구조 요약

Polymarket은 사건 결과에 베팅하는 예측시장(prediction market) 플랫폼입니다. 각 마켓은 Yes/No 또는 다중 아웃컴(outcome)을 가지며, 가격은 해당 결과의 암묵적 확률을 반영합니다. 온체인/오프체인 혼합 구조를 사용하고, 마켓 토큰은 CTF(Conditional Token Framework)로 표현될 수 있습니다(예: [[CTF]]).

- 주문 방식: 주문장(orderbook, CLOB) 기반 매칭과 AMM/스왑형 모델이 혼재할 수 있음
- 자산: 주로 USDC.e 등 스테이블코인으로 결제
- 온체인 요소: 포지션 토큰(ERC-1155), 스플릿/머지/리뎀트 흐름(보상/상환)

추가 플랫폼 특징:

- 네트워크: Polygon 기반으로 운영되며, 가스비·확정성 측면에서 경량화된 온체인 흐름을 제공합니다.
- 가격 표현: 마켓 가격은 0.00–1.00 범위로 표시되며, 표시된 가격은 암묵적 확률로 해석됩니다(예: 0.72 → 약 72%).
- 리소스 분리: Gamma API(마켓/이벤트/프로필), Data API(포지션·트레이드·리더보드), CLOB API(오더북·주문) 등 용도별 엔드포인트로 분리되어 있어 데이터 접근 경로가 명확합니다.
- 정산: 포지션 토큰은 결과에 따라 $1.00 또는 $0.00로 정산되며, 승리 토큰을 Redeem하여 자산을 회수합니다.

## 마켓·오더 유형 상세

- CLOB(중앙 주문장): 지정가 주문으로 시장에 유동성을 제공. 복잡한 체결 규칙과 리베이트/수수료 정책이 적용될 수 있어 고빈도 추종자에게 유리하거나 불리할 수 있음(리베이트 존재 시 유리).
- AMM/스왑형: 즉시 체결을 위한 유동성 풀 기반. 슬리피지 비용이 체결량에 따라 비선형적으로 증가.
- Split/Merge 워크플로우: 온체인 포지션 토큰을 생성/병합하여 포지션을 관리. 가스비와 트랜잭션 지연이 발생할 수 있음.

(관련: [[CLOB]], [[CTF]])

## 수수료·실행비용 분석 (추정 예시)

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

## Copytrade에서의 시사점 및 권장 실무

- 대상 선정: 리더보드·포지션·승률 등 계량지표로 후보를 선별하되, 과거 성과의 표본오차와 조작 가능성을 고려(자세한 선별 기준은 [[Copytrade-초기-선별-가이드]] 참조).
- 포지션 사이징: 자본 대비 가중치를 계산해 거래당 비용을 상쇄하고도 의미있는 기대수익을 확보할 수 있도록 설정.
- 실행 속도 최적화: 추종 지연(follow-execution delay)은 성과에 큰 영향을 줌. 가능한 자동화, 낮은 레이턴시 엔드포인트(CLOB API) 사용 권장(관련: [[전략/Copytrade/추종-실행-속도-최적화]]).
- 비용 관찰: 실거래 전 시뮬레이션(백테스트)으로 누적 비용을 포함한 기대 수익률을 검증(관련: [[백테스트-가이드]]).
- 리스크 완화: 최대 익스포저 한도, 추종 중단 규칙(예: 연속 손실 n회 시 정지), 포지션 캡 등 자동화 규칙 적용(관련: [[전략/Copytrade/추종-중단-규칙]], [[전략/Copytrade/리스크-관리]]).
- 모니터링: 리더보드 조작 탐지, 오라클 지연/결정 오류 모니터링, 비정상 트랜잭션 감지(관련: [[리더보드-조작-탐지]], [[전략/Copytrade/리스크-시나리오]]).

## API 예제 및 데이터 활용

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

- 데이터 팁: 리더보드와 트레이드/포지션 API를 교차 분석해 트레이더의 거래주기, 평균 포지션 크기, 승률 등을 산출하면 선별 품질을 높일 수 있음(관련: [[리더보드-트레이더-데이터]], [[데이터/수집-파이프라인]]).

## 주요 리스크 포인트

- 대형 베팅(Whale)으로 인한 시장 충격
- 리더보드 조작 또는 가짜 활동
- 이벤트 확정 지연이나 오라클 오류(결과 확정 지연)

리스크 관리 기법은 [[전략/Copytrade/리스크-관리]] 및 [[전략/Copytrade/리스크-시나리오]] 문서를 참고해 적용해야 합니다.

## 관련 및 연계 문서

- [[CTF]] — 마켓의 온체인 토큰 표현
- [[CLOB]] — 주문장 기반 거래와 가격 형성
- [[전략/Copytrade/전략분석]] — 추종 전략과 성과 비교
- [[리더보드-트레이더-데이터]] — 트레이더 데이터 수집 및 지표
