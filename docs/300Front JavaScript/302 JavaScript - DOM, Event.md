---
layout: default
title: JavaScript 기본 - DOM, Event
nav_order: 302
description: JavaScript 기본 - DOM, Event
parent: JavaScript
---

230803

# JavaScript - DOM, Event

생성 일시: 2023년 8월 2일 오후 8:50

- DOM
- Event

# DOM

---

## window 제공 함수

- alert
- confirm
- prompt
- open
- parseInt, parseFloat
- setTimeout, clearTimeout
- setInterval, clearInterval

![DOM, Event](https://github.com/yyoungl/yyoungl.github.io/assets/127117707/5fbc5918-5ac3-4dcf-85eb-9876408a40e2)

## DOM

![DOM, Event](https://github.com/yyoungl/yyoungl.github.io/assets/127117707/38f0ef96-4a15-45e9-983f-1d3fd00001cc)

- XML, HTML 문서의 각 항목을 계층으로 표현하여 생성, 변형, 삭제할 수 있도록 돕는 인터페이스
- DOM은 문서 요소 집합을 트리 형태의 계층 구조로 HTML 표현
- HTML 문서의 요소를 제어하기 위해 지원
- 상단의 document 노드를 통해 접근

## 문서 접근 방식 이해

- getElementById (string)
- querySelector(css selector)
- querySelectorAll(css selector)

### getElementById (string)

`JavaScript`

```jsx
var ele = document.getElemendById("a");
```

`HTML`

```html
<section>
	<h2>테스트</h2>
	<div id="a" class ="b">지역</div>
	<div class="b">광주</div>
	<div name="c">구미</div>
	<p name="c">대전</p>
	<p class="d">서울</p>
	<p class="e">부울경</p>
</section>
```

### querySelector (css selector)

```jsx
var ele = document.querySelector("#a");
var ele document.getElementById("a");
```

```jsx
var ele = document.querySelector(".b");
```

```jsx
var ele = document.querySelector("[name='c']");
// 똑같이 특정 Attribute를 가진 요소만 선택할 수 있음
// "[width=...]"
```

```html
<section> 
	<h2>테스트</h2>
	<div class="b">광주</div>
	<div class="b">광주</div>
	<div name="c">구미</div>
	<p name="c">구미</div>
	<p class="d">서울</p>
	<p class="e">부울경</p>
</section>
```

### querySelectorAll (css selector)

- querySelector와 사용방식 동일
- 결과를 배열처럼 사용
    
    ```jsx
    var list = document.querySelectorAll("div");
    for (var i=0; i<list.length; i++) {
    	console.log(list[i])
    }
    ```
    

```jsx
var ele = document.querySelectorAll("#a");
```

```jsx
var ele = document.querySelectorAll("div");
```

```jsx
var ele = document.querySelectorAll(".b");
```

```jsx
var ele = document.querySelectorAll("[name='c']");
```

```html
<section> 
	<h2>테스트</h2>
	<div class="b">광주</div>
	<div class="b">광주</div>
	<div name="c">구미</div>
	<p name="c">구미</div>
	<p class="d">서울</p>
	<p class="e">부울경</p>
</section>
```

## 문서 조작 방식 이해

- `createElement(tagName)`
- `createTextNode(text)`
- `appendChild(node)`
- `removeChild(node)`
- `setAttribute(name, value)`
- `innterHTML`
- `innerTEXT`

### createElement(string), append(string | node)

```jsx
// 엘리먼트 생성
var ele = document.createElement("img);
// 추가할 기존 엘리먼트 접근
var parent = document.getElementById("list");
// 엘리먼트 추가
parent.append(ele);
```

```html
<div id="list"></div>
// 매모리에 생성 (화면에 보이지 않는 상태) 
<img> 

-----------

<div id="list">
	<img>
</div>
```

### setAttribute(name, value)

```jsx
var ele document.createElement("img");

// 생성된 img 엘리먼트에 속성 추가하기
ele.setAttribute("src", "./images/cake.jpg");
ele.setAttribute("width", 200);
ele.setAttribute("height", 150);

ele.src="./images/cake.jpg";
ele.width=200;
ele.height=150;
```

```html
<img>

// 이게 이렇게 됨

<img src="./images/cake.jpg" width="200" height="150">
```

### 속성 설정 시 주의점 - 사용자 정의 속성

```jsx
var ele = document.createElement("img");
ele.setAttribute("src", "./images/cake.jpg");
ele.setAttribute("width", 200);
ele.setAttribute("height", 150);
ele.setATtribute("msg", "test");
```

```html
<img src = "./images/cake.jpg"
			width "200"
			height="150"
			msg="test"
>	
```

```jsx
ele.src = "./images/cake.jpg";
ele.width=200;
ele.height=150;
ele.msg="test"
```

```html
<img src="./imgaes/cake.jpg"
			width="200"
			height="150"
>
```

### innerHTML을 이용한 요소 내용 변경

조작할 엘리먼트 접근

```jsx
var list = document.getElementById("list");
```

```jsx
// 엘리먼트의 innerHTML을 접근
list.innerHTML
```

```html
<div id="list">

</div>
```

```jsx
// 처리할 작업 진행
list.innerHTML = "<img src='./images/cake.jpg"
	width='200' height='150' />";
```

```html
<div id="list"
	<img src="./images/cake.jpg"
		width='200' height='150 />
</div>
```