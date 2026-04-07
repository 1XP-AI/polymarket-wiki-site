---
title: "Copytrade 성능 모니터링"
category: "strategy"
created: "2026-04-07"
sources:
  - url: "https://polymarketcopytrading.com/risk-management"
    added: "2026-04-07"
  - url: "https://www.polycopytrade.net/blog/polymarket-copy-trading-risk-management.php"
    added: "2026-04-07"
related:
  - "[[전략/Copytrade/리스크-모니터링]]"
  - "[[전략/Copytrade/자동화-플로우]]"
  - "[[전략/Copytrade/리스크-관리]]"
  - "[[전략/Copytrade/추종-실행-속도-최적화]]"
  - "[[전략/Copytrade/성과-분석-지표]]"
  - "[[전략/Copytrade/알고리즘-선별-체크리스트]]"
---

# Copytrade 성능 모니터링

> Copytrade 전략의 실행 품질과 트레이더 성과를 지속적으로 추적·계측하는 방법

## 핵심 모니터링 지표

1. **복제 정확도**: 원본 트레이더 포지션 대비 팔로워 포지션 일치율
2. **실행 지연**: 감지→전송→체결 각 지연 시간(ms)
3. **평균 슬리피지**: 기대가 vs 체결가 차이
4. **트레이더별 P&L**: 복제된 트레이더당 누적 수익/손실
5. **API 오류율**: CLOB/Gamma API 호출 실패 비율

## 대시보드 및 알림 설계

- **실시간**(초-분): WebSocket 기반 가격·포지션 변화 감지
- **주기적**(1시간~1일): 집계 지표 계산 및 리포트 생성
- **임계치 기반**: 복제 정확도 < 90%, API 오류율 > 5% 시 경보

## 관련 문서
- [[전략/Copytrade/리스크-모니터링]] — 실시간 리스크 지표 정의 (sim 0.7273)
- [[전략/Copytrade/자동화-플로우]] — 자동화 파이프라인과 모니터링 연동
- [[전략/Copytrade/리스크-관리]] — 리스크 정책과 연계
- [[전략/Copytrade/추종-실행-속도-최적화]] — 실행 시간 최적화
- [[전략/Copytrade/알고리즘-선별-체크리스트]] — 자동화 선별 체크리스트 (sim 0.6920)
- [[전략/Copytrade/리스크-모니터링]] — 리스크 헤징 기법 (sim 0.7386)
- [[전략/Copytrade/성과-분석-지표]] — 성과 분석 지표
