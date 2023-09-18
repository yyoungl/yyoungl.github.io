---
layout: default
title: Servlet
nav_order: 501
parent: Java Backend
---

# Servlet

생성 일시: 2023년 9월 4일 오후 5:22

- 웹 프로그래밍
- Servlet
- Servlet Parameter

# 웹 프로그래밍

## Web Architecture

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTUTYB%2FbtsufZSZ7Ok%2FXnGiedd92WxiOICEBBj4Q0%2Fimg.png)

request, response를 보내기 위해서는 하나의 규약이 필요함: http

## 웹과 웹 프로그래밍

- URL (Uniform Resource Locator) 웹 상의 자원을 참조하기 위한 웹 주소
- 웹 페이지 (Web page) 웹 브라우저를 통해서 보여지는 화면
- 웹 서버 (Web Server) 클라이언트 요청에 맞는 응답 (웹 페이지) 를 제공
- 웹 어플리케이션 (Web Application) 웹 서버를 기반으로 실행되는 응용 소프트웨어
- 웹 어플리케이션 서버 (Web Application Servser, WAS) 요청이 오면 알맞은 프로그램을 실행하여 응답 만들고 제공하는 서버

### Dynamic Web Project

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeJWtLO%2FbtsuHbcVHGM%2FHSG0bN1pI79xncHaTQGWKK%2Fimg.png)

### Dynamic Web Project 구조

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcbvygP%2FbtsuGkVuZv9%2Fkrd4wmqKFvVvtJKfsNhnaK%2Fimg.png)

1. Web Application 실행에 필요한 Java 관련 Resource를 포함
2. Web Application 실행에 필요한 html, javascript ,css, JSP, Image 등 웹 컨텐츠를 포함

   웹 어플리케이션 설정 파일인 web.xml도 WebContent/WEB-INF/에 위치한다

### Hello Servlet

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmp4BU%2FbtsuGoXSxNT%2FdLh6pA8RLKQXkoHbWieAOk%2Fimg.png)

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrO8kC%2FbtsuIzY0dLy%2FNReP9fLgwkn1KnXLAnxH20%2Fimg.png)

# Servlet

---

## Servlet이란?

- Server + Applet 의 합성어
- 자바를 이용하여 웹에서 실행되는 프로그램을 작성하는 기술
- 자바를 이용하여 웹페이지를 동적으로 생성할 수 있음
  - Servlet은 자바 코드 안에 HTML을 포함

### Servlet API

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fs1wvf%2FbtsuIEssLMJ%2FiXzfB9hS4KrST5QzoO4Cek%2Fimg.png)

### Servlet 등록 방법 (web.xml)

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdiV0iM%2FbtsuG8tI6UC%2F8q3LS7ZWaZNoxodaMN6pQK%2Fimg.png)

### Servlet 등록방법 (Annotation)

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb2NStg%2FbtsugRHee4o%2FJNfjiXUhSiGkREjDehKf11%2Fimg.png)

## Servlet 생명주기 (Life-Cycle)

- 서블릿 인스턴스는 서블릿이 포함된 웹 컨테이너에 의해 제어된다
- 서블릿 인스턴스가 존재하지 않으면 다음과 같은 작업을 수행한다
  1. 서블릿클래스 로드
  2. 서블릿클래스 인스턴스 생성
  3. 서블릿 인스턴스 초기화
  4. 웹 컨테이너에 의한 서비스 메서드 호출
  5. destroy 메서드를 호출하여 서블릿 종료
- 서비스 메서드는 요청이 들어올 때마다 호출된다

# Servlet Parameter

---

### GET

- 지정된 리소스에서 데이터를 요청하는 데 사용
- query string (name/value 쌍)이 URL에 포함되어 전송됨
- POST와 비교하여 보안에 취약함
- URL이 길이 제한이 있으므로 전송 가능한 데이터의 길이가 제한적 (URL maximum characters: 2048)
  ASCII 문자만 가능

### POST

- 리소스를 생성/업데이트하기 위해 서버에 데이터를 보내는 데 사용
- HTTP header의 body에 파라미터를 포함하여 전송
- 데이터 길이에 대한 제한 없음
- 매개변수가 브라우저나 웹 서버에 저장되지 않음
- 제한 없음. 바이너리 데이터도 허용

### URL 구성요소

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcyGBqe%2FbtsuG6bHFnX%2FAS4mVDeOxk5OrigHjwRGtK%2Fimg.png)

프로토콜, 서버, 경로

- 프로토콜: 절차를 포함한 통신규약
- 서버: 웹 페이지를 요청할 서버의 주소, 실제 IP 주소나 도메인을 입력할 수 있다
- 경로: 서버 내의 상세 경로
- 쿼리 스트링: 추가로 서버로 데이터를 전송하기 위해서 사용한다. ‘?’ 마크를 적어 시작을 표시한다. `parameter_name=value` 형태로 작성하며, 파라미터가 여러 개일 경우 ‘&’로 구분하여 작성한다

### input tag 실습

- text (영어/한글)
- number
- radio
- checkbox
- select
- textarea
- hidden

### Front-Controller

- 웹에서 발생하는 모든 요청에 대해 호출되는 Servlet을 만들어 처리함
- 어떤 요청을 보냈을 때 관련 Servlet이 동작하게끔!! 비슷한 기능끼리 하나의 Servlet이 관리하도록 처리하는 것
- 서블릿이 하나임 → 요청을 구분할 수 없어!
- 어딘가에 요청을 보낼 때 요청의 종류를 구분해야 하는데 이것을 노출하면 사용자는 모르게 서버에다 전송하고 싶음… 그것이 (hidden) 사용자에게는 보이지 않는데 우리만 알 수 있음
