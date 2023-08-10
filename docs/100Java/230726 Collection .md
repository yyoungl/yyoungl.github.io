---
layout: default
title: JAVA Collection
nav_order: 109
description: JAVA 객체지향 Collection
parent: Java
---

# 230726 JAVA Collection

생성 일시: 2023년 7월 25일 오후 4:26

🌍**_[TISTORY](http://letusgrow.tistory.com)_**

- Collection Framework
  - List
  - Set
  - Map
  - Queue
  - Stack
- 정렬

# Collection Framework

---

- 틀, 뼈대: 객체들을 한곳에 모아 놓고 편리하게 사용할 수 있는 환경을 제공
  - 인터페이스의 일종이라고 생각하면 됨! (강제성, 독립성)
- 정적 자료구조 (Static data structure)
  - 고정된 크기의 정적 자료구조
  - 배열이 대표적인 정적 자료구조
  - 선언 시 크기를 명시하면 바꿀 수 없음
- 동적 자료구조 (Dynamic data structure)
  - 요소의 개수에 따라 자료구조의 크기가 동적으로 증가하거나 감소
  - 리스트, 스택, 큐 등
- 자료구조들의 종류는 결국은 어떤 구조에서 얼마나 빨리 원하는 데이터를 찾는가에 따라 결정된다
  - 순서를 유지할 것인가?
  - 중복을 허용할 것인가?
  - 다른 자료구조들에 비해서 어떤 단점과 장점을 가지고 있는가?
    ![Collection](https://github.com/yyoungl/yyoungl.github.io/assets/127117707/6ac897fa-0636-4f37-85be-6dfd13a70bb6)

!! `Map`은 Collection에서 상속받진 않지만 일종으로 묶여서 불림

## `java.util` 패키지

- 다수의 데이터를 쉽게 처리하는 방법 제공

### Collection Framework 핵심 interface

| interface | 특징                                        |
| --------- | ------------------------------------------- |
| List      | 순서가 있는 데이터의 집합, 데이터 중복 가능 |

ex 일렬로 줄 서기
ArrayList, LinkedList, Vector |
| Set | 순서를 유지하지 않는 데이터의 집합, 데이터 중복 불가
ex 로또 당첨 번호
HashSet, TreeSet… |
| Map | key와 value의 쌍으로 데이터를 관리하는 집합, key의 중복 불가, value는 중복 가능
ex 속성 - 값
HashMap, TreeMap |
| Queue | 지하철, 버스를 탈 때 대기줄과 같이 들어온 순서대로 나가는 자료구조
LinkedList |

### Collection interface

| 분류                              | Collection         |
| --------------------------------- | ------------------ |
| 추가                              | add(E e)           |
| addAll(Collection <? extends E>c) |
| 조회                              | contains(Object o) |

containsAll(Collection<?> c)
equals()
isEmpty()
iterator()
size() |
| 삭제 | clear()
removeAll(Collection<?> c)
retainAll(Collection<?> c) |
| 수정 | |
| 기타 | toArray() |

# List

---

## List

- 특징: 순서가 있고, 중복을 허용 (배열과 유사)
- 구현 클래스
  - ArrayList
  - LinkedList
  - Vector
- 내부적으로 배열을 이용하여 데이터를 관리
- 배열과 다르게 크기가 **유동적**으로 변함 (동적 자료구조)
- 배열을 다루는 것과 유사하게 사용할 수 있음
- 주요 메서드
  | 분류 | Collection | List |
  | -------------------------------------------- | ------------------------- | ---- |
  | 추가 | add(E e), |
  | addAll(Collection<? extends E> c) | add(int index, E element) |
  | addAll(int index, Collection<? extends E> c) |
  | 조회 | contains(Object o) |
  containsAll(Collection<?> c)
  equals()
  isEmpty()
  iterator()
  size() | get(int index)
  indexOf(Object o)
  lastIndexOf(Object o)
  listIterator() |
  | 삭제 | clear()
  removeAll(Collection<?> c)
  retainAll(Collection<?> c) | remove(int index) |
  | 수정 | | set(int index, E element) |
  | 기타 | toArray() | subList(int fromIndex, int toIndex) |

## 주요 메서드

```java
//문자열을 저장할 List, 구현체는 ArrayList
List<String> names = new ArrayList<>();

//추가
names.add("양만춘");
names.add("홍길동");
names.add("양만춘");
names.add("이순신");
names.add(0, "임꺽정");

System.out.println(names);
```

## Array 복습

- 같은 타입의 데이터를 묶어 사용하는 자료구조
- 접근 속도가 빠름
  메모리 공간에 할당되어 저장되기 때문에 주소값을 알고 있어서 빠르게 접근 가능
- 크기를 변경할 수 없어 추가 데이터를 넣을 때, 새로운 배열을 만들고 복사함
- 데이터 삭제 시, 인덱스를 재조정하기 위해 전체 데이터를 옮겨야 함
- ArrayList 역시 Array를 활용하므로 이 같은 특징을 가지고 있음

## ArrayList

- `add(E e)`데이터 입력
- `get(int index)` 데이터 추출: 인덱스로 바로 접근할 수 없으므로 `get` 활용
  - 인덱스로만 get 할 수 있나 보네…
- `size()` 입력된 데이터의 크기 반환
- `remove(int i)` 특정한 데이터를 삭제: 인덱스로 삭제
- `remove(Object o)` 특정한 데이터를 삭제: o 에 해당하는 데이터 삭제
- `clear()` 모든 데이터 삭제
- `contains(Object o)` 특정 객체가 포함되어 있는지 체크
- `isEmpty()` 비어있는지 체크 (true, false return)
- `addAll(Collection c)` 기존 등록된 콜렉션 데이터 입력
- `iterator()` iterator 인터페이스 객체 반환

## LinkedList

- 각 요소를 Node로 정의하고 node는 다음 요소의 참조 값과 데이터로 구성됨
- 각 요소가 다음 요소의 링크 정보를 가지며 연속적으로 구성될 필요가 없음
  ![Collection 1](https://github.com/yyoungl/yyoungl.github.io/assets/127117707/11259801-3c30-40b6-8700-3e8abac83818)

# Set

---

## Set

- 집합을 나타내는 자료 구조
- 특징: 순서가 없고, 중복을 허용하지 않음
- 장점: 빠른 속도, 효율적인 중복 데이터 제거 수단
- 단점: 단순 집합의 개념으로 정렬하려면 별도의 처리가 필요함
- 구현 클래스
  - **HashSet**
    - 해시 테이블에 원소를 저장
    - 성능면에서 우수하다고 알려져 있음
    - 원소들의 순서가 일정하지 않음
  - TreeSet (Binary Search Tree) → 지금 할 필요는 없음
    - red-black tree에 원소 저장
    - 값에 따라서 순서가 결정
    - 값을 순서대로 정렬할 필요가 있다면 고려해 볼 만한 선택지

### Hash??

값을 하나하나 비교하는 equals로 값을 찾음, hash 연산값이 다르면 다른 값으로 판단

값의 크기가 클수록 값들의 중복은 줄어들지만 차지하는 메모리가 많아짐

- `add(E e)` 데이터 입력
- `size()` 입력된 데이터의 크기 변환
- `remove(Object o)` 특정한 데이터를 삭제
- `clear()` 모든 데이터 삭제
- `contains(Object o)` 특정 객체가 포함되어 있는지 체크
- `isEmpty()` 비어있는지 체크 (true, false return)
- `iterator()` iterator 인터페이스 객체 반환
- `toArray()` Set의 내용을 Object 형의 배열로 반환

# Map

---

## Map

- 사전과 같은 자료구조
- 특징: Key(키)와 value(값)를 하나의 Entry로 묶어서 데이터 관리
- 순서는 없으며, 키에 대한 중복은 없음! 값은 중복될 수 있음
- 장점: 빠른 속도
- 구현 클래스
  - HashMap
    ```java
    Map<키 자료형, 값 자료형> map = new HashMap<>();
    HashMap<String, String> map = new HashMap<>();
    ```
  - TreeMap
- `V put(K key, V value)` 데이터 입력
  - 중복된 키값을 넣으면 새로운 값으로 바뀜 → 덮어쓰기!
- `V get(Object key)` 데이터 추출
- `V remove(K key)` 키의 값을 지우고 반환, 없다면 `null`을 반환
- `boolean containsKey(Object key)` 특정한 key 포함 여부
- `void putAll(Map<K key, V value> m)` 기존 콜렉션 데이터 추가
- `Set<Map.Entry<K, V>> entrySet()`
  - (key와 value) 쌍을 표현하는 Map, Entry 집합을 반환

# Queue

---

## Queue

- queue는 인터페이스, 구현체는 LinkedList를 사용
- 큐 자료구조: FIFO, (first-in-first-out) 가장 먼저 들어온 값이 가장 먼저 빠져나감
- `boolean offfer(E e)` 데이터를 추가
- `E peek()` 가장 앞에 있는 데이터 조회
- `E poll()` 가장 앞에 있는 데이터 빼내기
- `boolean isEmpty()` 큐가 비어 있는지 여부

# Stack

---

## Stack

- Stack 클래스를 사용
- 스택 자료구조: LIFO, (last-in-first-out) 가장 나중에 들어온 값이 가장 먼저 빠져나감
- `E push(E e)` 데이터를 추가
- `E peek()` 가장 위에 있는 데이터 조회
- `E pop()` 가장 위에 있는 데이터 빼내기
- `boolean isEmpty()` 스택이 비어 있는지 여부

# 정렬

---

- 요소들을 특정 기준에 맞추어 내림차순 또는 오름차순으로 배치하는 것
- 순서를 가지는 Collection들만 정렬 가능
- Collections의 sort()를 이용한 정렬

### Comparable interface

T와 o를 비교한 후 뺀 값 (T-o) 에 따라서 결과값이

- 양수: 자리 바꿈
- 음수: 자리 유지
- 0: 동일 위치

```java
public interface Comparable<T> {
	public int compareTo(T o);
}
```

ex 숫자를 기준으로 기본 `오름차순` 정렬인데, 예를 들어 `56, 20` 두 숫자 56 - 20 > 0 일 경우 자리 바꾸기

### Comparator의 활용

- 객체가 Comparable을 구현하고 있지 않거나 사용자 정의 알고리즘으로 정렬하려는 경우
  - String을 알파벳 순이 아니라 글자 수 별로 정렬을 하고 싶다
- `sort(List<T> list, Comparator<? Super T> c)`
  ```java
  public interface Comparator<T> {
  	int compare(T o1, T o2);
  }
  ```
  ```java
  public class StringLengthComparator implements Comparator<String> {
  	@Override
  	public int compare(String o1, String o2) {
  		int len1 = o1.length();
  		int len2 = o2.length();
  		return Integer.compare(len1, len2);
  	}
  }
  public void istringLengthSort() {
  	Collections.sort(names, new StringLengthComparator());
  	System.out.println(names);
  }
  ```
- 1회성 객체 사용 시 anonymous inner class 사용
- 클래스 정의, 객체 생성을 한번에 처리

  ```java
  //before
  Collections.sort(names, new StringLengthComparator());

  //after
  Collections.sort(names, new Comparator<String>() {
  	@Override
  	public int compare(String o1, String o2) {
  		return Integer.compare(o1.length(), o2.length());
  	}
  });
  ```

- 람다 표현식 사용
  ```java
  Collections.sort(names, (o1, o2) -> {
  	return Integer.compare(o1.length(), o2.length());
  });
  ```

## ** 실습 내용 중 **

### toArray 메소드

---

```java
list.toArray(res);
```

res라는 array에 list를 넣는다는 느낌인 듯. 하지만 res라는 array는 list의 사이즈만큼의 공간으로 만들어 줘야 함
