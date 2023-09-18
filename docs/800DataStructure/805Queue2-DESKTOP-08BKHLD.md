---
layout: default
title: 자료구조 Queue - 원형 큐, 우선순위 큐
nav_order: 805
parent: 자료구조
---

# 230821 큐 (Queue) (2)

생성 일시: 2023년 8월 18일 오전 11:56

- 원형큐
- 우선순위 큐

# 원형 큐 Circular Queue

---

## 원형 큐의 구조

### 초기 공백 상태

- front = rear = 0

### Index의 순환

- front와 rear의 위치가 배열의 마지막 인덱스인 n-1를 가리킨 후, 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동해야 함
- 이를 위해 나머지 연산자 mod 사용함

### front 변수

- 공백 상태와 포화 상태 구분을 쉽게 하기 위해 front가 있는 자리는 사용하지 않고 항상 빈자리로 둠

### 삽입 위치 및 삭제 위치

|        | 삽입 위치             | 삭제 위치               |
| ------ | --------------------- | ----------------------- |
| 선형큐 | rear = rear+1         | front = front+1         |
| 원형큐 | rear = (rear+1) mod n | front = (front+1) mod n |

## 원형 큐의 연산 과정

**1) create Queue**

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlVQxG%2FbtstG47GBHd%2FQU02AghrvxS0ua80bviBa0%2Fimg.png)

**2) enQueue(A)**

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKyOeh%2FbtstG5r1m83%2F9Sh6kiBFI5DRhz8LZowZ3K%2Fimg.png)

**3) enQueue(B)**

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVekga%2Fbtstzmud8DM%2FKCzbmupEfMSzIS4RId7nUk%2Fimg.png)

**4) deQueue()**

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdvy6VN%2FbtstKYTEpEI%2FgYiV3LhkY4WNv8KHQnMHy0%2Fimg.png)

**5) enQueue(C)**

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmgzKM%2FbtstyusCJ8m%2Fu3lMj5XZdGr1aVU1CzEmdk%2Fimg.png)

**6) enQueue(D)**

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbsttXJ%2FbtstzmHLz6a%2FPavTGdN0Sz4FLNSdOdzgL1%2Fimg.png)

### 초기 공백 큐 생성

- 크기 n인 1차원 배열 생성
- front와 rear를 0으로 초기화

### 공백 상태 및 포화 상태 검사: `isEmpty()` `isFull()`

- 공백 상태: front = rear
- 포화 상태: 삽입할 때 rear의 다음 위치 = 현재 front
  - (rear+1) mod n = front
  ```java
  isEmpty() {
  	if (front == rear) return true;
  	else return false;
  }
  isFull() {
  	if ((rear+1) mod n == front) return true;
  	else return false;
  }
  ```

### 삽입: enQueue(item)

- 마지막 원소 뒤에 새로운 원소를 삽입하기 위해

  1. rear 값을 조정하여 새로운 원소를 삽입할 자리를 마련함: rear = (rear+1) mod n;
  2. 그 인덱스에 해당하는 배열 원소 cQ[rear]에 item을 저장

     ```java
     enQueue(item) {
     	if (isFull()) print("Queue_Full")
     	else {
     		rear = (rear+1) mod n;
     		cQ[rear] = item;
     	}
     }
     ```

### 삭제: deQueue(), delete()

- 가장 앞에 있는 원소를 삭제하기 위해

  1. front 값을 조정하여 삭제할 자리를 준비함
  2. 새로운 front 원소를 리턴 함으로써 삭제와 동일한 기능

     **deQueue()**

     ```java
     deQueue() {
     	if (isEmpty()) print("Queue_Empty");
     	else {
     		front = (front+1) mod n;
     		return cQ[front];
     	}
     }
     ```

     **delete()**

     ```java
     delete() {
     	if (isEmpty()) print("Queue_Empty");
     	else front = (front+1) mod n;
     }
     ```

# 우선순위 큐 Priority Queue

---

## 우선순위 큐의 특성

- 우선순위를 가진 항목들을 저장하는 큐
- FIFO 순서가 아니라 우선순위가 높은 순서대로 먼저 나가게 된다

## 우선순위 큐의 적용 분야

- 시뮬레이션 시스템
- 네트워크 트래픽 제어
- 운영체제의 태스크 스케줄링

## 우선순위 큐의 구현

- 배열을 이용한 우선순위 큐
- 리스트를 이용한 우선순위 큐

## 우선순위 큐의 기본 연산

- 삽입: `enQueue`
- 삭제: `deQueue`
  ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbyN5Nn%2FbtstMgsYhP0%2FnVxR4UwOerLjXT42VyxJwk%2Fimg.png)

### 배열을 이용하여 우선순위 큐 구현

- 배열을 이용하여 자료 저장
- 원소를 삽입하는 과정에서 우선순위를 비교하여 적절한 위치에 삽입하는 구조
- 가장 앞에 최고 우선순위의 원소가 위치하게 됨

### 문제점

- 배열을 사용하므로 삽입이나 삭제 연산이 일어날 때 원소의 재배치가 발생함
- 이에 소요되는 시간이나 메모리 낭비가 큼
