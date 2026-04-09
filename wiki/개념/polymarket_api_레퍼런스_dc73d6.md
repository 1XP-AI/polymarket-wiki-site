---
id: legacy_raw_02_api_fbe99e
title: Polymarket API 레퍼런스
type: concept
status: draft
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-09T14:10:08Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 1
evidence_coverage: 1.0
confidence: medium
related_pages:
- source_summary_src_raw_02_api_md_fbe99e01
tags:
- concept
- internal
---

# Polymarket API 레퍼런스

## 요약

<!-- para: para_001 -->
> 출처: docs.polymarket.com API Reference (2026-04-04 수집)

## 핵심 사실

<!-- para: para_002 -->
- **Public (인증 불필요)**: 마켓 데이터 조회, 가격 조회, 오더북 조회
- **L1 Auth (지갑 서명만)**: 초기 설정, API 키 생성
- **L2 Auth (API 키)**: 주문 생성/취소, 트레이드 조회, 포지션 관리

<!-- para: para_003 -->
```
POLY_ADDRESS: 지갑 주소
POLY_SIGNATURE: 서명
POLY_TIMESTAMP: 타임스탬프
POLY_NONCE: 논스
POLY_API_KEY: API 키
POLY_PASSPHRASE: 패스프레이즈
```

## 세부 내용

<!-- para: para_004 -->
모든 엔드포인트에 속도 제한 적용. 자세한 수치는 공식 문서 참조. ---

<!-- para: para_005 -->
| 엔드포인트 | 메서드 | 설명 |
|-----------|--------|------|
| `/events` | GET | 이벤트 목록 조회 |
| `/events/{id}` | GET | ID로 이벤트 조회 |
| `/events/slug/{slug}` | GET | Slug로 이벤트 조회 |
| `/events/{id}/tags` | GET | 이벤트 태그 조회 |

<!-- para: para_006 -->
| 엔드포인트 | 메서드 | 설명 |
|-----------|--------|------|
| `/markets` | GET | 마켓 목록 조회 |
| `/markets/{id}` | GET | ID로 마켓 조회 |
| `/markets/slug/{slug}` | GET | Slug로 마켓 조회 |
| `/markets/{id}/tags` | GET | 마켓 태그 조회 |

<!-- para: para_007 -->
| 엔드포인트 | 메서드 | 설명 |
|-----------|--------|------|
| `/book` | GET | 오더북 조회 (단일 토큰) |
| `/books` | POST | 오더북 조회 (다수 토큰) |
| `/price` | GET | 시장 가격 조회 |
| `/prices` | GET/POST | 다수 토큰 가격 조회 |
| `/midpoint` | GET | 미드포인트 가격 |
| `/midpoints` | GET/POST | 다수 미드포인트 |
| `/spread` | GET | 스프레드 조회 |
| `/spreads` | POST | 다수 스프레드 |
| `/last-trade-price` | GET | 최종 거래 가격 |
| `/prices-history` | GET | 가격 히스토리 |
| `/batch-prices-history` | POST | 다수 마켓 가격 히스토리 |
| `/fee-rate` | GET | 수수료율 조회 |
| `/tick-size` | GET | 최소 가격 단위 조회 |
| `/time` | GET | 서버 시간 |

## 열린 질문

<!-- para: para_008 -->
Pending review.

## 관련 페이지

<!-- para: para_009 -->
소스 요약: source_summary_src_raw_02_api_md_fbe99e01
