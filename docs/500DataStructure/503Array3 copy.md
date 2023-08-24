---
layout: default
title: 자료구조 Array(3) - 이차원 배열
nav_order: 503
description: 이차원 배열
parent: 자료구조
---


# 2차원 배열

---

## 2차원 배열의 선언

-   2차원 이상의 다차원 배열은 차원에 따라 Index를 선언
-   2차원 배열의 선언: 세로길이 (행의 개수), 가로길이 (열의 개수) 를 필요로 함

```
int[][] twoDimArr = new int[2][4]
// (2행 4열의 2차원 배열 선언)
```

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPFa4Z%2Fbtsr5KWvAqX%2Fb8arIcKpUfykCPiLEsdpU0%2Fimg.png)

## 배열 순회

-   n X m 배열의 n \* m 개의 모든 원소를 빠짐없이 조사하는 방법

### 행 우선 순회

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fl4OMa%2Fbtsr3btObfQ%2F3W0GWK5W0eCVLudFBKvgX0%2Fimg.png)

```
int i; // 행의 좌표
int j; // 열의 좌표

for i from 0 to n-1
    for j from 0 to m-1
        Array[i][j] // 필요한 연산 수행
```

### 열 우선 순회

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FE9LtS%2FbtsrTouvcCI%2FyyGV7Prn1r9CDeEheREbbk%2Fimg.png)

```
int i; // 행의 좌표
int j; // 열의 좌표

for j from 0 to m-1
    for i from 0 to n-1
        Array[i][j] // 필요한 연산 수행
```

### 지그재그 순회

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUhoAe%2FbtsrZBsJTr0%2FOK5Hpvt6903gvVVBrEcPjK%2Fimg.png)

```
int i; // 행의 좌표
int j; // 열의 좌표

for i from 0 to n-1
    for j from to m-1
        Array[i][j+(m-1-2*j)*(i%2)]
        // 필요한 연산 수행
```