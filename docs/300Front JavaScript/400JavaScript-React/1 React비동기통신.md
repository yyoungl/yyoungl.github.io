---
layout: default
title: JavaScript React에서의 비동기 통신
nav_order: 1
description: JavaScript React에서의 비동기 통신
parent: React
---

# 리액트에서의 비동기 통신

생성일: 2023년 4월 11일 오후 3:30

# 비동기 통신과 프로미스

## 01 자바스크립트 비동기 1

### 자바스크립트 비동기의 등장

- 초기 웹 환경에서는, 서버에서 모든 데이터를 로드하여 페이지를 빌드했으므로 자바스크립트에서는 별도의 비동기 처리가 필요하지 않음
- Ajax(Asynchronous JavaScript and XML) 기술의 등장으로 페이지 로드 없이 client-side에서 서버로 요청을 보내 데이터를 처리할 수 있게 됨
- XMLHttpRequest라는 객체를 이용해 서버로 요청을 보낼 수 있게 됨

### 자바스립트와 비동기

- 자바스크립트는 single-threaded language이므로, 만일 서버 요청을 기다려야 한다면 유저는 멈춰 있는 브라우저를 보게 될 것
- 따라서 동기가 아닌 비동기 처리를 이용해 서버로 통신할 필요가 있음
- 비동기 요청 후, main thread는 유저의 입력을 받거나, 페이지를 그리는 등의 작업을 처리함
- 비동기 응답을 받으면, 응답을 처리하는 callback 함수를 task queue에 넣음
- event loop는 main thread에 여유가 있을 때 task queue에서 함수를 꺼내 실행함

### 동기 vs 비동기

**동기(synchronous)** 코드는, 해당 코드 블록을 실행할 때 thread의 제어권을 넘기지 않고 순서대로 실행 (이전의 코드 실행이 끝나지 않으면 다음으로 넘어가지 않음)

**비동기(asynchronous)** 코드는, 코드의 순서와 다르게 실행됨 ex setTimeout 등  
비동기 처리 코드를 감싼 블록은 task queue에 넣어짐  
main thread가 동기 코드를 실행한 후에 제어권이 돌아왔을 때 event loop가 task queue에 넣어진 비동기 코드 실행

## 02 자바스크립트 비동기 2

### 비동기 처리를 위한 내부 구조

- 브라우저에서 실행되는 자바스크립트는 event driven 시스템으로 작동
- 웹앱을 로드하면 브라우저는 HTML document를 읽어 문서에 있는 CSS code, JS code를 불러옴
- 자바스크립트 엔진은 코드를 읽어 실행
- 브라우저의 main thread는 자바스크립트 코드에서 동기적으로 처리되어야 할 코드 실행 외에도, 웹 페이지를 실시간으로 렌더링하고, 유저의 입력을 감지하고, 네트워크 통신을 처리하는 등 수많은 일을 처리
- 비동기 작업을 할당하면, 비동기 처리가 끝나고 브라우저는 task queue에 실행 코드를 넣음
- main thread는 event lopo를 돌려 task queue에 직업이 있는지 체크
- 작업이 있으면 task 실행

**diagram**

![react-비동기](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCe9OW%2FbtsrhFV32fg%2FfhEwl7vI3x8r6pwVwM3Lh1%2Fimg.png)

## 03 Promise

### Callback pattern vs Promise

### Callback pattern ex setTimeout

- 비동기 처리 후 실행될 코드를 Callback function으로 보내는 것
- 비동기 처리가 고도화되면서 Callback hell 등이 단점으로 부각됨
- Promise를 활용하여 비동기 처리의 순서 조작, 에러 핸들링, 여러 비동기 요청 처리 등을 쉽게 처리할 수 있게 됨

### Promise

- Promise 객체: 객체가 생성 당시에는 알려지지 않은 데이터에 대한 Proxy
- 비동기 실행이 완료된 후에 `.then` `.catch` `.finally` 등의 핸들러를 붙여 각각 데이터 처리 로직, 에러 처리 로직, 클린업 로직을 실행
- then 체인을 붙여 비동기 실행을 마치 동기 실행처럼 동작하도록 함
- 전체 스펙은… [https://promiseaplus.com](https://promiseaplus.com)
- Promise 객체는 pending, fulfilled, rejected 상태를 가짐
- fulfilled, rejected 두 상태를 settled 라고 한다
- pending: 비동기 실행이 끝나기를 기다리는 상태
- fulfilled: 비동기 실행이 성공한 상태
- rejected: 비동기 실행이 실패한 상태
- then, catch는 비동기(Promise), 동기 실행 중 어떤 것이라도 리턴할 수 있음

### Multiple Promise handling

Promise는 여러 가지 Promise를 동시에 처리할 수 있는 함수를 객체 단위로 제공함

- **Promise.all()** 모든 프로미스가 fulfilled 되길 기다림  
  하나라도 에러 발생 시, 모든 프로미스 요청 중단됨
- **Promise.allSettled()** 모든 프로미스가 settled 되길 기다림
- **Promise.race()** 넘겨진 프로미슫르 중 하나라도 settled 되길 기다림
- \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***\*\*\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***Promise.any()\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***\*\*\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** 넘겨진 프로미스 중 하나라도 fulfilled 되길 기다림

### Promise chaining, nested promise

- Promise 객체는 settled 되더라도 계속 핸들을 붙일 수 있음
- 핸들러를 붙인 순서대로 호출됨
- .catch 뒤에 계속 핸들러가 붙어있다면, 에러를 처리한 후에 계속 진행됨  
  이때는 catch에서 리턴한 값이 then으로 전달됨

## 04 async/await

### async/await

- Promise 체인을 구축하지 않고도 Promise를 직관적으로 사용할 수 있는 문법
- 많은 프로그래밍 언어에 있는 try … catch 문으로 에러를 직관적으로 처리
- async function을 만들고 Promise를 기다려야 하는 표현 앞에 await 붙임

### 여러 개의 await

- 여러 개의 await을 순서대로 나열하여 then chain을 구현할 수 있음
- try … catch문을 자유롭게 활용하여 에러 처리를 적용

### async/await - Promise와의 조합

- async/await을 사용하면 코드가 순차적으로 실행되어 끝나는 대로 먼저 처리
- Promise.all을 활용하면 코드가 병렬적으로 처리됨

## 05 POSTMAN, Open API, CORS

### POSTMAN 소개

- 서버와의 통신을 위해 API를 활용하는 경우, React 앱으로만 요청하여 API가 동작하는지 알아보는 건 비효율적이고
- 수많은 API의 endpoint와 실행 조건 등을 관리하는 것도 힘들다

→ POSTMAN은 API를 테스트하기 위한 개발 도구

- API 요청에 필요한 데이터: Auto, header, payload, query 등을 쉽게 세팅
- 다른 개발자가 쉽게 셋업해 테스트할 수 있도록 API 정보를 공유할 수 있음
- Request를 모아 Collection으로 만들어 API를 종류별로 관리
- 환경 변수를 정의하여 환경별(production server, development server 등)로 테스트 가능
- [https://wwww.postman.com](https://wwww.postman.com)

### Open API

- RESTful API를 하나의 문서로 정의하기 위한 문서 표준
- OpenAPI Specification(OAS)으로 정의됨
- Swagger 등의 툴로 Open API로 작성된 문서를 파싱해 테스팅 도구로 만들 수 있음
- 프론트엔드 개발자, 백엔드 개발자와의 협업 시 중요한 도구로 사용
- API의 method, endpoint를 정의
- endpoint마다 인증 방식, content type 등 정의
- body data, query string, path variable 등 정의
- 요청, 응답 데이터 형식과 타입 정의 - data model(JSON 등) 활용 (schema)

→ 특정 언어로 국한된 게 아니라서 어떤 언어를 사용하든 상관없음!

### CORS (Cross-Origin Resource Sharing)

- 브라우저는 모든 요청 시 Origin 헤더를 포함
- 서버는 Origin 헤더를 보고, 해당 요청이 원하는 도메인에서부터 출발한 것인지를 판단
- 다른 Origin에서 온 요청은 서버에서 기본적으로 거부함

→ 브라우저가 요청을 보내기 전에 options라는 요청을 미리 보냄 (요청을 처리할 수 있는지 물어보는 것) 처리할 수 없다고 하면 브라우저는 서버에 요청을 보낼 수 없다고 판단하고 네트워크 요청 실패!!

- 그러나, 보통 서버의 endpoint와 홈페이지 domain은 다른 경우가 많음
- 따라서 서버에는 홈페이지 domain을 허용하여 다른 domain이라 하더라도 요청을 보낼 수 있게 함
- 서버는 Access-Control-Allow-Origin 외에 Access-Control-\*을 포함하는 헤더에 CORS 관련 정보를 클라이언트로 보냄
- 웹사이트에 악성 script가 로드되어 수상한 요청을 하는 것을 막기 위함
- 반대로, 익명 유저로부터의 DDos 공격을 막기 위함
- 서버에 직접 CORS 설정을 할 수 없다면 Proxy 서버 등을 만들어 해결
