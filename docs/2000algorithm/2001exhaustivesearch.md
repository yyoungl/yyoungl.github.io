---
layout: default
title: 완전 검색 Exhaustive Search
nav_order: 2001
description: 완전 검색 알고리즘
parent: Algorithm
---


# 완전 검색 Exhaustive Search

---

## Baby-gin Game

## 설명

-   0~9 사이의 숫자 카드에서 임의의 카드 6장을 뽑았을 때, 카드가 연속적인 번호를 갖는 경우는 run이라 하고, 3장의 카드가 동일한 번호를 갖는 경우를 triplet이라 한다.
-   그리고, 6장의 카드가 run과 triplet으로만 구성된 경우를 baby-gin으로 부른다
-   6자리의 숫자를 입력받아 baby-gin의 여부를 판단하는 프로그램을 작성하라

### 입력 예

-   667767은 두 개의 triplet이므로 baby-gin이다 (666, 777)
-   054060은 한 개의 run과 한 개의 triplet이므로 역시 baby-gin이다 (456, 000)
-   101123은 한 개의 triplet이 존재하나, 023이 run이 아니므로 baby-gin이 아니다.
-   (123을 run으로 사용하더라도 011이 run이나 triplet이 아님)

### 6자리의 숫자를 입력받아 어떻게 baby-gin 여부를 찾을 것인가?

### 완전 검색!!

-   완전 검색 방법은 문제의 해법으로 생각할 수 있는 모든 경우의 수를 나열해 보고 확인하는 기법이다
-   Brute-force 혹은 Generate-and-Test 기법이라고도 불리운다
-   모든 경우의 수를 테스트한 후, 최종 해법을 도출한다.
-   일반적으로 경우의 수가 상대적으로 작을 때 유용하다

### 완전 검색으로 시작하라

-   모든 경우의 수를 생성하고 테스트하기 때문에 수행 속도는 느리지만, 해답을 찾아내지 못할 확률이 적다
-   자격검정평가 등에서 주어진 문제를 풀 때, **우선 완전 검색으로 접근**하여 해답을 도출한 후, 성능 개선을 위해 다른 알고리즘을 사용하고 해답을 확인하는 것이 바람직하다

### 완전 검색을 활용한 Baby-gin 접근

-   6개의 숫자로 만들 수 있는 모든 숫자 나열 (중복 포함)
    
-   ex) 입력으로 \[2, 3, 5, 7, 7, 7\]을 받았을 경우, 아래와 같이 순열을 생성할 수 있다


### 해답 테스트하기

-   앞의 3자리와 뒤의 3자리를 잘라, run와 triplet 여부를 테스트하고 최종적으로 baby-gin을 판단한다
    
-   ex)


## 순열을 어떻게 생성할 것인가

### 순열 (Permutation)

-   서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것
-   서로 다른 n개 중 r개를 택하는 순열은 $nPr$
-   그리고 $nPr$ 은 다음과 같은 식이 성립한다
-   $nPr = n_(n-1)_(n-2)_..._(n-r+1)$
-   $nPn = n!$ 이라고 표기하며 Factorial 이라 부른다.
-   $n!=n_(n-1)_(n-2)_..._2\*1$

### ex) {1, 2, 3}을 포함하는 모든 순열을 생성하는 함수

-   동일한 숫자가 포함되지 않았을 때, 각 자리수 별로 loop을 이용해 아래와 같이 구현할 수 있다.
-   `for i1 from 1 to 3 { for i2 from 1 to 3 { if i2 != i1 { for i3 from 1 to 3 { if i3 != i1 and i3 != i2 { print (i1, i2, i3) } } } } }`