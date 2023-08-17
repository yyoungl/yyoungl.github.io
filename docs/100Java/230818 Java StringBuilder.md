---
layout: default
title: JAVA StringBuilder
nav_order: 112
description: JAVA StringBuilder
parent: Java
---

# Java StringBuilder Class

문자열 폭발 문제에서 날 구해준 StringBuilder 클래스에 대한 오라클 문서를 살펴보았다.

전에 짝꿍이 쓰는 걸 봤는데 이번에 어떤 메소드가 있는지 제대로 알아보았다.

# StringBuilder

## StringBuilder란

---

[Java Development Kit Version 20 API Specification](https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/lang/StringBuilder.html)

```java
public class StringBuilder
extends object
implements Serializable, Comparable<StringBuilder>, CharSequence
```

StringBuilder란 변경 가능한 문자들의 나열(sequence)이다. StringBuffer와 비슷하지만, 동기화를 보장할 수는 없다.

일반적인 경우, StringBuffer보다 빠르다. … 고 써있다.

StringBuilder는 single thread에서 적합하기 때문에 multiple thread에서 StringBuilder의 인스턴스들은 안전하진 않아서 multiple thread 에서 사용해야 한다면 StringBuffer를 사용하는 것을 권장한다.

## StringBuilder 사용하기

---

### 생성하기

```java
StringBuilder sb = new StringBuilder();
StringBuilder sb = new StringBuilder(int capacity);
StringBuilder sb = new StringBuilder(CharSequence seq);
StringBuilder sb = new StringBuilder(String str);
```

### `StringBuilder()`

StringBuilder는 기본 16개 character만큼의 공간이 주어진다.

### `StringBuilder(int capacity)`

16칸이 아닌 capacity 만큼의 공간이 할당되어 생성된다.

### `StringBuilder(CharSequence seq)`

charsequence(char 값을 읽을 수 있는 시퀀스라고 함)

`16 + seq.length()` 만큼의 공간이 할당되고, 해당 문자열이 입력된다.

### `StringBuilder(String str)`

`16 + seq.length()` 만큼의 공간이 할당되고, 해당 문자열이 입력된다.

### 관련 메소드

자주 사용할 만한 메소드만 골라 보았다.

### `append()` 문자 붙이기

```java
StringBuilder sb = new StringBuilder();
StringBuilder sb.append(char c);
StringBuilder sb.append(String s);
StringBuilder sb.append(int i);
StringBuilder sb.append(StringBuffer sbf);
```

### `delete()` 삭제하기

```java
void sb.delete(int start, int end); // 시작 인덱스부터 끝 인덱스 전까지 해당하는 문자 삭제
void sb.deleteCharAt(int index); // 인덱스에 해당하는 문자 삭제
```

### `indexOf()` 특정 문자열 검색

```java
int sb.indexOf(String str); // str이 처음 등장하는 문자열의 시작 인덱스 반환
int sb.indexOf(String str, int fromIndex); // fromIndex부터 str에 해당하는 문자열이 시작되는 인덱스 반환
```

### 문자열 조작

```java
StringBuilder sb.insert(int offset, ___); // offset에 문자열 삽입
void setLength(int newLength); // 길이 초기화 (앞에서부터)
String sb.subString(int start, int end);
String sb.subString(int start); // start ~ end 전까지 자르고 문자열 return
String sb.toString() // 문자열로 바꾸기
```
