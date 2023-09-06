---
layout: default
title: 자료구조 Queue - 정의, 특성, 선형 큐
nav_order: 505
parent: 자료구조
---

# 큐 (Queue) (1)

생성 일시: 2023년 8월 17일 오후 8:34

- 큐
- 선형큐
- 큐의 활용

# Queue

---

## 큐(Queue)의 특성

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
  - 큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 이루어지는 구조
- 선입선출구조 (FIFO: First In First Out)
  - 큐에 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입 (First In) 된 원소는 가장 먼저 삭제 (First Out) 된다

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbYg3WM%2FbtsteRurR9Y%2Fi63jn3oVQoFaadabo1erxK%2Fimg.png)

## 큐의 구조 및 기본 연산

### 큐의 선입선출 구조

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPx8kT%2FbtstkUjmfC9%2FahW3P1BsLNeQimZKskWKp1%2Fimg.png)

### 큐의 기본 연산

- 삽입: enQueue
- 삭제: deQueue

| 연산          | 기능                                                |
| ------------- | --------------------------------------------------- |
| enQueue(item) | 큐의 뒤쪽(rear 다음)에 원소를 삽입하는 연산         |
| deQueue()     | 큐의 앞쪽(front)에서 원소를 삭제하고 반환하는 연산  |
| createQueue() | 공백 상태의 큐를 생성하는 연산                      |
| isEmpty()     | 큐가 공백 상태인지를 확인하는 연산                  |
| isFull()      | 큐가 포화 상태인지를 확인하는 연산                  |
| Qpeek()       | 큐의 앞쪽(front)에서 원소를 삭제 없이 반환하는 연산 |

### 큐의 연산 과정

1. 공백 큐 생성: `createQueue();`

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbM96vq%2Fbtss9hniCOz%2FEwxJeRlC0cc19f1LVoUYtk%2Fimg.png)

2. 원소 A 삽입: `enQueue(A);`

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcvvBj2%2Fbtstk6cRKmi%2FErFX9JEkzmMKEwRKBiXIek%2Fimg.png)

3. 원소 B 삽입: `enQueue(B);`

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6rE6w%2FbtstfPbU8po%2FytPeQyi47JpkKKs1xXuDrk%2Fimg.png)

4. 원소 반환/삭제: `deQueue();`

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuYFt5%2FbtstfTk55qM%2FqAJsDTF0LX3mfSxlXdOfrk%2Fimg.png)

5. 원소 C 삽입: `enQueue(C);`

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FD1w3Q%2Fbtss9CEQW92%2Foqcaou9V6MVgeRgEoewsJK%2Fimg.png)

6. 원소 반환/삭제: `deQueue();`

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyKxNG%2FbtsteSNDMXE%2FNTvbxYV3gTtFta3Dkwxfu0%2Fimg.png)

7. 원소 반환/삭제: `deQueue();`

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdu5ONu%2FbtsteQI3jeM%2FZFBsr28NKc9CbMFZEQEck1%2Fimg.png)

# 선형 큐 (Linear Queue)

---

## 큐의 구현

### 선형 큐

- 1차원 배열을 이용한 큐
  - 큐의 크기 = 배열의 크기
  - front: 마지막으로 삭제된 인덱스
  - rear: 저장된 마지막 원소의 인덱스
- 상태 표현
  - 초기 상태: front = rear = -1
  - 공백 상태: front = rear
  - 포화 상태: rear = n-1 (n: 배열의 크기, n-1: 배열의 마지막 인덱스)

### 초기 공백 큐 생성

- 크기 n인 1차원 배열 생성
- front와 rear를 -1로 초기화

### 삽입: `enQueue(item)`

- 마지막 원소 뒤에 새로운 원소를 삽입하기 위해

  1. rear 값을 하나 증가시켜 새로운 원소를 삽입할 자리를 마련

  2. 그 인덱스에 해당하는 배열 원소 Q[rear]에 item을 저장

  ```java
  enQueue(item) {
  	if (isFull()) print("Queue_Full")
  	else {
  		rear = rear+1;
  		Q[rear] = item;
  	}
  }
  ```

### 삭제: `deQueue()`

- 가장 앞에 있는 원소를 삭제하기 위해

  1. front 값을 하나 증가시켜 큐에 남아 있는 첫 번째 원소로 이동

  2. 새로운 첫 번째 원소를 리턴 함으로써 삭제와 동일한 기능을 함

  ```java
  deQueue() {
  	if (isEmpty()) print("Queue_Empty")
  	else {
  		front = front+1;
  		return Q[front];
  	}
  }
  ```

### 공백 상태 및 포화 상태 검사: `isEmpty()`, `isFull()`

- 공백 상태: front=rear
- 포화 상태: rear=n-1 (n: 배열의 크기, n-1: 배열의 마지막 인덱스)
  ```java
  isEmpty() {
  	if (front == rear) return true;
  	else return false;
  }
  isFull() {
  	if (rear=n-1) return true;
  	else return false;
  }
  ```

### 검색: `Qpeek()`

- 가장 앞에 있는 원소를 검색하여 반환하는 연산
- 현재 front의 한자리 뒤 (front+1)에 있는 원소, 즉 큐의 첫 번째에 있는 원소를 반환
  ```java
  Qpeek() {
  	if (isEmpty()) print("Queue_Empty");
  	else return Q[front+1];
  }
  ```

## 연습문제1

**************************\*\***************************\*\***************************\*\***************************큐를 구현하여 다음 동작을 확인해 봅시다**************************\*\***************************\*\***************************\*\***************************

- 세 개의 데이터 1, 2, 3을 차례로 큐에 삽입하고
- 큐에서 세 개의 데이터를 차례로 꺼내서 출력한다
  - 1, 2, 3이 출력되어야

## 선형 큐 이용시의 문제점

### 잘못된 포화 상태 인식

- 선형 큐를 이용하여 원소의 삽입과 삭제를 계속할 경우, 배열의 앞부분에 활용할 수 있는 공간이 있음에도 불구하고, rear=n-1 인 상태 즉, 포화상태로 인식하여 더 이상의 삽입을 수행하지 않게 됨
  ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVl7GG%2FbtstghlUdJA%2FQIAzKzfFN6eNLKv841Yy30%2Fimg.png)

**해결방법 1**

- 매 연산이 이루어질 때마다 저장된 원소들을 배열의 앞부분으로 모두 이동시킴
- 원소 이동에 많은 시간이 소요되어 큐의 효율성이 급격히 떨어짐
  ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvAZ4h%2Fbtss9lb6WaH%2FxAEd1EHxRE7MqIXKLVmiX0%2Fimg.png)

**해결방법 2**

- 1차원 배열을 사용하되, 논리적으로는 배열의 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용
- 원형 큐의 논리적 구조
  ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7c0B1%2FbtstfSfo0nZ%2FFVjI3jDU95zc1Hk4GLM641%2Fimg.png)

다음 글에서는 원형 큐를 만나보자!
