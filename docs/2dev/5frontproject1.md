---
layout: default
title: Front 관통 프로젝트 <영상 관리 프로그램 웹>
nav_order: 5
description: Java 관통 프로젝트 <영상 관리 프로그램 웹>
parent: Project
---

# Front 관통 프로젝트: 영상 관리 프로그램

{: .fs-6 .fw-300 }
[Github](https://github.com/yyoungl/ssafit-front){: .btn .fs-5 .mb-4 .mb-md-0 }

**개발 기간** 2023/08/11 (1일)

**개발 인원** 2명

[이영현](https://github.com/yyoungl) [@olrlozl](https://github.com/olrlozl)

### 프로젝트 목표

1. HTML, CSS, JavaScript 활용
2. CSS, Bootstrap으로 향상된 디자인 구현
3. UX, UI를 고려한 사이트를 구현하여 사용자 입장에서 편리하고 멋진 디자인 설계

### 프로젝트 요구사항

1. Wireframe Tool을 이용하여 구현할 웹 페이지 프로토타입 설계
2. SSAFIT 사이트 메인 페이지 및 메뉴
   1. 메인 페이지 구성: 운동영상 정보의 다양한 화면 구성
   2. 메뉴 구성: 사이트 주요 메뉴 구성
3. 운동 영상에 대한 리뷰 관리 페이지
   1. 리뷰 목록, 등록, 수정, 상세, 삭제
4. 회원가입/로그인 메뉴
5. 유저의 찜한 동영상, 팔로잉/팔로워 목록

### 사용 기술

- HTML
- CSS
- Bootstrap

### 구현 과정

**1. Prototype 제작**

모든 화면을 완성하려면 시간적 여유가 없을 것 같아 Wireframe Tool을 사용하진 않고 예시로 주어진 구현 화면을 활용하여 간략한 프로토타입을 만들었다.

**2. 개발 환경 조성**

이번에도 Github 저장소를 만들어서 함께 작업했다. 다만, HTML과 CSS를 활용하여 화면부터 구현할 생각으로 메인 브랜치에서 직접 작업했다.
각자 맡은 파일만 수정하되, VSCode에서는 충돌이 발생하면 대조할 수 있어 충돌이 발생해도 금방 해결할 수 있었다.
프로토타입을 기반으로 폴더와 파일 구조를 미리 만들어 두고, CDN을 활용해 부트스트랩을 가져와 개발을 시작했다.

**3. 개발**

요구하는 것들을 화면에 띄우는 것을 가장 우선으로 했다. 팀원은 리뷰 관련 페이지를 모두 만들고, 메인 페이지와 메뉴, 회원가입/로그인, 찜과 팔로우 화면은 내가 맡아서 했다. 각자 작업한 내용을 중간중간 합치고 확인하며 차근차근 개발을 진행했다.

### 느낀 점

처음 구현하고자 했던 화면과 흡사하게 만들어서 아주 뿌듯하다.

오랜만에 Bootstrap을 사용해서 처음엔 버전이 맞지 않아 제공되는 js가 작동하지 않았다. 조금 당황했지만 버전에 맞는 컴포넌트를 가져다 만들었다. -> Bootstrap 컴포넌트를 제공하는 사이트 URL을 보면 버전이 나타나는데, 이 버전을 변경하면 버전에 맞는 컴포넌트를 가져다 쓸 수 있다.

메뉴가 존재하는 `<header>`처럼 모든 페이지에 들어가는 요소의 경우, 모든 파일에 넣어야 했기 때문에 변경 사항이 한꺼번에 반영되지 않아 조금 불편했다. 리액트나 뷰 같은 개발 툴을 사용할 때는 꼭 컴포넌트 하나를 만들어서 개발해야겠다.

이 과정에서 팀원이 내가 못 보고 지나친 것들을 체크해 줘서 고마웠다. 서로 안 되는 부분이 있으면 활발히 의견을 말하며 크고 작은 문제점을 해결할 수 있었다.

### 더 해볼만한 것

JavaScript로 기능을 구현하고 데이터를 관리해 봤어야 하는데 시간이 허락하지 않았다. 다음에는 클릭으로 페이지 이동뿐 아니라 데이터 관리를 통해 리뷰 관리 기능 같은 것들도 구현해 보고 싶다.

### 파일 구성

**메인 페이지 및 메뉴 구성**

메인 화면 `main.html`

메뉴 구성: `header`

**리뷰 관리 페이지**

리뷰 목록 `reviewList.html`

리뷰 상세 `reviewDetail.html`

리뷰 수정 `reviewEdit.html`

리뷰 등록 `addReview.html`

**회원가입/로그인**

회원가입 페이지 `register.html`

로그인 페이지 `login.html`

**찜/팔로잉**

회원 찜 영상 관리 `likeList.html`

회원 친구 팔로우 관리 `follow.html`

### 메인 화면 - 영상 목록 조회 및 메뉴

![메인 페이지 및 메뉴 구성](https://github.com/yyoungl/ssafit-front/blob/main/result/%EA%B8%B0%EB%B3%B8%20-%20%EB%A9%94%EC%9D%B8%20%ED%8E%98%EC%9D%B4%EC%A7%80%20%EB%B0%8F%20%EB%A9%94%EB%89%B4%20%EA%B5%AC%EC%84%B1.PNG?raw=true)

### 리뷰 관리

![리뷰 등록](https://github.com/yyoungl/ssafit-front/blob/main/result/%EA%B8%B0%EB%B3%B8%20-%20%EB%A6%AC%EB%B7%B0%20%EA%B4%80%EB%A6%AC%20%EB%A6%AC%EB%B7%B0%20%EB%93%B1%EB%A1%9D.PNG?raw=true)

![리뷰 목록](https://github.com/yyoungl/ssafit-front/blob/main/result/%EA%B8%B0%EB%B3%B8%20-%20%EB%A6%AC%EB%B7%B0%20%EA%B4%80%EB%A6%AC%20%EB%A6%AC%EB%B7%B0%20%EB%AA%A9%EB%A1%9D.PNG?raw=true)

![리뷰 상세](https://github.com/yyoungl/ssafit-front/blob/main/result/%EA%B8%B0%EB%B3%B8%20-%20%EB%A6%AC%EB%B7%B0%20%EA%B4%80%EB%A6%AC%20%EB%A6%AC%EB%B7%B0%20%EC%83%81%EC%84%B8.PNG?raw=true)

![리뷰 수정](https://github.com/yyoungl/ssafit-front/blob/main/result/%EA%B8%B0%EB%B3%B8%20-%20%EB%A6%AC%EB%B7%B0%20%EA%B4%80%EB%A6%AC%20%EB%A6%AC%EB%B7%B0%20%EC%88%98%EC%A0%95.PNG?raw=true)

### 찜 영상 관리

![찜 영상 관리](https://github.com/yyoungl/ssafit-front/blob/main/result/%EC%8B%AC%ED%99%94%20-%20%EC%B0%9C%20%EC%98%81%EC%83%81%20%EA%B4%80%EB%A6%AC.PNG?raw=true)

### 팔로우 목록

![팔로우](https://github.com/yyoungl/ssafit-front/blob/main/result/%EC%8B%AC%ED%99%94%20-%20%ED%8C%94%EB%A1%9C%EC%9A%B0.PNG?raw=true)

### 회원가입/로그인

![회원가입](https://github.com/yyoungl/ssafit-front/blob/main/result/%EC%B6%94%EA%B0%80%20-%20%ED%9A%8C%EC%9B%90%EA%B0%80%EC%9E%85.PNG?raw=true)

![로그인](https://github.com/yyoungl/ssafit-front/blob/main/result/%EC%B6%94%EA%B0%80%20-%20%EB%A1%9C%EA%B7%B8%EC%9D%B8.PNG?raw=true)
