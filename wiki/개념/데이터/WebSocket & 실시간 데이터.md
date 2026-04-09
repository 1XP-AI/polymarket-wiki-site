---
id: legacy_raw_06_websocket_506430
title: WebSocket & 실시간 데이터
type: concept
status: verified
created_at: '2026-04-09T14:10:08Z'
last_updated: '2026-04-09T15:11:57Z'
as_of: '2026-04-09'
owners:
- wiki-system
source_count: 5
evidence_coverage: 1.0
confidence: medium
related_pages:
- legacy_wiki_copytrade_0c3a80
- legacy_wiki_copytrade_6a6853
tags:
- concept
sources:
- url: https://blog.naver.com/brotechtalks/224159705271
- url: https://uvicorn.dev/release-notes/
- url: https://websocket.org/reference/websocket-api
- url: https://yinternational.co.kr/websocket-%EC%8B%A4%EC%8B%9C%EA%B0%84-%ED%86%B5%EC%8B%A0%EC%9D%98-%EB%AA%A8%EB%93%A0-%EA%B2%83-http%EC%99%80%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%99%80-%ED%99%9C%EC%9A%A9-%EC%82%AC%EB%A1%80/
- url: https://developer.mozilla.org/ko/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications
---
# WebSocket & 실시간 데이터

## 요약

<!-- para: para_001 -->
> 출처: docs.polymarket.com WebSocket (2026-04-04 수집)

<!-- para: para_002 -->
Polymarket은 실시간 데이터 스트리밍을 위해 여러 WebSocket 채널을 제공한다.

<!-- para: para_003 -->
- 인증 불필요
- 실시간 오더북, 가격, 마켓 변경 데이터
- 구독할 마켓(토큰 ID)을 지정

<!-- para: para_004 -->
- 오더북 업데이트 (bid/ask 변경)
- 가격 변경
- 거래 체결
- 마켓 상태 변경

<!-- para: para_005 -->
- L2 Auth 필요
- 자신의 주문/거래 업데이트
- 주문 상태 변경 (생성, 매칭, 체결, 취소)
- 포지션 변경

<!-- para: para_006 -->
- 스포츠 경기 실시간 스코어
- 게임 상태 업데이트

<!-- para: para_007 -->
- 코멘트 스트리밍
- 크립토 가격
- 주가 (equity prices)

<!-- para: para_008 -->
- `/trades?address={wallet}` 를 주기적으로 호출

## 추가 내용

<!-- para: para_009 -->
Polymarket은 4가지 WebSocket 채널을 제공하며, 용도와 인증 요구사항이 다르다.

|채널 | 인증 | 용도 |
|------|------|------|
| Market | 불필요 | 공개 오더북·가격·거래 실시간 스트림 |
| User | L2 Auth 필요 | 개인 주문/체결/포지션 이벤트 |
| Sports | 불필요 | 스포츠 경기 스코어·상태 업데이트 |
| RTDS | 불필요 | 외부 데이터(크립토 시세, 주가, 코멘트) |

## 세부 내용

<!-- para: para_010 -->
Bro의 IT이야기 : 네이버 블로그

<!-- para: para_011 -->
WebSocket 실시간 통신의 모든 것, HTTP와의 차이와 활용 사례 - Y Information
콘텐츠로 바로가기
메뉴
닫기
여러분의 일상에 작지만 소중한 변화를 드리고자 합니다. 이곳에서 발견하는 정보가 조금이나마 도움이 되기를 바랍니다.

<!-- para: para_012 -->
WebSocket API: Events, Methods & Properties | WebSocket.org
Skip to content
WebSocket.org
Search
Ctrl
K
Cancel
GitHub
Guides
Core Concepts
The Road to WebSockets
WebSocket Protocol
The Future of WebSockets
WebSockets and AI
Implementation
Building a WebSocket App
WebSocket Reconnection
Heartbeat & Keep-Alive
Error Handling
Connection Limits
WebSockets at Scale
Best Practices
Security
Authentication
Security Hardening
Testing
Autobahn TestSuite
Troubleshooting
403 Forbidden Errors
Connection Refused
CORS & Cross-Origin
Debugging in Chrome DevTools
Timeout & Dropped Connections
Infrastructure
Nginx Configuration
AWS ALB Configuration
Cloudflare Configuration
Kubernetes Ingress
Frameworks
React
Next.js
Express.js
Django
FastAPI
Spring Boot
Use Cases
Building a Chat App
Real-time Notifications
AI/LLM Token Streaming
Languages
JavaScript & Node.js
Python
Go
Rust
Java
C# & .NET
PHP
Protocol Comparisons
Overview
WebSockets vs HTTP
WebSockets vs SSE
WebSockets vs Long Polling
WebSockets vs WebTransport
WebSockets vs MQTT
WebSockets vs WebRTC
WebSockets vs gRPC
WebSocket vs REST API
Socket.IO vs WebSocket
SignalR vs WebSocket
Managed Services Compared
Decision Matrix
Reference
API Reference
WebSocket API
Close Codes
Protocol & Transport
WebSocket Handshake
WebSocket Headers
WebSocket Ports
wss vs ws
WebSocket vs TCP
Browser Support
Standards
Standards Tracker
Tools
Echo Server
WebSocket vs SSE vs HTTP
Resources
WebSocket Resources
Community
📖 Once Upon a Socket
GitHub
On this page
Overview
Quick Reference
Creating a Connection
Essential Events
Sending Data
Closing Connection
The WebSocket API Overview
Key Benefits
The WebSocket Interface
Constructor
Connection States
Checking Connection State
Properties
Read-Only Properties
Configurable Properties
Methods
send(data)
close([code][, reason])
Events
Event Types
open Event
message Event
error Event
close Event
Practical Usage Patterns
Reconnection Strategy
Heartbeat/Ping-Pong Pattern
Error Handling Best Practices
Common Use Cases
Chat Application
Live Data Streaming
Gaming and Real-time Collaboration
Performance Considerations
Message Size and Frequency
Buffer Management
Connection Pooling
TypeScript Support
Type Definitions
Typed Message Interfaces
Typed WebSocket Wrapper Class
Enum-based State Management
Async/Await Pattern with TypeScript
Working with Binary Data
Sending Binary Data
Receiving Binary Data
Browser Compatibility
Current Browser Support
Feature Detection
Browser-Specific Considerations
Security Considerations
Always Use Secure WebSockets (WSS)
Validate Origin
Input Validation
Authentication
Rate Limiting
Common Gotchas
bufferedAmount and Backpressure
Message Size Limits
Close Codes and Their Meanings
onerror Limitations
lastEventId Irrelevance
binaryType Configuration
Related Interfaces
CloseEvent
MessageEvent
WebSocket Close Codes
Standard Codes (1000-1015)
Application Codes (4000-4999)
IoT and Mobile Considerations
Battery Optimization
Live Streaming Patterns
Adaptive Bitrate Streaming
Further Reading
Specifications and Standards
WebSocket.org Resources
Developer Resources
Testing Tools
Libraries and Frameworks
FAQ
How do I create a WebSocket connection in JavaScript? What are the WebSocket readyState values?

<!-- para: para_013 -->
WebSocket을 이용하여 클라이언트 애플리케이션 작성하기 - Web API | MDN
Skip to main content
Skip to search
MDN
HTML
HTML: Markup language
HTML reference
Elements
Global attributes
Attributes
See all…
HTML guides
Responsive images
HTML cheatsheet
Date & time formats
See all…
Markup languages
SVG
MathML
XML
CSS
CSS: Styling language
CSS reference
Properties
Selectors
At-rules
Values
See all…
CSS guides
Box model
Animations
Flexbox
Colors
See all…
Layout cookbook
Column layouts
Centering an element
Card component
See all…
JavaScript
JS
JavaScript: Scripting language
JS reference
Standard built-in objects
Expressions & operators
Statements & declarations
Functions
See all…
JS guides
Control flow & error handing
Loops and iteration
Working with objects
Using classes
See all…
Web APIs
Web APIs: Programming interfaces
Web API reference
File system API
Fetch API
Geolocation API
HTML DOM API
Push API
Service worker API
See all…
Web API guides
Using the Web animation API
Using the Fetch API
Working with the History API
Using the Web speech API
Using web workers
All
All web technology
Technologies
Accessibility
HTTP
URI
Web extensions
WebAssembly
WebDriver
See all…
Topics
Media
Performance
Privacy
Security
Progressive web apps
Learn
Learn web development
Frontend developer course
Getting started modules
Core modules
MDN Curriculum
Check out the video course from Scrimba, our partner
Learn HTML
Structuring content with HTML module
Learn CSS
CSS styling basics module
CSS layout module
Learn JavaScript
Dynamic scripting with JavaScript module
Tools
Discover our tools
Playground
HTTP Observatory
Border-image generator
Border-radius generator
Box-shadow generator
Color format converter
Color mixer
Shape generator
About
Get to know MDN better
About MDN
Advertise with us
Community
MDN on GitHub
Blog
개발자를 위한 웹 기술
Web API
웹 소켓
WebSocket을 이용하여 클라이언트 애플리케이션 작성하기
This page was translated from English by the community. Learn more and join the MDN Web Docs community.

<!-- para: para_014 -->
Release Notes - Uvicorn
Skip to content
Uvicorn
Release Notes
Initializing search
Kludex/uvicorn
Uvicorn
Kludex/uvicorn
Welcome
Installation
Settings
Server Behavior
Concepts
Concepts
ASGI
Lifespan
WebSockets
Event Loop
Deployment
Deployment
Deployment
Docker
Release Notes
Release Notes
Table of contents
0.44.0 (April 6, 2026)
0.43.0 (April 3, 2026)
0.42.0 (March 16, 2026)
0.41.0 (February 16, 2026)
0.40.0 (December 21, 2025)
0.39.0 (December 21, 2025)
0.38.0 (October 18, 2025)
0.37.0 (September 23, 2025)
0.36.1 (September 23, 2025)
0.36.0 (September 20, 2025)
0.35.0 (June 28, 2025)
0.34.3 (June 1, 2025)
0.34.2 (April 19, 2025)
0.34.1 (April 13, 2025)
0.34.0 (December 15, 2024)
0.33.0 (December 14, 2024)
0.32.1 (November 20, 2024)
0.32.0 (October 15, 2024)
0.31.1 (October 9, 2024)
0.31.0 (September 27, 2024)
0.30.6 (August 13, 2024)
0.30.5 (August 2, 2024)
0.30.4 (July 31, 2024)
0.30.3 (July 20, 2024)
0.30.2 (July 20, 2024)
0.30.1 (June 2, 2024)
0.30.0 (May 28, 2024)
0.29.0 (March 19, 2024)
0.28.1 (March 19, 2024)
0.28.0 (March 9, 2024)
0.27.1 (February 10, 2024)
0.27.0.post1 (January 29, 2024)
0.27.0 (January 22, 2024)
0.26.0 (January 16, 2024)
0.25.0 (December 17, 2023)
0.24.0.post1 (November 6, 2023)
0.24.0 (November 4, 2023)
0.23.2 (July 31, 2023)
0.23.1 (July 18, 2023)
0.23.0 (July 10, 2023)
0.22.0 (April 28, 2023)
0.21.1 (March 16, 2023)
0.21.0 (March 9, 2023)
0.20.0 (November 20, 2022)
0.19.0 (October 19, 2022)
0.18.3 (August 24, 2022)
0.18.2 (June 27, 2022)
0.18.1 (June 23, 2022)
0.18.0 (June 23, 2022)
0.17.6 (March 11, 2022)
0.17.5 (February 16, 2022)
0.17.4 (February 4, 2022)
0.17.3 (February 3, 2022)
0.17.2 (February 3, 2022)
0.17.1 (January 28, 2022)
0.17.0.post1 (January 24, 2022)
0.17.0 (January 14, 2022)
0.16.0 (December 8, 2021)
0.15.0 (August 13, 2021)
0.14.0 (June 1, 2021)
0.13.4 (February 20, 2021)
0.13.3 (December 29, 2020)
0.13.2 (December 12, 2020)
0.13.1 (December 12, 2020)
0.13.0 (December 8, 2020)
0.12.3 (November 21, 2020)
0.12.2 (October 19, 2020)
0.12.1 (September 30, 2020)
0.12.0 (September 28, 2020)
0.11.8 (July 30, 2020)
0.11.7 (July 28, 2020)
0.11.6 (July 17, 2020)
0.11.5 (April 29, 2020)
0.11.4 (April 28, 2020)
0.11.3 (February 17, 2020)
0.11.2 (January 20, 2020)
0.11.1 (December 20, 2019)
0.11.0 (December 20, 2019)
0.10.8 (November 12, 2019)
0.10.7 (November 12, 2019)
0.10.6 (November 12, 2019)
0.10.5 (November 12, 2019)
0.10.4 (November 9, 2019)
0.10.3 (November 1, 2019)
0.10.2 (October 31, 2019)
0.10.1 (October 31, 2019)
0.10.0 (October 29, 2019)
Contributing
Sponsorship
Table of contents
0.44.0 (April 6, 2026)
0.43.0 (April 3, 2026)
0.42.0 (March 16, 2026)
0.41.0 (February 16, 2026)
0.40.0 (December 21, 2025)
0.39.0 (December 21, 2025)
0.38.0 (October 18, 2025)
0.37.0 (September 23, 2025)
0.36.1 (September 23, 2025)
0.36.0 (September 20, 2025)
0.35.0 (June 28, 2025)
0.34.3 (June 1, 2025)
0.34.2 (April 19, 2025)
0.34.1 (April 13, 2025)
0.34.0 (December 15, 2024)
0.33.0 (December 14, 2024)
0.32.1 (November 20, 2024)
0.32.0 (October 15, 2024)
0.31.1 (October 9, 2024)
0.31.0 (September 27, 2024)
0.30.6 (August 13, 2024)
0.30.5 (August 2, 2024)
0.30.4 (July 31, 2024)
0.30.3 (July 20, 2024)
0.30.2 (July 20, 2024)
0.30.1 (June 2, 2024)
0.30.0 (May 28, 2024)
0.29.0 (March 19, 2024)
0.28.1 (March 19, 2024)
0.28.0 (March 9, 2024)
0.27.1 (February 10, 2024)
0.27.0.post1 (January 29, 2024)
0.27.0 (January 22, 2024)
0.26.0 (January 16, 2024)
0.25.0 (December 17, 2023)
0.24.0.post1 (November 6, 2023)
0.24.0 (November 4, 2023)
0.23.2 (July 31, 2023)
0.23.1 (July 18, 2023)
0.23.0 (July 10, 2023)
0.22.0 (April 28, 2023)
0.21.1 (March 16, 2023)
0.21.0 (March 9, 2023)
0.20.0 (November 20, 2022)
0.19.0 (October 19, 2022)
0.18.3 (August 24, 2022)
0.18.2 (June 27, 2022)
0.18.1 (June 23, 2022)
0.18.0 (June 23, 2022)
0.17.6 (March 11, 2022)
0.17.5 (February 16, 2022)
0.17.4 (February 4, 2022)
0.17.3 (February 3, 2022)
0.17.2 (February 3, 2022)
0.17.1 (January 28, 2022)
0.17.0.post1 (January 24, 2022)
0.17.0 (January 14, 2022)
0.16.0 (December 8, 2021)
0.15.0 (August 13, 2021)
0.14.0 (June 1, 2021)
0.13.4 (February 20, 2021)
0.13.3 (December 29, 2020)
0.13.2 (December 12, 2020)
0.13.1 (December 12, 2020)
0.13.0 (December 8, 2020)
0.12.3 (November 21, 2020)
0.12.2 (October 19, 2020)
0.12.1 (September 30, 2020)
0.12.0 (September 28, 2020)
0.11.8 (July 30, 2020)
0.11.7 (July 28, 2020)
0.11.6 (July 17, 2020)
0.11.5 (April 29, 2020)
0.11.4 (April 28, 2020)
0.11.3 (February 17, 2020)
0.11.2 (January 20, 2020)
0.11.1 (December 20, 2019)
0.11.0 (December 20, 2019)
0.10.8 (November 12, 2019)
0.10.7 (November 12, 2019)
0.10.6 (November 12, 2019)
0.10.5 (November 12, 2019)
0.10.4 (November 9, 2019)
0.10.3 (November 1, 2019)
0.10.2 (October 31, 2019)
0.10.1 (October 31, 2019)
0.10.0 (October 29, 2019)
Release Notes
0.44.0 (April 6, 2026)
¶
Added
¶
Implement websocket keepalive pings for websockets-sansio (
#2888
)
0.43.0 (April 3, 2026)
¶
You can quit Uvicorn now. We heard you, @pamelafox - all 47 of your Ctrl+C's (thanks for flagging it, and thanks to @tiangolo for the fix 🙏).
