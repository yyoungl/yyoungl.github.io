---
layout: default
title: 자료구조 Array(2) - 검색, 선택 정렬, 카운팅 정렬
nav_order: 502
description:
parent: 자료구조
---

# 230808 Array (2)

생성 일시: 2023년 8월 7일 오후 4:36

- 검색(Search)
- 선택 정렬(Selection Sort)
- 카운팅 정렬

# 검색 Search

---

### 저장되어 있는 자료 중에서 원하는 항목을 찾는 작업

### 목적하는 탐색 키를 가진 항목을 찾는 것

- 탐색 키(search key): 자료를 구별하여 인식할 수 있는 키

## 검색의 종류

- 순차 검색 (sequential search)
- 이진 검색 (binary search)
- 인덱싱 (indexing)

# 순차 검색 Sequential Search

---

### 일렬로 되어 있는 자료를 순서대로 검색하는 방법

- 가장 간단하고 직관적인 검색 방법
- 배열이나 연결 리스트 등 순차구조로 구현된 자료구조에서 원하는 항목을 찾을 때 유용함
- 알고리즘이 단순하여 구현이 쉽지만, 검색 대상의 수가 많은 경우에는 수행 시간이 급격히 증가하여 비효율적

### 2가지 경우

- 정렬되어 있지 않은 경우
- 정렬되어 있는 경우

## 정렬되어 있지 않은 경우

---

### 검색 과정

- 첫 번째 원소부터 순서대로 검색 대상과 키 값이 같은 원소가 있는지 비교하며 찾는다
- 키값이 동일한 원소를 찾으면 그 원소의 인덱스를 반환한다
- 자료구조의 마지막에 이를 때까지 검색 대상을 찾지 못하면 검색 실패

### ex) 2를 검색하는 경우

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcghado%2Fbtsr5Y8iGWG%2Fk4IPPBa20ppLt6CHZPPUMK%2Fimg.png)

### ex) 8을 검색하는 경우

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2K6K5%2Fbtsr5dEDJcr%2FiAO2IZAPSjKhUP7HBFLI10%2Fimg.png)

### 찾고자 하는 원소의 순서에 따라 비교 회수가 결정됨

- 첫 번째 원소를 찾을 때는 1번 비교, 두 번째 원소를 찾을 때는 2번 비교…
- 정렬되지 않은 자료에서의 순차 검색의 평균 비교 회수
    
    $= (1/n)*(1+2+3+...+n) = (n+1)/2$
    
- 시간 복잡도 O(n)

### 구현 예

```java
// a: 1차원 배열, n: 배열 크기, key: 찾고 싶은 값
sequentialSearch(int[] a, int n, int key) 
	i = 0
	while (i<n and a[i] != key)
		i+=1;
	if (i<n) return i;
	else return -1;
```

찾는 값이 존재하는 인덱스 반환

→ 만약 중복된 값이 존재한다면 개수를 세거나 인덱스들을 보관해야 함. `return` 하지 않고 나머지 인덱스도 탐색

## 정렬되어 있는 경우

---

## 검색 과정

- 자료가 오름차순으로 정렬된 상태에서 검색을 실시한다고 가정하자.
- 자료를 순차적으로 검색하면서 키 값을 비교하여 원소의 키 값이 검색 대상의 키 값보다 크면 찾는 원소가 없다는 것이므로 더 이상 검색하지 않고 검색을 종료한다

### 예) 11을 검색하는 경우

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdbqDwJ%2Fbtsr0X3m5IO%2F5EM6imMo1jI8Mfrbt2Vr51%2Fimg.png)

### 예) 10을 검색하는 경우

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvMaIO%2Fbtsr5gnQ1DH%2FYFrFhTX6T4h1OzwmulP041%2Fimg.png)

### 찾고자 하는 원소의 순서에 따라 비교 회수가 결정됨

- 정렬이 되어 있으므로 검색 실패를 반환하는 경우 평균 비교 회수가 반으로 줄어든다
- 시간 복잡도: O(n)
    
    → 평균적으로는 정렬되어 있는 경우, 정렬되어 있지 않은 경우 똑같다 (뭘 찾으려고 할지 모르기 때문에)
    

### 구현 예

```java
// a: 1차원 배열, n: 배열 크기, key: 찾고 싶은 값
sequentialSearch2(int[] a, int n, int key) 
	i = 0
	while (a[i]<key)
		i += 1;
	if (a[i]==key) return i;
	else return -1;
```

# 이진 검색 Binary Search

---

**자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법**

- 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여 가면서 보다 빠르게 검색을 수행함

**이진 검색을 하기 위해서는 자료가 정렬된 상태여야 한다.**

### 검색 과정

1. 자료의 중앙에 있는 원소를 고른다
2. 중앙 원소의 값과 찾고자 하는 목표 값을 비교한다
3. 목표 값이 중앙 원소의 값보다 작으면 자료의 왼쪽 반에 대해서 새로 검색을 수행하고, 크다면 자료의 오른쪽 반에 대해서 새로 검색을 수행한다
4. 찾고자 하는 값을 찾을 때까지 1~3의 과정을 반복한다

**예) 이진 검색으로 7을 찾는 경우**

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwjzIT%2Fbtsr65TDMFR%2FE9sktfW3KHn6e9DZpGNP0K%2Fimg.png)

**예) 이진 검색으로 20을 찾는 경우**

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTeaNE%2FbtsrVuBdVzk%2FuSNkP1B0zbDlB68837Kp61%2Fimg.png)

## 구현

- 검색 범위의 시작점과 종료점을 이용하여 검색을 반복 수행한다
- 이진 검색의 경우, 자료의 삽입이나 삭제가 발생했을 때 배열의 상태를 항상 정렬 상태로 유지하는 추가 작업이 필요하다
    
    ```java
    binarySearch(int[] a, int key)
     start = 0;
    	end = a.length - 1;
    	while (start <= end) {
    		middle = (start + end)/2;
    		if (a[middle] == key) return true; // 검색 성공
    		else if (a[middle] > key) end = middle - 1; // 왼쪽
    		else start = middle + 1; // 오른쪽
    	}
    return false; // 검색 실패
    ```
    

### 재귀 함수 이용

- 아래와 같이 재귀 함수를 이용하여 이진 검색을 구현할 수도 있다
- 재귀 함수에 대해서는 나중에 더 자세히 배우도록 한다
    
    ```java
    binarySearch2(int[] a, int low, int high, int key) {
    	if (low > high) return false; // 검색 실패
    	middle = (low + high)/2;
    	if (key==a[middle]) return true; // 검색 성공
    	else if (key<a[middle]) // 왼쪽
    		return binarySearch2(a, low, middle-1, key)
    	else if (key>a[middle]) // 오른쪽
    		return binarySearch2(a, middle+1, high, key)
    ```
    

# 선택 정렬 = 셀렉션 알고리즘 Selection Sort

---

- **저장되어 있는 자료로부터 k번째로 큰 혹은 작은 원소를 찾는 방법을 셀렉션 알고리즘이라 한다**
    - 최소값, 최대값 혹은 중간 값을 찾는 알고리즘을 의미하기도 한다
- **선택 과정**
    - 셀렉션은 아래와 같은 과정을 통해 이루어진다
        - 정렬 알고리즘을 이용하여 자료 정렬하기
        - 원하는 순서에 있는 원소 가져오기
- **아래는 k번째로 작은 원소를 찾는 알고리즘**
    - 1번부터 k번까지 작은 원소들을 찾아 배열의 앞쪽으로 이동시키고, 배열의 k번째를 반환한다
    - k가 비교적 작을 때 유용하며 O(kn)의 수행시간을 필요로 한다
        
        ```java
        Select (int[] nums, int k) {
        	for i from 1 to k {
        		minIndex = i;
        		 for j from i+1 to n {
        			if nums[minIndex] > nums[j] {
        				minIndex = j;
        			}
        		}
        		swap(nums[i], nums[minIndex]);
        		// java에서 swap 사용: swap(nums, index1, index2);
        	}
        	return nums[k];
        }
        ```
        

### 포켓볼 순서대로 정렬하기

- 왼쪽과 같이 흩어진 당구공을 오른쪽 그림처럼 정리한다고 하자. 어떻게 하겠는가?
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxKhfk%2FbtsrTRXJGNd%2Fk6kDg3F5ZxkBeUS0DARny1%2Fimg.png)
    
- 많은 사람들은 당구대 위에 있는 공 중 가장 작은 숫자의 공부터 골라서 차례대로 정리할 것이다. 이것이 바로 선택 정렬이다.
- **주어진 자료등 줄 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식**
    - 앞서 살펴본 셀렉션 알고리즘을 전체 자료에 적용한 것이다

### 정렬 과정

- 주어진 리스트 중에서 최소값을 찾는다
- 그 값을 리스트의 맨 앞에 위치한 값과 교환한다
- 맨 처음 위치를 제외한 나머지 리스트를 대상으로 위의 과정을 반복한다

### 시간 복잡도

- O(n^2)
1. 주어진 리스트에서 최소값을 찾는다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FK0KTr%2Fbtsr5K3f6xL%2F8CHxhwHt6eMWxr00TgtKfK%2Fimg.png)
    
2. 리스트의 맨 앞에 위치한 값과 교환한다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcvzeis%2FbtsrYLJrDkA%2F5qva6qJktivN16qpDSxSSK%2Fimg.png)
    
3. 미정렬 리스트에서 최소값을 찾는다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeT5TKW%2FbtsrYNtICr0%2FgHs0KY6iuYNw7g6ktmbYR1%2Fimg.png)
    
4. 리스트의 맨 앞에 위치한 값과 교환한다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBBWT5%2Fbtsr4mhxp8N%2FP6PK4nlxw8lZ4dksPzngo0%2Fimg.png)
    
5. 미정렬 리스트에서 최소값을 찾는다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcGP6zV%2FbtsrYAA6TI7%2FyehhkEbyyCBhQfr8TK3vT0%2Fimg.png)
    
6. 리스트의 맨 앞에 위치한 값과 교환한다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbXbVCx%2FbtsrUnB4JjB%2FrPKDGoC4oUp8aATYkiwTL1%2Fimg.png)
    
7. 미정렬 리스트에서 최소값을 찾는다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAgwol%2Fbtsr5ZsAOnl%2FbEu6X8Hc8qfzZGASknznk0%2Fimg.png)
    
8. 리스트의 맨 앞에 위치한 값과 교환한다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb5LJW4%2Fbtsr5fPZrK6%2Ftl7WASkebrh4rnXpf0Yixk%2Fimg.png)
    
- 미정렬 원소가 하나 남은 상황에서는 마지막 원소가 가장 큰 값을 갖게 되므로, 실행을 종료하고 선택 정렬이 완료된다

## 알고리즘

```java
SelectionSort(int[] nums, int N) {
	for i from 0 to n-1 {
		a[i], ..., a[n-1] 원소 중 최소값 a[k] 찾음
		a[i]와 a[k] 교환
	}
}
```

```java
SelectionSort(int[] nums, int N) { // nums : 정렬할 배열, N: 배열 크기
	for i from 0 to N-1 {
		minIdx = i;
		for j from i+1 to N {
			if (nums[minIdx] > nums[j]) {
				minIdx = j;
			}
		}
		swap(nums[i], nums[minIdx]);
	}
}
```

# 카운팅 정렬 Counting Sort

---

- **항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘**
- 제한사항
    - 정수나 정수로 표현할 수 있는 자료에 대해서만 적용 가능
    - 각 항목의 발생 회수를 기록하기 위해, 정수 항목으로 인덱스 되는 카운트들의 배열을 사용하기 때문이다
    - 카운트들을 위한 충분한 공간을 할당하려면 집합 내의 갖아 큰 정수를 알아야 한다
- 시간 복잡도
    
    O(n+k): n은 배열의 길이, k는 정수의 최대값
    
- 발생 빈도의 누적합 n번 이하 등장하는 것들이 몇 개인지. → 내가 어디부터 들어가야 하나? 를 판단
    
    이를 바탕으로 정렬한다. 중복으로 발생하는 숫자를 포함해서 오름차순 정렬
    

### 정렬 과정

`[0, 4, 1, 3, 1, 2, 4, 1]` →  `[0, 1, 1, 1, 2, 3, 4, 4]`

**1단계**

- Data에서 각 항목들의 발생 회수를 세고, 정수 항목들로 직접 인덱스 되는 카운트 배열 counts에 저장한다

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FerdHzV%2FbtsrTOzXb2E%2FdBJHq1GpRL7W226khMWK11%2Fimg.png)

**2단계** 누적합 구하기

**3단계** 정렬하기

- `counts[1]`을 감소시키고 Temp에 1을 삽입한다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmOA3e%2FbtsrYz90RzW%2FfiIYL5kcCWDFk79qWKYw8k%2Fimg.png)
    
- `counts[4]`를 감소시키고 Temp에 4를 삽입한다
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdkpeKw%2FbtsrTRckkwY%2FxaqGlXBTfbFGBophrByyN1%2Fimg.png)
    
- `counts[2]`를 감소시키고 Temp에 2를 삽입한다.
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F2SRRd%2FbtsrYAunz9m%2FobnmS67zhxslrGmMlmUUqk%2Fimg.png)
    
- `counts[1]`을 감소시키고 Temp에 1을 삽입한다.
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Foonb0%2FbtsrZwZjnNG%2FfkMRvYhQK37VbFJKs7poW1%2Fimg.png)
    
- `counts[3]`을 감소시키고 Temp에 3을 삽입한다.
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSZ2EH%2Fbtsr657aUDz%2FTHQtyvp0pS1cDPzz1AB3AK%2Fimg.png)
    
- `counts[1]`을 감소시키고 Temp에 1을 삽입한다.
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC9S9R%2Fbtsr5MfIUnt%2FNbbhki2JYsEwqrkAViW2uk%2Fimg.png)
    
- `counts[4]`를 감소시키고 Temp에 4를 삽입한다.
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbRNyaA%2FbtsrTsjkOpW%2FYFXaoVdsDy5kfAczCFKSBk%2Fimg.png)
    
- `counts[0]`을 감소시키고 Temp에 0을 삽입한다.
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FciWvr1%2FbtsrUuunPSm%2F2KhSDO1rH5qaTA6HZQWBak%2Fimg.png)
    
- Temp 업데이트 완료하고 정렬 작업을 종료한다.

```java
Counting_Sort(A, B, k)
// A[] 입력 배열
// B[] 정렬된 배열
// C[] 카운트 배열
// k 최대값, n: 입력 배열 길이

C = new int[k];

for i from 0 to n
	C[A[i]] += 1; // 개수 세기

for i from 1 to k
	C[i] += C[i-1] // 누적합

for i from n-1 to 0
	B[C[A[i]]-1] = A[i]
	C[A[i]] -= 1
```

### 카운팅 정렬을 항상 사용하는 게 좋은가?

- `{1, 2, 10억, 1}`을 정렬하고자 할 때 메모리 낭비가 발생

### 카운팅 정렬은 안정정렬이라고 하는데 무슨 뜻인가?

- **같은 값을 가지는 복수의 원소들이 정렬 후에도 정렬 전과 같은 순서를 가진다**
    
![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdZRnnP%2FbtsrTrdEtrL%2FXsV7OpwtKczoHLt8dKNnk0%2Fimg.png)
    

### 복수의 원소를 카운팅 정렬

**두 번째 기준 정렬**

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbeSmVL%2FbtsrUrLcvW8%2FK8KPM31JzVuapOcSuh5Ur1%2Fimg.png)

**첫 번째 기준 정렬**

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkyFes%2Fbtsr4JKBudi%2FqfV9YIFUaX9d8Nt8NHKt71%2Fimg.png)

**정렬 끝**

![Array2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FusJHg%2Fbtsr0t2yFdh%2FkkD174aV1muSuMz2PotQC1%2Fimg.png)

### 정렬 알고리즘 비교

| 알고리즘 | 평균 수행시간 | 최악 수행시간 | 알고리즘 기법 | 비고 |
| --- | --- | --- | --- | --- |
| 버블 정렬 | O(n^2) | O(n^2) | 비교와 교환 | 코딩이 가장 손쉽다 |
| 선택 정렬 | O(n^2) | O(n^2) | 비교와 교환 | 교환의 회수가 버블, 삽입 정렬보다 작다 |
| 카운팅 정렬 | O(n+k) | O(n+k) | 비교환 방식 | n이 비교적 작을 때만 가능하다 |
| 삽입 정렬 | O(n^2) | O(n^2) | 비교와 교환 | n의 개수가 작을 때 효과적이다 |
| 병합 정렬 | O(nlogn) | O(nlogn) | 분할 정복 | 연결 리스트의 경우 가장 효율적인 방식 |
| 퀵 정렬 | O(nlogn) | O(n^2) | 분할 정복 | 최악의 경우 O(n^2) 이지만, 평균적으로는 가장 빠르다 |