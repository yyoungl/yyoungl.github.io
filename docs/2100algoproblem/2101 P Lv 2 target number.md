---
layout: default
title: 프로그래머스2 타겟 넘버 Java
nav_order: 2101
description:
parent: Algorithm Problems
---

# (Lv.2) 타겟 넘버

생성일: 2023년 6월 28일 오후 3:51

# 문제 [🌐](https://school.programmers.co.kr/learn/courses/30/lessons/43165)

n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

```python
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```

사용할 수 있는 숫자가 담긴 배열 `numbers`, 타겟 넘버 `target`이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return하도록 solution 함수를 작성해주세요.

### 제한사항

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

### 입출력 예

| numbers         | target | return |
| --------------- | ------ | ------ |
| [1, 1, 1, 1, 1] | 3      | 5      |
| [4, 1, 2, 1]    | 4      | 2      |

## 접근 방법

문제를 풀 수 있는 방법은 너비 우선 탐색 (BFS) 과 깊이 우선 탐색 (DFS) 이 있다. BFS는 숫자를 더하거나 뺀 경우의 수를 단계마다 하나씩 다 구해보는 것이고, DFS는 한 가지 경우를 탐색하고, 결과값을 얻은 다음 다른 경우로 넘어가는 방식이다. 일단 BFS만 올려야징~

### BFS 깊이 우선 탐색

두 번째 예시로 살펴보자!

```python
# numbers = [4, 1, 2, 1]
# target = 4

answer = 0 # target number를 만들 수 있는 경우의 수
result = [0] # 계산 결과를 담을 리스트
```

```python
# numbers = [4, 1, 2, 1]
# target = 4

    for num in numbers:
        temp = []
        for i in result:
            temp.append(i+num)
            temp.append(i-num)
        result = temp
```

- numbers에 들어있는 숫자 num에 대해 반복, 결과값을 보관할 temp 선언

1. 첫 번째 숫자 4에 대해 반복문
   - result에 있는 0에 4를 더하고, 뺀 후 temp에 append한다.
   - temp = [4, -4]
   - result = temp = [4, -4] 가 됨
2. 두 번째 숫자 1에 대해서 다시 반복문
   - result = [4, -4] 이므로 temp에는 4+1 = 5, 4-1 = 3 append되고
   - -4에 대해 -4+1 = -3, -4-1 = -5
   - result = temp = [5, 3 ,-3, -5]
3. 세 번째 숫자 2에 대해 반복
   - result = [5, 3, -3, 5]
   - result = temp = [7, 3, 5, 1, -1, -5, -3, -7]
4. 네 번째 숫자 1에 대해 반복
   - result = [8, 6, 4, 2, 6, 4, 2, 0, 0, -2, -4, -6, -2, -4, -6, -8]

```python
    for x in result:
        if x == target:
            answer+=1
```

result 배열에 target이 몇 개 있는지 확인 → return

## Full Solution

```python
#BFS
def solution(numbers, target):
    answer = 0
    result = [0]
    for num in numbers:
        temp = []
        for i in result:
            temp.append(i+num)
            temp.append(i-num)
        result = temp
    for x in result:
        if x == target:
            answer+=1

    return answer
```
