---
id: legacy_wiki_copytrade_3f7013
title: 청산 전략(Exit Rules)
type: concept
status: verified
created_at: '2026-04-09T14:10:11Z'
last_updated: '2026-04-09T16:13:32Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_copytrade_copytrade_5e34e9
- legacy_wiki_copytrade_eff435
tags:
- concept
sources:
- url: https://viewpoint.pwc.com/dt/gx/en/pwc/industry/industry_INT/industry_INT/real_estate__1_INT/Applying-IFRS-for-the-real-est/5-Real-estate-structures-and-tax-considerations/51-Consolidation/512-Definition-of/5123-Exit-strategy.html
- url: https://www.imidaily.com/europe/germanys-overlooked-exit-rule-men-aged-17-to-45-now-need-bundeswehr-permission-to-leave/
- url: https://portal.mexem.com/ko/trading/exit-strategy.php
- url: https://www.thegoodreview.com.au/2026/03/trust-company-exit-%EC%A0%84%EB%9E%B5-%EC%99%84%EC%A0%84-%EA%B0%80%EC%9D%B4%EB%93%9C-2026/
- url: https://blog.naver.com/topbuilding/223856763062
---
# 청산 전략(Exit Rules)

## 요약

<!-- para: para_001 -->
> 한 줄 요약: Copytrade에서 추종한 포지션의 손절·목표·자동 중단 규칙을 체계화하여 리스크를 통제하는 실전 가이드입니다.

<!-- para: para_002 -->
Copytrade는 타인의 포지션을 복제하는 특성상 진입보다 청산(Exit) 규칙이 더 중요합니다. 청산 규칙은 손절(stop-loss), 부분 청산(scale-out), 이익 실현(take-profit), 그리고 추종 중단(follow-stop)으로 구성되어야 합니다.

<!-- para: para_003 -->
- 포지션별 최대 손실 한도(MDD per position)를 미리 정한다 (예: 카피비율 기준 -5%). - 시장 유동성과 슬리피지를 고려해 스탑 주문과 시장가 주문의 조합을 사용한다.

<!-- para: para_004 -->
1) 손절(Stop-loss): 진입 가격 대비 -6% 도달 시 지정가로 부분(50%) 청산, -10% 도달 시 전부 청산. 2) 이익 실현(Take-profit): +12% 달성 시 30% 부분 청산, +25% 달성 시 추가 청산. 3) 트레이더 성과 기반 추종 중단(Follow-stop): 해당 트레이더의 30일 누적 수익률이 -8% 이하로 내려가면 신규 진입 중단 및 보유 포지션을 지정된 비율(예: 30%)로 축소.

<!-- para: para_005 -->
- 주문 지연(latency)과 슬리피지를 줄이기 위해 WebSocket 이벤트 기반으로 트리거하고, 제출 시 가격 한도(limit)과 허용 슬리피지 범위를 함께 검증한다. - 백테스트를 통해 각 손절·이익 실현 임계값의 기대 성과(Sharpe, Win-rate, MDD)를 검증한다. - 여러 트레이더를 팔로우하는 경우 포지션 사이즈를 동적 재조정(리밸런싱)하여 포트폴리오 수준의 손실 한도를 유지한다.

<!-- para: para_006 -->
- 신규 트레이더 A를 1:100 비율로 복제. 진입 후 -7% 하락 발생 → 자동으로 50% 청산(지정가), 이후 추가 하락 시 전체 청산. 트레이더 A의 30일 누적손실이 -12%로 떨어지면 추종 중단 규칙 발동.

<!-- para: para_007 -->
- [[Copytrade 데이터 수집 가이드]] — 포지션 크기 및 청산 타이밍의 연계
- [[Copytrade 데이터 수집 가이드]] — 포트폴리오 레벨 리스크 한도 설정
- [[Copytrade 데이터 수집 가이드]] — 트레이더 성과 기반 중단 규칙

## 세부 내용

<!-- para: para_008 -->
금융 분석가 마에스의 시선 : 네이버 블로그

<!-- para: para_009 -->
Trust & Company Exit 전략 완전 가이드 2026
콘텐츠로 바로가기
더굿리뷰 – The Good Review
온라인 광고, SEO, 웹사이트, 여행, 맛집, 호주, 시드니, 전화번호, 교민업소, 리뷰의 모든 것
메뉴
홈
About Us
호주 교민 업소록
맛집
제품/상품
WordPress
IT 트렌드
한국뉴스
Contact US
로그인
더굿리뷰 - The Good Review
>
호주생활
>
Trust & Company Exit 전략 완전 가이드 2026
작성일자
2026-03-03
2026-03-03
글쓴이
더굿리뷰
Trust & Company Exit 전략 완전 가이드 2026
이 글은 Trust & Company 전체 구조 전략의 마무리 단계입니다. 기초 구조는
Family Trust 가이드
,
고소득 전략은
고소득 사업자 구조 설계
,
유보 전략은
Bucket Company 전략
,
리스크 관리는
Division 7A 해설
을 먼저 참고하세요.

<!-- para: para_010 -->
청산 전략 | Interactive Brokers LLC
정치, 경제 및 기후 예측 계약 실시간 확인 -
고객 로그인
|
시장 보기
|
더 알아보기
개인
개인, 공동 명의 또는 퇴직
비전문 어드바이저
기관
기관 홈
어드바이저 계좌
등록된 투자 어드바이저
패밀리 오피스
기관 계좌
프랍 트레이딩 그룹
헤지 펀드
소개 증권사
중소기업
머니 매니저
행정/관리 계좌
컴플라이언스 관리자
직원 플랜 관리자
SIMPLE IRA
풀-서비스 관리자
보험 제공자
펀드 관리자
헤지 펀드 할당자 (Hedge Fund Allocator)
기타 계좌
교육 기관
무료 체험
채용
회사 소개
강점 및 보안
정보 및 이력
수상 경력
IBKR 뉴스
언론 및 미디어
IR (기업 활동)
소셜 미디어의 IBKR
지속 가능성
규제 보고서
친구 추천
제휴 프로그램
이용 안내/지원
IBKR FeatureExplorer
계좌 이체
개인
계좌
기관 판매 연락처
자주 묻는 질문 (FAQ)
세금 정보
언어
English
Español
Português
한국어
中文简体
中文繁體
Interactive Brokers 홈
계좌 개설
Log In
왜 IBKR인가
가격
수수료
신용 융자 금리
이자율
공매도 비용
리서치 및 뉴스
마켓 데이터 가격 책정
주식 수익률 향상 프로그램
기타 수수료
트레이딩
플랫폼
API
증거금
기호 및 거래소 검색
상품 개요
주문 유형
보고
증권 대차
주요 기능
확률 랩 (Probability Lab)
글로벌 아웃소싱 트레이딩 데스크
지속 가능한 투자
IBKR 예측 트레이더 (ForecastTrader)
서비스
IBKR 글로벌 애널리스트
포트폴리오 애널리스트
채권 마켓 플레이스
뮤추얼 펀드 마켓플레이스
거래 수수료 없는 ETF
투자자 마켓 플레이스
공매도 증권
통합 현금 관리
타사 통합
인터렉티브 어드바이저 (Interactive Advisors)
교육
IBKR 캠퍼스
트레이더 아카데미
트레이더 인사이트
IBKR 팟캐스트
IBKR 퀀트 블로그
웹 세미나
트레이딩 랩
트레이더 용어사전
트레이더 캘린더
검색
로그인
포털 로그인
IBKR 데스크탑 다운로드
트레이더 워크스테이션 다운로드
IBKR 모바일 다운로드
IB Gateway 다운로드
모든 IBKR 플랫폼 비교
IBKR 예측 트레이더 (ForecastTrader)
계좌 개설
회원 가입
회원 가입 완성
필요한 서류 목록
본인에게 적합한 계좌를 선택하기 위한 가이드
Interactive Brokers 홈
포털 로그인
계좌 개설
뒤로 가기
계좌 개설
등록 시작
회원 가입 완성
필요한 서류 목록
본인에게 적합한 계좌를 선택하기 위한 가이드
IBKR 예측 트레이더 (ForecastTrader)
무료 체험
왜 IBKR인가
계좌 종류
뒤로 가기
개인
개인, 공동명의 또는 퇴직
비전문 어드바이저
기관
기관 홈
어드바이저 계좌
등록된 투자 어드바이저 (RIA)
패밀리 오피스
기관 계좌
프랍 트레이딩 그룹
헤지 펀드
소개 증권사
중소 기업
머니 매니저
행정/관리 계좌
컴플라이언스 관리자
직원 플랜 관리자
SIMPLE 퇴직 계좌 (IRA)
풀-서비스 관리자
보험업자
펀드 관리자
헤지펀드 할당자
기타 계좌
교육 기관
가격
뒤로 가기
가격
수수료
신용 융자 금리
이자율
공매도 비용
리서치 및 뉴스
마켓 데이터 가격
주식 수익률 향상
기타 수수료
트레이딩
뒤로 가기
트레이딩
플랫폼
API
증거금
기호 및 거래소 검색
금융 상품 개요
주문 유형
보고서
증권 대차
주요 기능 설명
확률 랩
글로벌 아웃소싱 트레이딩 데스크
지속 가능한 투자
IBKR 예측 트레이더 (ForecastTrader)
서비스
뒤로 가기
서비스
IBKR 글로벌 애널리스트
포트폴리오 애널리스트
채권 마켓플레이스
뮤추얼 펀드 마켓플레이스
거래 수수료가 없는 ETF
투자자 마켓플레이스
공매도 증권
통합 현금 관리
타사 통합
인터렉티브 어드바이저
교육
뒤로 가기
교육
IBKR 캠퍼스
트레이더스 아카데미
트레이더스 인사이트
IBKR 팟캐스트
IBKR 퀀트 블로그
웹 세미나
트레이딩 랩
트레이더 용어 사전
트레이더 캘린더
회사 소개
뒤로 가기
회사 소개
강점과 보안
정보와 역사
채용
수상 이력
IBKR 새소식
언론과 미디어
IR (기업 활동)
소셜 미디아의 IBKR
지속가능한 성장
규제 보고서
친구 소개
제휴 프로그램
이용 안내/지원
뒤로 가기
이용 안내/지원
IBKR 기능 익스플로러 (FeatureExplorer)
계좌 이체
개인
기관
기관 판매 부서 연락처
자주 묻는 질문 (FAQ) 검색
세금 정보
언어
뒤로 가기
언어
English
Español
Português
한국어
中文简体
中文繁體
Privacy Preference Center
This website uses cookies to offer a better browsing experience and to collect usage information. By clicking on the "ACCEPT COOKIES" button you accept our Cookie Policy.

<!-- para: para_011 -->
5.1.2.3. Exit strategy
Menu
Latest updates
Latest updates
What's new on Viewpoint?

<!-- para: para_012 -->
Germany's Overlooked Exit Rule: Men Aged 17 to 45 Now Need Bundeswehr Permission to Leave - IMI Daily
Skip to content
Search
About
Articles
Regions
Africa
Asia Pacific
Caribbean
Europe
Latin America
MENA
North America
Intel & Data
Policy Updates
Industry Trends
Opinion
Tax
10 On The Weekend
Analysis
IM People in The News
Partner Content
Events
Barcelona 2026
Find a Pro
Partners
3 Comma Capital
Ariete Capital
Arish Capital Partners
Arton Capital
Beyond Global Partners
CIP Turkey
ClientReferrals
EC Holdings
EDICR
Empowered Startups
EU Law Firm
Georgaki Law Firm
Get Golden Visa
Globevisa Group
Grupo Los Pueblos
GSC International
Joseph Rowe Law
Latitude Group
Mercan Group
MIBS Group
NTL Trust
OIKOS Property Developments
Optimize Investment Partners
Optylon Krea
Orience
Passport Legacy
Prime Developments
Vardikos & Vardikos
Vignale Capital
World Talents
Programs
Promote
Real Estate
Resources
Approved CBI Agents
Blacklisted CBI Agents
Caribbean CBI Documentaries
CBI Banned Nationalities
CBI Transparency Index
Digital Nomad Visas
EU Citizenship by Descent
History of CBI
Investment Migration Books
Jobs
My Sovereign Score
Portugal Golden Visa Funds​
Settlement Blocs
Subscribe to the Newsletter
IMI Pro
Become a Pro
My IMI Pro Profile
IMI Pro Dashboard
Log In
Pro Tools
IMI Rolodex
IMI Data Center
IMI Private Briefings
IMI Citizenship Catalog
IMI RCBI Processing Times
About
Articles
Regions
Africa
Asia Pacific
Caribbean
Europe
Latin America
MENA
North America
Intel & Data
Policy Updates
Industry Trends
Opinion
Tax
10 On The Weekend
Analysis
IM People in The News
Partner Content
Events
Barcelona 2026
Find a Pro
Partners
3 Comma Capital
Ariete Capital
Arish Capital Partners
Arton Capital
Beyond Global Partners
CIP Turkey
ClientReferrals
EC Holdings
EDICR
Empowered Startups
EU Law Firm
Georgaki Law Firm
Get Golden Visa
Globevisa Group
Grupo Los Pueblos
GSC International
Joseph Rowe Law
Latitude Group
Mercan Group
MIBS Group
NTL Trust
OIKOS Property Developments
Optimize Investment Partners
Optylon Krea
Orience
Passport Legacy
Prime Developments
Vardikos & Vardikos
Vignale Capital
World Talents
Programs
Promote
Real Estate
Resources
Approved CBI Agents
Blacklisted CBI Agents
Caribbean CBI Documentaries
CBI Banned Nationalities
CBI Transparency Index
Digital Nomad Visas
EU Citizenship by Descent
History of CBI
Investment Migration Books
Jobs
My Sovereign Score
Portugal Golden Visa Funds​
Settlement Blocs
Subscribe to the Newsletter
IMI Pro
Become a Pro
My IMI Pro Profile
IMI Pro Dashboard
Log In
Pro Tools
IMI Rolodex
IMI Data Center
IMI Private Briefings
IMI Citizenship Catalog
IMI RCBI Processing Times
Europe
April 4, 2026
Germany’s Overlooked Exit Rule: Men Aged 17 to 45 Now Need Bundeswehr Permission to Leave
Buried clause in December's military reform requires Bundeswehr approval for extended male absences; dual nationals included, enforcement mechanisms remain undefined. Ahmad Abbas
IMI
• Amman
Since January 1, Germany has required that men between the ages of 17 and 45 obtain permission from a
Bundeswehr
Career Center before leaving the country for more than three months.
