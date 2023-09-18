---
layout: default
title: 자료구조 Array(1) - 알고리즘, 배열, 버블 정렬
nav_order: 801
description:
parent: 자료구조
---

# 230807 Array (1)

- 알고리즘
- 배열
- 정렬
- 버블 정렬 (Bubble Sort)

# 알고리즘

---

- (명) 알고리즘: 유한한 단계를 통해 문제를 해결하기 위한 절차나 방법이다. 주로 컴퓨터 용어로 쓰이며, 컴퓨터가 어떤 일을 수행하기 위한 단계적 방법을 말한다.
- 간단하게 다시 말하면 어떠한 문제를 해결하기 위한 절차라고 볼 수 있다.
- ex) 1부터 100까지 합을 구하는 문제
- 컴퓨터 분야에서 알고리즘을 표현하는 방법은 크게 두 가지
  - 의사코드와 순서도

![Array1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFIZkf%2FbtsrwAhaGap%2FzbT2JiCbMKxdcqO2bMndik%2Fimg.png)

- **무엇이 좋은 알고리즘인가?**
  1.  정확성: 얼마나 정확하게 동작하는가
  2.  작업량: 얼마나 적은 연산으로 원하는 결과를 얻어내는가
  3.  메모리 사용량: 얼마나 적은 메모리를 사용하는가
  4.  단순성: 얼마나 단순한가
  5.  최적성: 더 이상 개선할 여지 없이 최적화되었는가
- 주어진 문제를 해결하기 위해 여러 개의 다양한 알고리즘이 가능
- ⇒ 어떤 알고리즘을 사용해야 하는가?
- 알고리즘의 성능 분석 필요
  - 많은 문제에서 성능 분석의 기준으로 알고리즘의 작업량을 비교한다
- ex) 1부터 100까지 합을 구하는 문제
- 알고리즘의 작업량을 표현할 때 시간복잡도로 표현한다.
- 시간 복잡도 (Time Complexity)
  - 실제 걸리는 시간을 측정
  - 실행되는 명령문의 개수(N)를 계산
  - ****\*\*\*\*****\*\*\*\*\*****\*\*\*\*****알고리즘 1******\*\*******\*\*******\*\*******
  - `CalcSum(n) { sum = 0; // 1번 for ( i=1; i<=n; i++) //1+1번 sum+=1; // 1번 return sum; }`
  - ****\*\*****\*\*\*****\*\*****알고리즘 2****\*\*****\*\*\*\*****\*\*****3번의 연산
  - 1 + n\* 3 = 3n+1 의 연산
  - `Calcsum(n) { return n*(n+1)/2 // 3번 }`

### 시간 복잡도 빅-오(O) 표기법

- 빅-오 표기법 (Big-Oh Notation)
- 시간 복잡도 함수 중에서 가장 큰 영향력을 주는 n에 대한 항만을 표시
- 계수(Coefficient)는 생략하여 표시

ex)

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTi8Pu%2FbtsrsTBImed%2FLHizkzYkhJHkZads0Ldxi1%2Fimg.png)

- n개의 데이터를 입력받아 저장한 후 각 데이터에 1씩 증가싴니 후 데이터를 화면에 출력하는 알고리즘의 시간 복잡도는 어떻게 되나? **O(n)**

## 다양한 시간 복잡도의 비교

### 요소 수가 증가함에 따라 각기 다른 시간복잡도의 알고리즘은 아래와 같은 연산 수를 보인다

![Array3](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc59IG8%2Fbtsrype6Xgm%2F3Q125DYVgaZ4siy5vIrty0%2Fimg.png)

![Array4](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFuJ9O%2FbtsrB0eL0cc%2FbXzKkmM4Mwki4i0wyBj9aK%2Fimg.png)

### 시간 복잡도별 실행 시간 비교

![Array5](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5rNAh%2Fbtsrtd01CkB%2Fy9vDnIhx4IeiRezeN93Ns0%2Fimg.png)

# 배열

---

## 배열이란 무엇인가

- 일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조
- 아래의 예는 6가지 변수를 사용해야 하는 경우, 이를 배열로 바꾸어 사용하는 것이다

![Array6](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FemEUeL%2FbtsrAQp84tt%2FWTS0JANolbcuRBKYscn1E0%2Fimg.png)

### 배열의 필요성

- 프로그램 내에서 여러 개의 변수가 필요할 때, 일일이 다른 변수명을 이용하여 자료에 접근하는 것은 매우 비효율적일 수 있다.
- 배열을 사용하면 하나의 선언을 통해서 둘 이상의 변수를 선언할 수 있다.
- 단순히 다수의 변수 선언을 의미하는 것이 아니라, 다수의 변수로는 하기 힘든 작업을 배열을 활용해 쉽게 할 수 있다.

## 1차원 배열

### 1차원 배열의 선언

- 자료형: 배열을 이루는 자료형
- 이름: 프로그램에서 사용할 배열의 이름
- 길이: 배열을 이루는 원소의 수

![Array7](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdkE7zW%2FbtsrwXpMq9x%2FkZQX6wfvaDtKhqVpagSuEK%2Fimg.png)

### 1차원 배열의 접근

```
nums[0] = 10; // 배열 nums의 0번째 원소에 10을 저장
nums[idx] = 20; // 배열 nums의 idx에 원소에 20을 저장
```

자바에서는 음수 인덱스는 안 돼! → 요소를 제외하는 것을 의미

크기를 벗어나서도 안 돼!

마지막 인덱스를 가져오고 싶으면, nums\[nums.length()-1\]

### 1차원 배열의 순회

- 배열의 요소를 빠짐없이 조사하는 방법
- `for ( ; ; ) { }`

## SW 문제를 완벽하게 풀기 위한 5단계

1.  지문을 읽는다
2.  문제를 이해한다
3.  문제를 손으로 푼다
4.  푼 걸 코딩한다
5.  디버깅하고 검증한다

# 정렬

---

- 2개 이상의 자료를 특정 기준에 의해 작은 값부터 큰 값 (오름차순: ascending), 혹은 그 반대의 순서대로 (내림차순: descending) 재배열하는 것

### 키

- 자료를 정렬하는 기준이 되는 특정 값

![Array8](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcx1c4p%2Fbtsrxn2Ryls%2Fca1dZUfzYa5BRGKZhVVQUk%2Fimg.png)

## 대표적인 정렬 방식의 종류

- 버블 정렬 (Bubble Sort)
- 선택 정렬 (Selection Sort)
- 삽입 정렬 (Insertion Sort)
- 카운팅 정렬 (Counting Sort)
- 병합 정렬 (Merge Sort)
- 퀵 정렬 (Quick Sort)

### APS 과정을 통해 자료구조와 알고리즘을 학습하면서 다양한 형태의 정렬을 학습하게 된다

# 버블 정렬 (Bubble Sort)

---

### 인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식

### 정렬 과정

- 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동한다
- 한 단계가 끝나면 가장 큰 원소가 마지막 자리로 정렬된다
- 교환하며 자리를 이동하는 모습이 물 위에 올라오는 거품 모양과 같다고 하여 버블 정렬이라고 한다

### 시간 복잡도

- O(n^2)

### 버블 정렬 과정

![Array9](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fr0bQj%2FbtsrBoAdL8D%2F7JR08hdNTYBSxB0KrIMG4K%2Fimg.png)

![Array10](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbg5iCr%2FbtsrCRPbxHE%2FTdBAZGZaCSKx6WNDXYqLGK%2Fimg.png)

![Array11](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAX03n%2FbtsrtdUjx8Q%2FNnfp8vn3af2gSL2qg4I1U1%2Fimg.png)

정렬 끝

![Array12](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrtEpA%2FbtsrB33A0vE%2FCD8EhP9pnwqKXiBLXOR5yk%2Fimg.png)

## 배열을 활용한 버블 정렬

```
BubbleSort(int[] a, int N) { // a[] : 정렬할 배열, N: 배열의 크기
    for i from N-1 to 0 decreasing by 1 {
        for j from 0 to i {
            if (a[j] > a[j+1]) then {
                temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
            }
        }
    }
}
```
