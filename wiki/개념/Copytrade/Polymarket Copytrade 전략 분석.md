---
id: legacy_raw_03_copytrade_c17abe
title: Polymarket Copytrade 전략 분석
type: concept
status: verified
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-09T17:13:11Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 6
evidence_coverage: 1.0
confidence: medium
related_pages: []
tags:
- concept
sources:
- url: https://www.ai-polymarket.com/polytrader/copy-trading.html
- url: https://polynoob.com/copytrading-on-polymarket/
- url: https://www.polycopytrade.net/documentation.php
- url: https://www.polycopy.dev/guides/how-to-copy-trade-polymarket
- url: https://www.holypoly.io/blog/how-to-copy-trade-polymarket
- url: https://docs.polymarket.com/
---
# Polymarket Copytrade 전략 분석

## 요약

<!-- para: para_001 -->
> 출처: Polymarket API 구조 분석 + Signal Foundry 설계 (2026-04-04)

<!-- para: para_002 -->
다른 트레이더의 거래를 **실시간으로 감지하고 따라하는** 전략. Polymarket에서는 공개 API를 통해 누구의 포지션이든 조회 가능하므로, copytrade가 기술적으로 가능하다.

<!-- para: para_003 -->
GET https://data-api.polymarket.com/v1/leaderboard
파라미터: window=all

|daily|weekly|monthly, limit, offset

- 수익률 기준 트레이더 순위
- 트레이더 지갑 주소 획득 가능
- 기간별 필터링 (전체/일간/주간/월간)

<!-- para: para_004 -->
GET https://gamma-api.polymarket.com/public-profile?address={wallet}

- 프로필 정보, 거래 통계

<!-- para: para_005 -->
GET https://data-api.polymarket.com/positions?address={wallet}

- 현재 보유 포지션 전체 조회
- 마켓별 토큰 수량, 방향 (Yes/No)

<!-- para: para_006 -->
GET https://data-api.polymarket.com/trades?address={wallet}

- 과거 거래 기록
- 체결 가격, 수량, 시간, 방향

<!-- para: para_007 -->
GET https://data-api.polymarket.com/activity?address={wallet}

- 최근 활동 (거래, 포지션 변경 등)

<!-- para: para_008 -->
GET https://gamma-api.polymarket.com/public-profile?address={wallet}

<!-- para: para_009 -->
GET https://data-api.polymarket.com/positions?address={wallet}

<!-- para: para_010 -->
GET https://data-api.polymarket.com/trades?address={wallet}

## 세부 내용

<!-- para: para_011 -->
Copy Trading on Polymarket - Automatically Follow Successful Traders Guide
PolyTrader
Home
Polycule Bot
Copy Trading
Telegram Bot
Social Trading
Home
Copy Trading
Copy Trading on Polymarket - Complete Guide
Automatically follow successful traders and mirror their trades with customizable settings and advanced filters
Start Copy Trading
What is Copy Trading? Copy trading allows you to automatically mirror the trades of successful Polymarket traders.

<!-- para: para_012 -->
How to Copy Trade on Polymarket: Step-by-Step Guide 2026 | HolyPoly
#1 prediction market data intelligence platform for professional traders
HolyPoly
Learn hub
Movers
FAQ
Spread scan
Unlock premium features
Sign in
Get Pro
How to Copy Trade on Polymarket: Step-by-Step Guide (2026)
Copy trading on Polymarket means following the same positions as top-performing wallets. This guide explains what it is, how to find the best wallets to copy, and how to get copy-ready instructions so you can place the same trades on Polymarket in under a minute.

<!-- para: para_013 -->
Documentation - Polymarket Copy Trade
Polymarket
Copy
Trade
Smart Trading Protocol
Home
Features
Top Traders
Pricing
Blog
Start Trading
Menu
Home
Features
Top Traders
Pricing
Blog
Start Trading
Documentation
Complete
User Guide
Everything you need to know to set up and optimize your automated copy trading bot. Getting Started
Quick setup guide
Wallet Setup
Connect MetaMask
Copy Trading
Configure the bot
Subscription
Plans & payments
Contents
Getting Started
Wallet Setup
Dashboard Overview
Copy Trading Bot
Wallet Tracking
Trade Settings
Trade History
Subscription Plans
Security
FAQ
Troubleshooting
Getting Started
Welcome to Polymarket Copy Trade!

<!-- para: para_014 -->
Documentation - Polymarket Copy Trade
PolyMarket
Trading
Bot
Smart Trading Protocol
Home
Features
Top Traders
How It Works
Pricing
Start Trading
Menu
Home
Features
Top Traders
How It Works
Pricing
Start Trading
Documentation
Complete
User Guide
Everything you need to know to set up and optimize your automated copy trading bot. Getting Started
Quick setup guide
Wallet Setup
Connect MetaMask
Copy Trading
Configure the bot
Subscription
Plans & payments
Contents
Getting Started
Wallet Setup
Dashboard Overview
Copy Trading Bot
Wallet Tracking
Trade Settings
Trade History
Subscription Plans
Security
FAQ
Troubleshooting
Getting Started
Welcome to Polymarket Copy Trade!

<!-- para: para_015 -->
How to Copy Trade on Polymarket — Complete Guide (2025)
POLYCOPY
Technology
Markets
Leaderboard
Guides
How It Works
Support
Get Started
Home
/
Guides
/
Copy Trade Polymarket
Beginner Guide
8 min read
Updated June 2025
How to Copy Trade on
Polymarket
A complete step-by-step guide to automatically copy the trades of top Polymarket traders. Learn how to set up copy trading for BTC, ETH, SOL, and XRP 15-minute prediction markets with sub-500ms execution speed.

<!-- para: para_016 -->
Copytrading on Polymarket | PolyNoob
PolyNoob
The Ultimate Guide to Polymarket and Beyond
Prediction Market Basics
Guides/How and Why
How to Stay Safe from Discord Scams
How to Trade in Polymarket: 4 Essential Steps Before Buying in a Prediction Market
UMA Disputes on Polymarket: How It Works
What Is a Clarification on Polymarket? What Is a Prediction Market?

<!-- para: para_017 -->
Overview - Polymarket Documentation
Skip to main content
Polymarket Documentation
home page
English
Search... ⌘
K
Changelog
Get Help
Main Site
Main Site
Search...
