---
layout: default
title: JavaScript 기본 - 객체, 함수
nav_order: 301
description: JavaScript 기본 - 객체, 함수
parent: JavaScript
---

# 230802 JavaScript

생성 일시: 2023년 8월 1일 오후 8:10

- JavaScript
- 기본 문법
- 객체
- 함수

# JavaScript

---

## 자바스크립트란?

- 프로토타입 기반 객체 생성을 지원하는 동적 스크립트 언어
- 웹 브라우저에서 주로 사용, Node.js를 이용하여 콘솔 환경에서 사용
- 웹 브라우저의 UI를 제어하기 위해 만들어진 프로그래밍 언어
- 자바와 기본 구문이 비슷하다 (C언어의 기본 구문을 바탕으로 함)
- Mocha → LiveScript → JavaScript

- ECMA International: 정보 통신에 대한 표준을 제정하는 비영리 표준화 기구
- ECMAScript: ECMA-262 기술 규격에 의해 정의된 범용 스크립트 언
- EMCAScipt6: ECMA에서 제안하는 6번째 표준 명세 (2015 발표)

# 기본 문법

---

## HTML 자바스크립트 사용

- `<script>` `</script>` 태그를 사용
- 문서 내 위치 제약이 없다
    
    ```html
    <html>
    <head>
    	<meta charset="UTF-8">
    	<title>JavaScript</title>
    	<script>console.log('head');</script>
    </head>
    <body>
    	<script>console.log('body');</script>
    </body>
    </html>
    ```
    

## 외부 스크립트 참조하기

- `.js` 확장자를 가진 파일을 생성
- html 문서에서 `<script src=”외부 파일의 위치”></script>`

### 주석

```jsx
// 한줄 주석
/*
	여러 줄 주석
*/
```

## 변수 (Variable)

- 자바스크립트의 변수 타입은 가리키는 값에 대한 타입을 나타낸다
- var, let, const 키워드를 이용해서 변수를 선언
- var를 이용한 변수의 선언일 경우 중복 선언이 가능
- undefined는 변수에 아무 값도 없어서 타입을 알 수 없는 경우를 말한다
- 동적 타입: 대입되는 값에 따라서 용도가 변경되는 방식
- 문자, $, _ 로 시작, 대소문자 구분, 예약어 사용 X

### var

- 재 선언 가능, 재 할당 가능
- ES6 이전에 변수 선언 시 사용
- 호이스팅 (Hoisting) 특성이 있음
- 함수 스코프

```jsx
var id = "hong";
console.log(id);
var id = "kim";
console.log(id);
```

호이스팅??

### let

- 재선언 불가, 재할당 가능
- 블록 스코프

```jsx
let id = "hong";
console.log(id);
let id = "kim";
console.log(id);
```

### const

- 재선언 불가, **재할당 불가**
- 블록 스코프
- 대문자 SNAKE_CASE 사용
- 선언 시 값을 할당해야 함
- 상수로 사용

```jsx
const id = "hong";
console.log(id);
id = "kim"; // error
console.log(id);
```

### undefined

- 변수에 값이 대입되지 않은 상태

```jsx
var name;
console.log(name);
```

## 데이터 타입 (Data Type)

- 기본 데이터 타입 (Primitive Type)
    - String, Number, Boolean, null, undefined
- 객체 타입 (Reference Type)
    - Object - function, array 등

** es6 추가된 타입: Symbol (변경 불가능한 기본 타입)

## typeof - 변수의 자료형 검사

```jsx
console.log(typeof ("test")); //string
console.log(typeof (10)); // number
console.log(typeof (true)); //boolean
console.log(typeof (null)); //object
console.log(typeof (a)); //undefined
console.log(typeof ({}))); //object
console.log(typeof (function () {})); //function
console.log(typeof (Symbol()) //symbol
```

- typeof 데이터
- typeof (데이터)
- typeof 의 결과는 문자열 반환

- null의 데이터 타입은 null이 아닌 object (설계 실수 ㅋㅋㅋ)
- function은 기능을 가진 객체

**es6 추가된 타입: Symbol (변경 불가능한 기본 타입)

### 동적 데이터 타입 - 다양한 값의 대입이 가능

```jsx
var val = 10;
console.log(val, typeof(val)); // 10 'number'
val = hello;
console.log(val, typeof(val)); // hello string
val = true;
console.log(val, typeof(val)); // true 'boolean'
```

## 숫자형 (Number)

- 정수와 실수로 나누어 구분하지 않음. (부동소수점 형식)
- 일반적인 숫자와 특수 숫자 포함 (infinity, NaN, …)
- e를 활용하여 거듭제곱 표현 가능

## 문자열 (String)

- `""`로 감싼다.
- `''`로 감싼다.
- ````(backtick)으로 감싼다. -> Template Literal (ES6)
여러 줄 입력이 가능 - 공백, 줄 넘김 유지
문자열 내 `$(변수명)`을 이용하여 변수와 문자열을 결합
- UTF-16 형식

```jsx
let msg = "자바스크립트 문자열";
msg = '자바스크립트 문자열';
msg = `자바스크립트 문자열`;

let name =  "홍길동";
msg = `나의 이름은 ${name}입니다.`;

let msg2 = `저의 이름은 홍길동입니다.`;
```

### 문자열 연산

- 문자열과 숫자 타입의 + 연산 → 문자열
- 문자열과 숫자 타입의 + 연산 이외 → 숫자

## 자바스크립트 `false`

- 아래의 5가지 값은 `false`로 인식, 나머지 값은 `true`로 인식
- `null`
- `undefined`
- `0`
- `'' (빈 문자열)`
- `NaN`

## 연산자 (Operator)

- + 덧셈, 단항 사용시 Number()와 동일한 역할
- -
- *
- /
- %
- **
- = 할당 연산자
- +=, -=, *=, … 복합 할당 연산자
- ++, — 증감 연산자

### 일치 연산자

- 값과 타입이 일치하는지 체크
- `===` `!==`
- 두 개 쓸 경우, **값만 일치**하는지 체크
- 세 개 쓸 경우, **타입까지 일치**하는지 체크

## 제어문 (Java 유사)

- 조건문 (Condition)
    - if
    - switch
- 반복문 (Loop)
    - for
    - while
    - do-while

## 배열 (Array)

- 배열의 생성: [] 또는 Array() 활용
- 배열의 크기는 동적으로 변경된다
- 크기가 지정되어 있지 않은 경우에도 데이터의 입력 가능
- 배열의 길이는 가장 큰 인덱스 +1 한 값이다
- 배열은 여러가지의 데이터 타입을 하나의 배열에 입력할 수 있다
- `push` 함수를 이용하여 데이터 추가 가능

```jsx
var arr1 = [];
var arr2 = new Array();

arr[0] = 10;
arr[2] = 30;
console.log(arr1[0], arr1[1], arr1[2]); // 10 undefined 30
console.log(arr1.length); //3

arr1[3] = "문자열";
arr1[4] = {};
arr1[5] = [1, 2, 3];
arr1[6] = true;
arr1.push("추가");
```

# 객체 Object

---

## 객체 (Object)

- 객체는 문자열로 이름을 붙인 값들의 집합체이다. (Key : Value)
    
    key만 출력하는 법!!
    
    ```jsx
    for (key in object) {
    	console.log(key)
    }
    ```
    
- 객체에 저장하는 값을 프로퍼티 (Property) 라고 한다.
- 객체는 prototype 이라는 특별한 프로퍼티를 가지고 있다.

### 객체 (Object) 만들기

- 객체 리터럴 이용: {}
- Object 생성자 이용: `new Object()`
- 생성자 함수 이용

```jsx
let member1 = {}
let member2 = new Object();
function Member() {}
let member3 = new Member()
```

******************************객체 (Object) 생성 시 프로퍼티 추가******************************

```jsx
let member1 = {id: "why", email: "ssafy@a.com"}
function Member(id, email) {
	this.id = id;
	this.email = email;
}
let member2 = new Member("shy", "ssafy@a.com");
```

************************************************객체 (Object) 프로퍼티************************************************

- `.`(dot) 또는 `[]`를 이용하여 프로퍼티의 조회 및 변경을 처리한다.

```jsx
let student = {
	name: "김싸피",
	age: 20,
	hobby: ["공부", "숙면"],
	"favorite singer": "아이유",
};
```

```jsx

```

### 추가/수정/삭제

```jsx
var member = {"id": "hong", "email": "hong@a.com"};
member.namer = "홍길동";
console.log(member);
```

```jsx
let member = {id: "shy", email: "ssafy@a.com"}
member["id"] = "ssafy";
member.email = "ssafy@ssafy.com";
```

```jsx
let member = {id: "shy", email: "ssafy@a.com"}
delete member.id;
console.log(member);
```

- 객체 변수에는 주소가 저장되어 공유 가능

```jsx
let member1 = {id: "hong", email: "hong@a.com"}
let member2 = member1;
member2.id = "kang";

console.log(member1.id); // kang
console.log(member2.id); // kang
```

- 함수 안에서의 `this`는 함수를 호출한 객체

```jsx
var m1 = {name: "홍길동"};
var m2 = {name: "배수지"};
function msg() {
	console.log(this);
	console.log(this.name + "님이 입장함...");
}
m1.msg = msg;
m2.msg = msg;
m1.msg();
m2.msg();
```

# 함수 function

---

## 함수 특징

- 자바스크립트에서 함수는 객체 타입으로 값처럼 사용이 가능하다
- 함수를 변수에 대입하거나 매개변수로 넘길 수 있다
- 배열의 요소에 넣거나 객체의 프로퍼티로 설정이 가능하다
- 매개변수의 개수가 일치하지 않아도 호출이 가능하다
- JavaScript의 함수는 일급 객체 (First-class citizen) 에 해당
    - 변수에 할당 가능
    - 함수의 매개변수로 전달 가능
    - 함수의 반환 값으로 사용 가능

### 함수 만들기

- 함수 선언식 (function declaration)
    
    ```jsx
    function 함수명() { 함수 내용 }
    ```
    
    - 함수의 이름과 함께 정의하는 방식
    - 함수의 이름
    - 매개 변수
    - 내용
    - 호이스팅 됨
- 함수 표현식
    
    ```jsx
    let 함수명 = function() { 함수 내용 }
    ```
    
    - 익명함수로 정의 가능
    - 매개 변수
    - 내용

### 선언식 vs 표현식

- 선언식 함수는 호이스팅의 영향을 받아 함수 선언 이전에 호출이 가능하다
- 표현식 함수는 선언 이전에 호출이 불가능하다
    
    
    ```jsx
    func();
    
    function func() {
    	console.log('선언식');
    }
    ```
    
    호출 가능
    
    ```jsx
    func();
    
    let func = function() {
    	console.log('표현식');
    };
    ```
    
    호출 불가능
    

### 함수의 리턴

- 함수의 실행 결과로 함수를 반환할 수 있다
- 함수가 특별한 값을 리턴하지 않은 경우 `undefined`가 반환된다
    
    
    ```jsx
    function func() {
    	return function (num1, num2) {
    		return num1 + num2;
    	}
    }
    
    function func2() {}
    ```
    
    ```jsx
    let callFn = func();
    let result = callFn(100, 200);
    console.log(result);
    
    console.log(func2()); // undefined 출력
    ```
    

### 함수 호출

- 정의된 함수를 호출 시 함수를 값으로 넘길 수 있다
    
    
    ```jsx
    function func(callFn) {
    	callFn('hello');
    }
    
    function fn(msg) {
    	console.log(msg);
    }
    ```
    
    ```jsx
    func(fn);
    ```
    

## 함수 매개변수

- 함수는 호출 시 매개변수의 영향을 받지 않는다
- `arguments`라는 함수 내부의 프로퍼티를 이용하여 매개변수의 처리가 가능하다
- 자바스크립트의 함수는 오버로딩 개념을 지원하지 않는다
- 기본 인자 (default arguments) 를 사용할 수 있다

```jsx
function fn1(num) {
	console.log("fn1", num)
}
```

```jsx
fn1(); // undefined
fn1(100); // 100
fn1(100, 100); // 100
```

## 함수 매개변수

```jsx
function fn() {
	console.log(arguments.length);
	for (let i=0; i<arguments.length; i++) {
		console.log(arguments[i]);
	}
}
```

```jsx
fn(1);
1
1
fn(1, 10, 100);
3
1
10
100
```

```jsx
function fn() {
	console.log(1);
}
function fn() {
	console.log(2);
}
function fn(num) {
	console.log(num);
}
```

```jsx
fn();
// undefined
fn(1);
1
```