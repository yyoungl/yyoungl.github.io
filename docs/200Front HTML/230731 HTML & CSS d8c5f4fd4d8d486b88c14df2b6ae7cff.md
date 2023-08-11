---
layout: default
title: HTML & CSS
nav_order: 201
description: HTML & CSS
parent: HTML/CSS
---

# HTML & CSS

생성 일시: 2023년 7월 31일 오후 2:11

- HTML
- CSS
- CSS Selector

# HTML

---

## HTML

- Hyper Text Markup Language
- Hyper Text: 참조를 통해 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트
- Markup: 태그 등을 이용하여 문서나 데이터의 구조를 명기하는 언어

![HTML](https://github.com/yyoungl/yyoungl.github.io/assets/127117707/2f02b82d-e25b-493a-a843-7ca9daee8271)

- 웹페이지를 작성하기 위한 언어
- `.html`(확장자)를 가짐
- 태그는 대소문자 구분이 없음
- 엔터, 스페이스바, 탭이 적용되지 않음

## HTML 구성요소

## 태그 (Tag)

- HTML의 요소는 태그와 내용으로 구성
  ```html
  <a href="https://edu.ssafy.com/">에듀싸피</a>
  ```
- 시작태그 / 종료태그로 쌍을 이루거나 시작 tag만 존재하는 tag도 있다
- 각각의 시작 태그는 속성과 속성값을 가질 수 있음

## 주석

- 주석의 내용은 브라우저에 출력이 되지 않음
- HTML tag의 내용을 설명하기 위한 용도로 사용
  ```html
  <!-- 주석 내용 -->
  ```

## 기본 구조

- html: HTML 최상위 요소, 문서의 root → head와 body로 구성
- head: 문서 제목 문자 코드(인코딩) 등 해당 문서에 대한 정보를 가지고 있고 브라우저 화면 출력 X
- meta: 문서의 작성자, 날짜 등 본문에 나타나지 않는 일반 정보들
- body: 브라우저 화면에 나타나는 정보
  id 속성을 이용하여 문서 내에서 tag 식별 가능 (중복 x)
  class 속성을 이용하여 여러 tag에 공통적인 특성 부여 (중복 o)

## 특수문자

| 엔티티 이름 | 설명                     | 화면출력 |
| ----------- | ------------------------ | -------- |
| $nbsp;      | Non-breaking space(공백) |          |
| $lt;        | Less than                | <        |
| $gt;        | Greater than             | >        |
| $amp;       | Ampersand                | &        |
| $quot;      | Quatation mark           | "        |
| $copy;      | Copyright                | ⓒ        |
| $reg;       | registered trademark     | ®        |

## Semantic tag

- 의미론적 요소를 담은 태그의 등장

| 태그 이름 | 설명                                                 |
| --------- | ---------------------------------------------------- |
| <header>  | 문서 전체나 섹션이 헤더                              |
| <nav>     | 네비게이션                                           |
| <aside>   | 사이드에 위치한 공간                                 |
| <section> | 문서의 일반적인 구분                                 |
| <article> | 문서, 페이지, 사이트 안에서 독립적으로 구분되는 영역 |
| <footer>  | 문서 전체나 섹션이 푸터                              |
| <h1>~<h6> | 6단계 구획 제목                                      |

- 코드의 가독성을 높이고 유지보수를 쉽게 함

![HTML 1](https://github.com/yyoungl/yyoungl.github.io/assets/127117707/03442739-cd28-4949-be14-a73f64111191)

## HTML 태그

## Text content

| 태그 이름     | 설명                                        |
| ------------- | ------------------------------------------- |
| <bloockquote> | 긴 인용문, 주로 들여쓰기를 한 것으로 그려짐 |
| <hr>          | 구분선                                      |
| <pre>         | 공백, 줄바꿈 등 입력된 그대로 화면에 표시   |
| <p>           | 하나의 문단                                 |
| <ul>          | 정렬되지 않은 목록 (번호 없는)              |
| <ol>          | 정렬된 목록 (번호 있는)                     |
| <div>         | 구문 컨텐츠를 위한 블록 컨테이너            |

## Inline text semantics

| 태그 이름    | 설명                                                                                                                        |
| ------------ | --------------------------------------------------------------------------------------------------------------------------- |
| <a>          | href 특성을 통해 다른 페이지나 같은 페이지의 어느 위치, 파일, 이메일 주소와 그 외 다른 URL로 연결할 수 있는 하이퍼링크 생성 |
| <b> <strong> | 굵은 글씨, 중대하거나 긴급한 콘텐츠 (strong)                                                                                |
| <br>         | 텍스트 안에 줄바꿈 생성                                                                                                     |
| <i> <em>     | 기울게 표시, 특정 문자열을 강조(em)                                                                                         |
| <q>          | 짧은 인라인 인용문                                                                                                          |
| <s>          | 취소선                                                                                                                      |
| <u>          | 밑줄                                                                                                                        |
| <sup> <sub>  | 위 첨자, 아래 첨자                                                                                                          |
| <span>       | 구문 콘텐츠를 위한 인라인 컨테이너                                                                                          |

## Image & Multimedia

| 태그 이름 | 설명                          |
| --------- | ----------------------------- |
| <audio>   | 소리 콘텐츠를 포함할 때 사용  |
| <img>     | 문서에 이미지                 |
| <video>   | 미디어 플레이어를 문서에 삽입 |

## Table content

| 태그 이름  | 설명                                     |
| ---------- | ---------------------------------------- |
| <table>    | 행과 열로 이루어진 표를 나타낸다         |
| <thead>    | 테이블의 열의 머리글인 행들의 집합       |
| <tbody>    | 표의 여러 행 (tr) 을 묶어서 표 본문 구성 |
| <tfoot>    | 테이블의 열을 요약하는 행들의 집합       |
| <tr>       | 테이블 행                                |
| <th> <td>  | 머리글, 데이터                           |
| <col>      | 표의 열을 나타냄                         |
| <colgroup> | 표의 열을 묶는 그룹 정의                 |
| <caption>  | 표의 설명 또는 제목을 나타냄             |

## Forms

- 사용자로부터 데이터를 입력받아 서버에서 처리하기 위한 용도로 사용
- 사용자가 작성한 데이터를 서버로 전송 (submit)

| 속성                                            | 설명                                                                             |
| ----------------------------------------------- | -------------------------------------------------------------------------------- |
| method                                          | GET: 주소 표시줄에 사용자가 입력한 내용이 표시                                   |
| 256~2048bytes(길이 제한)의 데이터만 서버로 전송 |
|                                                 | POST: HTTP 메세지의 Body에 담아서 전송하기 때문에 전송 내용의 길이에 제한이 없다 |
| 사용자가 입력한 내용이 표시되지 않는다          |
| name                                            | from의 이름을 지정                                                               |
| action                                          | <form> 태그 안의 내용들을 처리해 줄 서버상의 프로그램 지정 (URL)                 |
| target                                          | <action> 태그에서 지정한 스크립트 파일을 현재 창이 아닌 다른 위치에 열도록 지정  |

## input

- 요소의 동작은 type 속성에 따라 달라짐

| 속성                                                                             | 설명                                                                                                |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| autofocus                                                                        | 페이지 로딩 후 폼의 요소 중에서 해당 요소에 마우스 커서를 표시                                      |
| html5 이전에는 자바스크립트로 구현                                               |
| placeholder                                                                      | 텍스트를 입력할 때 도움이 되도록 입력란에 적당한 힌트 내용을 표시                                   |
| 클릭 시 자동으로 내용이 사라짐                                                   |
| readonly                                                                         | 입력란에 텍스트를 사용자가 직접 입력하지 못하게 읽기 전용으로 지정                                  |
| readonly, readonly = “readonly” readonly = “true” 로 표현                        |
| required                                                                         | form에 data를 입력한 후 submit 클릭 시 data를 서버로 전송하기 전 필수 입력 항목을 체크              |
| required, required = “required”로 표현                                           |
| min, max, step                                                                   | min, max는 해당 필드의 최대, 최소값 지정, step은 일정 간격 지정                                     |
| type이 date, datetime, datetime-local, month, week, time, number, range에서 사용 |
| size, minlength, maxlength                                                       | minlength, maxlength는 텍스트 입력 시 최대, 최소 길이 지정, size는 화면에 보여지는 글자의 길이 지정 |
| height, width                                                                    | type = “image”일 때 이미지의 너비와 높이를 지정                                                     |
| multiple                                                                         | type = “email” 이나 type = “file” 일 때 두 개 이상의 값을 입력                                      |
| <input> 태그 안에 속성 이름만 표시하면 됨                                        |

# CSS

---

## CSS

- **Cascading Style Sheets**
- HTML 문서를 화면에 표시하는 방식을 정의한 언어
- 웹 문서의 내용과 관계없이 디자인만 바꿀 수 있음
- 다양한 기기에 맞게 반응형으로 바뀌는 문서를 만들 수 있음

### 기본 구조

```css
.box {
  background-color: red;
  width: 100px;
  height: 100px;
}
```

### 적용 방법 1 (External style sheet)

- `<link>`를 사용하여 외부 스타일 시트 적용 (.css 파일)
- `<head>` 안에 작성

  ```html
  <head>
    <link rel="stylesheet" href="external.css" />
  </head>
  ```

  ```css
  // external.css
  h1 {
    color: red;
  }

  p {
    background-color: rgb(42, 100, 226);
  }
  ```

### 적용 방법 2 (Internal style sheet)

- 파일 내에 스타일을 적용하는 방식
- <style> 태그 사이에 CSS 규칙 작성
- <head> 안에 작성
- 외부 스타일 시트보다 우선 적용
  ```html
  <head>
    <style>
      h1 {
        color: red;
      }
      p {
        background-color: rgb(42, 100, 226);
      }
    </style>
  </head>
  ```

### 적용 방법 3 (inline style)

- tag에서 style 속성을 사용하고 속성값으로 CSS 규칙 작성
- 스타일 적용 우선순위는 ‘인라인 → 내부 스타일 시트 → 외부 스타일 시트’ 순
  ```html
  <h1 style = "color: red;>인라인 스타일</h1>
  <p style = "background-color: rgb(42, 100, 226); > 이곳은 내용입니다.</p>
  ```

# CSS Selector

---

## CSS 선택자

- HTML 문서에서 CSS 규칙을 적용할 요소를 정의
- 기본 선택자
  - 유형 선택자
  - 클래스 선택자
  - id 선택자
  - 특성 선택자
- 그룹 선택자
- 결합자
  - 자손 결합자, 자식 결합자
  - 일반 형제 결합자, 인접 형제 결합자, 열 결합자
- 의사 클래스 / 요소
  - 의사 클래스
  - 의사 요소

### Universal selector `*` (전체 선택자)

- HTML 문서 내 모든 element를 선택
- 사용법 → \* {style-properties)

### Type selector (유형 선택자)

- 태그명을 이용하여 스타일을 적용할 태그를 선택
- HTML 내에서 주어진 유형의 모든 요소를 선택
- 사용법 → element {style properties}

### ID selector (ID 선택자)

- id 특성 값을 비교하여, 동일한 id를 가진 태그 선택
- HTML 내에서 주어진 ID를 가진 요소가 하나만 존재해야 함
- 사용법 → #id-value {style properties}

### Selector list (선택자 목록)

- , 를 이용하여 선택자 그룹을 생성하는 방법
- 모든 일치하는 노드를 선택
- 사용법 → element, element {style properties}

### Descentdant combinator (자손 결합자)

- 첫번째 요소의 자손인 노드 선택
- 사용법 → selector1, selector2 { style properties}

### Child combinator (자식 결합자)

- 첫 번째 요소의 **바로 아래** 자식인 노드를 선택
- 사용법 → selector1 > selector2 { style properties }

### General sibling combinator (일반 형제 결합자)

- 첫 번째 요소를 뒤따르면서 같은 부모를 공유하는 두 번째 요소를 모두 선택
- 사용법 → former-element ~ target-element {style properties}

### Adjacent sibling combinator (인접 형제 결합자)

- 첫 번째 요소의 바로 뒤에 위치하면서 같은 부모를 공유하는 두 번째 요소 선택
- 사용법 → former-element + target-element {style properties }

## 우선순위

- 같은 요소에 두 개 이상의 CSS 규칙이 적용된 경우
  마지막 규칙, 구체적인 규칙, `!important`가 우선 적용
- id > class > tag

## 상속 Inheritance

- 부모 요소에 적용된 스타일이 자식 요소에게 상속이 될 수도 있고, 안 될 수도 있음.
- 상속되는 속성
  - 요소의 상속되는 속성에 값이 지정되지 않은 경우, 요소는 부모 요소의 해당 속성의 **계산 값**을 얻음
  - 대표적인 예는 color 속성
- 상속되지 않는 속성
  - 요소의 상속되지 않는 속성에 어떤 값이 지정되지 않은 경우, 요소는 그 속성의 **초기값**을 얻음
  - 대표적인 예는 border 속성
