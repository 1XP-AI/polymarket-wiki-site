---
title: "Copytrade-리더보드-심화"
category: "strategy"
created: "2026-04-05"
sources:
  - url: "https://data.polymarket.com/leaderboard"
    added: "2026-04-07"
  - url: "https://gamma-api.polymarket.com/markets"
    added: "2026-04-07"
  - url: "https://polymarketanalytics.com/traders"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://www.predictengine.ai/blog/how-to-use-polymarket-leaderboard"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://laikalabs.ai/prediction-markets/top-polymarket-traders"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://merlin.trade/leaderboard"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
  - url: "https://data-api.polymarket.com/v1/leaderboard"
    raw: "raw/fetched/2026-04-05-leaderboard-monthly.md"
    added: "2026-04-07"
  - url: "https://polyburg.com/polymarket-top-traders"
    raw: "raw/fetched/2026-04-07-leaderboard-and-risk.md"
    added: "2026-04-07"
related:
  - "[[트레이더/리더보드/데이터]]"
  - "[[전략/Copytrade/자동화-플로우]]"
  - "[[전략/Copytrade/포지션-사이즈-전략]]"
  - "[[전략/Copytrade/리밸런싱]]"
  - "[[전략/Copytrade/실행-비용]]"
  - "[[트레이더/리더보드-분석]]"
  - "[[전략/Copytrade/팔로우-스코어링-모델]]"
  - "[[개념/Copytrade]]"
---

# Copytrade-리더보드-심화

> 리더보드 데이터를 기반으로 Copytrade 대상을 선별·스코어링·추적하는 체계를 구축합니다. 단순 순위가 아닌 "누구를 따라 거래할 것인가"의 답을 구조화합니다.

## 내용

이 문서는 Polymarket 리더보드에서 발견되는 트레이더 기록을 심화 분석하여 Copytrade 대상 선별에 직접 활용할 수 있는 지표와 워크플로우를 제안합니다. 목적은 "누구를 따라 거래할 것인가"에 대한 의사결정을 구조화하고, 리스크 관리를 위해 정량·정성적 신호를 결합하는 것입니다.

## 1. 리더보드 데이터 소스 상세

Polymarket 리더보드는 단일 공식 엔드포인트가 아니라 여러 소스에서 각기 다른 형태로 제공됩니다.

| 소스 | URL | 특징 |
|------|-----|------|
| 공식 월간 | `https://data-api.polymarket.com/v1/leaderboard?window=monthly` | PnL 기준, 가장 공식적 |
| 공식 전체 | `https://clob.polymarket.com/rewards/leaderboard` | 리워드 기준, maker 활동 반영 |
| PolymarketAnalytics | `https://polymarketanalytics.com/traders` | 지갑별 PnL, 승률, 포지션 동시 조회 |
| PolyBurg | `https://polyburg.com/polymarket-top-traders` | 실시간 랭킹 + conviction score |
| Merlin.trade | `https://merlin.trade/leaderboard` | ROI·PnL·Volume 동시 정렬 |
| LaikaLabs | `https://laikalabs.ai/prediction-markets/top-polymarket-traders` | copy-ready 지갑 + 전략 요약 |

Copytrade 봇은 **공식 API를 폴링 기준으로 삼고**, 타 플랫폼은 교차검증용으로 활용합니다. `data-api.polymarket.com`의 `window` 파라미터(all/daily/weekly/monthly)를 활용해 기간별 스냅샷을 수집합니다.

### 실제 리더보드 스냅샷 예시 (2026-04-05 월간)

raw/fetched/2026-04-05-leaderboard-monthly.md에서 상위 10위:

| 순위 | 지갑 | PnL | 거래량 | PnL/Vol 비율 |
|------|------|-----|--------|-------------|
| 1 | 0x4924...3782 | $848,046 | $823,673 | 103% |
| 2 | Countryside | $666,795 | $21,585 | 3,089% |
| 3 | BBPK | $356,683 | $1,322,967 | 27% |

**해석 키워드**: PnL/Vol 비율이 100%를 초과하면 소수 대형 베팅에서 적중, 낮으면 고빈도 소규모 거래형입니다. Copytrade 관점에서는 전자가 신호당 기대수익은 높으나 샘플 리스크가 크고, 후자는 일관성은 높으나 [[전략/Copytrade/실행-비용]](슬리피지+수수료) 누적 영향을 더 받습니다. 자세한 분석은 [[트레이더/0x492442eab586f242b53bda933fd5de859c8a3782]] 참조.

## 2. 핵심 지표 제안 및 계산 방법

각 지표를 계산하는 구체적인 방법을 제시합니다.

### 2.1 단기 성과 지표

```
30일 수익률 = (현재 지갑 가치 - 30일 전 지갑 값) / 30일 전 지갑 값
승률(30일) = (수익 거래 수) / (총 거래 수)
기대값(EV) = (승률 × 평균승폭) - ((1-승률) × 평균패폭)
```

- **Copytrade 필터**: 30일 수익률 > 0 AND 거래수 >= 10
- EV > 0.05(5%) 이상이면 "신호당 기대 긍정"으로 분류

### 2.2 일관성 지표

```
샤프 비율(30일) = (일평균수익 - 무위험금리) / 일수익표준편차
승률 std = rolling 7일 승률의 표준편차
```

- 승률 std < 15%: tinggi nhất quán
- 샤프 > 1.0: 위험조정 수익 양호
- 샤프 < 0.5: 변동성 대비 수익 부족

### 2.3 유동성 적합성

```
유동성 비중 = 평균 포지션 크기 / 대상 마켓 유동성
```

- 비중 > 30%: 해당 트레이더가 진입하면 [[전략/Copytrade/시장-충격-측정]]에서 정의한 즉시 충격이 3-5¢ 이상 발생 가능
- Copytrade 시 포지션 스케일링 필수: 원 크기의 10-30%만 복제

### 2.4 행태 신호

- **진입-청산 간격**: 평균 보유기간이 1일 미만이면 고빈도 스캘퍼 → 추종 지연 치명적
- **리밸런싱 패턴**: 같은 마켓에서 반복 진입/청산하면 시장 타이밍 능숙도 신호
- **다중 마켓 동시 진입**: 3개 이상 마켓 동시 보유 시 분산 능력 or 집중도 부족 판단 필요

### 2.5 신뢰성 스코어

```
신뢰성 = 프로필 공개성(0/1) + 소셜 연계(0/1) + 활동 지속성(0-1)
활동 지속성 = min(최근활동일수 / 90, 1.0)
```

PolyVerify(`https://www.polyverify.com/leaderboard`) 같은 도구로 지갑 소유자 검증이 가능한 경우 신뢰성을 상향 조정합니다.

## 3. 스코어링 및 필터 — 3단계 워크플로우

### 단계 1: 하드 필터 (자동 제외)

- 최근 30일 거래수 < 5 → 제외 (표본 부족)
- 최근 7일 활동 없음 → 일시 보류
- 평균 포지션 / 마켓 유동성 > 50% → 제외 (시장 충격 과도)
- PnL < -$10,000 (30일 기준) → 제외

### 단계 2: 정량 스코어링

[[전략/Copytrade/팔로우-스코어링-모델]]의 가중치를 참고하되, 리더보드 특화 가중치:

```
Leaderboard Score = 0.35 × 수익률_z + 0.25 × 샤프_z + 0.20 × 일관성_z + 0.10 × 유동성 적합성 + 0.10 × 신뢰성
```

z-score 정규화 후 0-100 점수화.

### 단계 3: 정성 검증 (인간 검토)

- 프로필 공개 여부: 트위터/블로그/디스코드 활동 확인
- 전략 일관성: 정치 전문 vs 크립토 전문 vs 올라운더
- "Copytrade Wars" 현상([[개념/Copytrade]]): 상위 트레이더가 추종자를 의식해 지갑 변경, 전략 은닉 가능성

## 4. 조작 탐지와 예외 케이스

리더보드 상위권이 항상 Copytrade 적합하지는 않습니다.

| 함정 유형 | 패턴 | 탐지 방법 |
|-----------|------|-----------|
| 일회성 대형 적중 | 1-2개 거래가 전체 PnL의 80%+ | 개별 거래 기여도 분석 |
| 인셀 거래 (wash) | 자기 지갑 간 거래로 volume Inflate | 상대방 지갑 클러스터링 |
| 이벤트 직전 몰빵 | 마감 1시간 전 대량 진입 | 진입-마감 간격 히스토그램 |
| 고레버리지 도박 | 소수 베팅에 자본 대부분 노출 | 포지션 크기 집중도(Gini) |

자세한 탐지 기법은 [[전략/Copytrade/리더보드-조작-탐지]] 참조.

## 5. 운영 워크플로우

```
주간 루틴:
  1. data-api에서 leaderboard 스냅샷 수집 (all/daily/weekly/monthly)
  2. 기존 추적 트레이더와 비교 → 신규 진입/상위권 이탈 탐지
  3. 하드 필터 적용 → 후보풀 압축
  4. 정량 스코어 계산 → Top 20 선별
  5. 정성 검증(프로필, 소셜, 전략 일관성) → Top 10 확정
  6. Top 10을 [[전략/Copytrade/자동화-플로우]]에 등록

일일 루틴:
  1. 추적 중 트레이더 성과 체크
  2. score 급락(20%p 이상) 시 경고
  3. 하드 중단 조건 충족 시 자동 Follow 중지
```

## 6. 리더보드 API 폴링 구현

```python
import requests
from datetime import datetime

LEADERBOARD_URL = "https://data-api.polymarket.com/v1/leaderboard"

def fetch_leaderboard(window="monthly", limit=50):
    resp = requests.get(
        LEADERBOARD_URL,
        params={"window": window, "limit": limit},
        timeout=10
    )
    resp.raise_for_status()
    return resp.json()

def snapshot_and_save():
    data = fetch_leaderboard()
    timestamp = datetime.utcnow().isoformat()
    traders = []
    for t in data.get("leaderboard", []):
        traders.append({
            "rank": t.get("rank"),
            "address": t.get("address"),
            "pnl": t.get("pnl"),
            "volume": t.get("volume"),
            "timestamp": timestamp
        })
    # TODO: Save to raw/fetched/YYYY-MM-DD-leaderboard-{window}.md
    return traders
```

rate limit(초당 5-10회)을 고려해 폴링 간격을 5분 이상으로 설정합니다.

## 7. 관련 문서 간 연결 가이드

| 읽을 문서 | 얻을 것 | 다음 단계 |
|-----------|---------|----------|
| [[트레이더/리더보드/데이터]] | 리더보드 원자료, API 스펙 | → 본 문서의 스코어링 |
| [[트레이더/리더보드-분석]] | 리더보드 분석 프레임워크, 플랫폼 비교 | → 본 문서의 조작 탐지 |
| [[전략/Copytrade/팔로우-스코어링-모델]] | 팔로우 대상 점수화 알고리즘 | → 본 문서 Leaderboard Score |
| [[전략/Copytrade/자동화-플로우]] | 실제 실행 파이프라인 | → 스코어 기반 자동 등록 |
| [[개념/Copytrade]] | Copytrade 전체 개념·가중치 최적화 | → 전후 맥락 |
| [[전략/Copytrade/실행-비용]] | 슬리피지·수수료 영향 분석 | → 유동성 필터 임계값 |
| [[전략/Copytrade/포지션-사이즈-전략]] | 포지션 크기 결정 | → 사이징 규칙 |
| [[전략/Copytrade/리밸런스]] | 가중치 동적 조정 | → 주기적 Score 재계산 |

## 관련 문서

- [[트레이더/리더보드/데이터]] — 리더보드 원자료 및 수집 스펙
- [[트레이더/리더보드-분석]] — 리더보드 분석 프레임워크, 3단계 필터
- [[전략/Copytrade/자동화-플로우]] — 전략적 배분과 리스크 관리 관점 연결
- [[전략/Copytrade/포지션-사이즈-전략]] — 포지션 산정 상세 가이드
- [[전략/Copytrade/실행-비용]] — 실행 비용 정량화 가이드
- [[전략/Copytrade/팔로우-스코어링-모델]] — Laplace smoothing, 가중치 프로파일
- [[개념/Copytrade]] — Copytrade 개념 전반, 가중치 최적화
- [[전략/Copytrade/리더보드-조작-탐지]] — wash trading, PnL 조작 패턴
