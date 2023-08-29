---
layout: default
title: JAVA String
nav_order: 112
description: JAVA String
parent: Java
---

## 문자열

### 문자열의 분류

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbIFgi1%2FbtssBlWl4tk%2FZdKfFysLOLY7CSONr8r3A0%2Fimg.png)

### java 클래스에서 String 클래스에 대한 메모리 배치 예

- 그림에서 보이듯, java.lang.String 클래스에는 기본적인 메타 데이터 외에도 네 가지 필드들이 포함되어 있는데, hash값 (hash), 문자열의 길이 (count), 문자열 데이터의 시작점 (offset), 그리고 실제 문자열 배열에 대한 참조 (value) 이다

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBEuXt%2Fbtssuv0hhEb%2F2svC3YK9v8Hgd5cRfGkZd0%2Fimg.png)

### C언어에서 문자열 처리

- 문자열은 문자들의 배열 형태로 구현된 응용 자료형
- 문자배열에 문자열을 저장할 때는 항상 마지막에 끝을 표시하는 널문자(`\0`)을 넣어줘야 한다.
- `char ary[] = {'a', 'b', 'c', '\0'}; // 또는 char aryp[="abc";`
- 문자열 처리에 필요한 연산을 함수 형태로 제공한다
- `strlen(), strcpy(), strcmp(), ...`

### Java(객체지향 언어)에서의 문자열 처리

- 문자열 데이터를 저장, 처리해주는 클래스를 제공한다
- String 클래스를 사용한다
- `String str = "abc"; // 또는 String str = new String("abc");`
- 문자열 처리에 필요한 연산을 연산자, 메소드 형태로 제공한다
  - `+`, `lenght()`, `replace()`, `split()`, `substring()`, …

### C와 Java의 String 처리의 기본적인 차이점

- C는 아스키 코드로 저장한다
- java는 유니코드 (UTF16, 2byte)로 저장한다
- 파이썬은 유니코드 (UTF8)로 저장

**C**

```
char * name = "홍길동";
int count = strlen(name);
printf("%d", count);
```

6 출력

**Java**

```
String name = "홍길동";
System.out.println(name.length());
```

**Python**

```
name = "홍길동"
print(len(name))
```

3 출력

3 출력

## 문자열 뒤집기

- 자기 문자열에서 뒤집는 방법이 있고 새로운 빈 문자열을 만들어 소스의 뒤에서부터 읽어서 타겟에 쓰는 방법이 있겠다
- 자기 문자열을 이용할 경우는 swap을 위한 임시 변수가 필요하며 반복 수행을 문자열 길이의 반만을 수행해야 한다

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlfCh8%2FbtsswkcS1hw%2FVkp1tn6UaGbkIQpeZewoN1%2Fimg.png)

### 문자열 비교

- c: `strcmp()` 함수 제공
- Java에서는 `equals()` 메소드 제공
  - 문자열 비교에서 `==` 연산은 **메모리 참조가 같은지**를 묻는 것
- python에서는 `==` 연산자와 `is` 연산자를 제공한다
  - `==` 연산자는 내부적으로 특수 메서드 `__eq__()`를 호출

```
String s1 = "Hi";
String s2 = "Hello";
if(s1.equals(s2)==true) {
    System.out.println("Equal");
} else if (s1.equals(s2)==false) {
    System.out.println("Not Equal");
}
```

### 문자열 숫자를 정수형으로 반환

- c 언어에서는 `atoi()` 함수를 제공한다. 역 함수로는 `itoa()`가 있다.
- java에서는 숫자 클래스의 `parse` 메소드를 제공한다역함수로는 toString() 메소드를 제공한다
- ex) Integer.parseInt(String)
- python에서는 숫자와 문자 변환 함수를 제공한다
- ex) `int(”123”)`, `float(”3.14”)`, `str(123)`, `repr(123)`

## `atoi()`

```
int atoi(char[] charArr) {
    int value = 0;
    int digit;
    for (int i=0; i<charArr.length; i++) {
        if (charArr[i] >= '0' && charArr[i] <= '9')
            digit = charArr[i] - '0';
        else break;
        value = (value*10) + digit;
    }
    return value;
}
```

### 문자열 매칭 알고리즘 비교

- 찾고자 하는 문자열 패턴의 길이 m, 총 문자열 길이 n
- 고지식한 패턴 알고리즘: 수행시간 O(mn)
- 카프-라빈 알고리즘: 수행시간 Θ(n)
- KMP 알고리즘: 수행시간 Θ(n)
- 보이어-무어 알고리즘
  - 앞의 두 매칭 알고리즘들의 공통점은 텍스트 문자열의 문자를 적어도 한 번씩 훑는다는 것이다. 따라서 최선의 경우에도 Ω(n)
  - 보이어-무어 알고리즘은 텍스트 문자를 다 보지 않아도 된다
  - 발상의 전환: 패턴의 오른쪽부터 비교한다
  - 최악의 경우 수행시간: O(mn)
  - 입력에 따라 다르지만 일반적으로 Θ(n)보다 시간이 덜 든다

# 문자열 암호화

---

### 시저 암호(Caesar dipher)

- 줄리어스 시저가 사용했다고 하는 암호이다
- 시저는 기원전 100년 경에 로마에서 활약했던 장군이었다
- 시저 암호에서는 평문에서 사용되고 있는 알파벳을 일정한 문자 수만큼 \[평행이동\] 시킴으로써 암호화를 행한다

### 1만큼 평행했다는 카이사르 암호화의 예

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWLvmN%2FbtssvwLl9IZ%2F2xKyQkTMzNKb0DzljW7y81%2Fimg.png)

- 1만큼 평행했을 때 1을 키값이라 한다
- 수신자 이외의 사람(키가 1이라는 사실을 모르는 사람)이 암호문을
- 다른 정보 없이도 원본 메시지를 맞힐 수 있을까?
- 다시 말해, 시저 암호를 해독할 수 없을까?
