---
layout: default
title: 프로그래머스2 광물 캐기 Java
nav_order: 2104
parent: Algorithm Problems
---

# (Lv.2) 광물 캐기

생성일: 2023년 8월 18일 오후 4:23  
레벨: 2

🌍**_[TISTORY](http://letusgrow.tistory.com)_**

# 문제 [🌐](https://school.programmers.co.kr/learn/courses/30/lessons/172927)

마인은 곡괭이로 광산에서 광석을 캐려고 합니다. 마인은 다이아몬드 곡괭이, 철 곡괭이, 돌 곡괭이를 각각 0개에서 5개까지 가지고 있으며, 곡괭이로 광물을 캘 때는 피로도가 소모됩니다. 각 곡괭이로 광물을 캘 때의 피로도는 아래 표와 같습니다.

[##_Image|kage@ciqytr/btsrBqxZI9E/MA3gykYtr5JtA92HXxKkK0/img.png|CDM|1.3|{"originWidth":466,"originHeight":232,"style":"alignCenter"}_##]

예를 들어, 철 곡괭이는 다이아몬드를 캘 때 피로도 5가 소모되며, 철과 돌을 캘 때는 피로도가 1씩 소모됩니다. 각 곡괭이는 종류에 상관없이 광물 5개를 캔 후에는 더이상 사용할 수 없습니다.

마인은 다음과 같은 규칙을 지키면서 최소한의 피로도로 광물을 캐려고 합니다.

- 사용할 수 있는 곡괭이중 아무거나 하나를 선택해 광물을 캡니다.
- 한 번 사용하기 시작한 곡괭이는 사용할 수 없을 때까지 사용합니다.
- 광물은 주어진 순서대로만 캘 수 있습니다.
- 광산에 있는 모든 광물을 캐거나, 더 사용할 곡괭이가 없을 때까지 광물을 캡니다.

즉, 곡괭이를 하나 선택해서 광물 5개를 연속으로 캐고, 다음 곡괭이를 선택해서 광물 5개를 연속으로 캐는 과정을 반복하며, 더 사용할 곡괭이가 없거나 광산에 있는 모든 광물을 캘 때까지 과정을 반복하면 됩니다.

마인이 갖고 있는 곡괭이의 개수를 나타내는 정수 배열 `picks`와 광물들의 순서를 나타내는 문자열 배열 `minerals`가 매개변수로 주어질 때, 마인이 작업을 끝내기까지 필요한 최소한의 피로도를 return 하는 solution 함수를 완성해주세요.

### 제한사항

- `picks`는 \[dia, iron, stone\]과 같은 구조로 이루어져 있습니다.
  - 0 ≤ dia, iron, stone ≤ 5
  - dia는 다이아몬드 곡괭이의 수를 의미합니다.
  - iron은 철 곡괭이의 수를 의미합니다.
  - stone은 돌 곡괭이의 수를 의미합니다.
  - 곡괭이는 최소 1개 이상 가지고 있습니다.
- 5 ≤ `minerals`의 길이 ≤ 50
  - `minerals`는 다음 3개의 문자열로 이루어져 있으며 각각의 의미는 다음과 같습니다.
  - diamond : 다이아몬드
  - iron : 철
  - stone : 돌

### 입출력 예

| picks       | minerals                                                                                                     | result |
| ----------- | ------------------------------------------------------------------------------------------------------------ | ------ |
| \[1, 3, 2\] | \["diamond", "diamond", "diamond", "iron", "iron", "diamond", "iron", "stone"\]                              | 12     |
| \[0, 1, 1\] | \["diamond", "diamond", "diamond", "diamond", "diamond", "iron", "iron", "iron", "iron", "iron", "diamond"\] | 50     |

## 접근 방법

문제를 이해하는 것도 한참 걸렸다….

1.  광물은 무조건 순서대로 채굴해야 한다.
2.  한 곡괭이를 잡으면 광물 5개를 캐거나 더 이상 캘 광물이 없을 때까지 사용해야 한다.
3.  이를 바탕으로 **가장 적은 피로도**로 **최대한 많은 광물**을 채굴해야 한다.

결론적으로 말하면 광물을 5개씩 묶은 후 총 가치를 부여하고, 가치가 큰 것부터 좋은 곡괭이로 채굴했다.

코드가 아주 길기 때문에 하나씩 살펴봅시다!!

**캘 수 있는 광물 개수 파악**

모든 광물을 캐기에는 곡괭이가 부족하거나, 곡괭이가 남을 수도 있다. 주어진 곡괭이 개수를 활용해서 캘 수 있는 광물 배열을 다시 만들었다. (광물이 남는다면 캐지 못하기 때문)

```
int pickSum = 0;
        for (int pick : picks)
            pickSum += pick;

        // 그리고 곡괭이로 캘 수 있는 최대 광물 개수가 주어진 광물의 개수보다 더 작을 수도 있기 때문에 배열을 초기화해주기 위해 len을 초기화했습니다..
        int len;
        if (pickSum*5 < minerals.length) {
            len = pickSum*5;
        } else {
            len = minerals.length;
        }

        // 찐_최종_미네랄.java
        String[] mineralFinal = new String[len];
        for (int pick =0 ; pick <len; pick++) {
            mineralFinal[pick] = minerals[pick];
        }
```

**광물을 5개 그룹으로 묶기 & 그룹별 가치 부여**

거스름돈 문제의 원리를 사용했다. 광물은 5개고, 총 개수가 5개기 때문에 나누기 연산으로 5개의 광물 중 다이아몬드, 철, 돌의 개수를 파악할 수 있도록 각각 가치를 100, 10, 1로 부여했다.

그리고 가장 큰 가치를 가진 광물 그룹 (=돌 곡괭이로 채굴했을 때 피로도가 가장 많이 드는 그룹) 을 찾기 위해 내림차순으로 정렬했다.

++ 처음에 광물을 모두 캐지 못할 수도 있다는 것을 인지하지 못한 채 오름차순부터 했다가, 위의 배열 자르는 부분을 추가했다.

```
// 곡괭이 하나로 캘 수 있는 광물의 구간 (5씩 끊음)
        Integer[] value = new Integer[pickSum];
        Arrays.fill(value, 0);

        // 한 곡괭이로 5개를 캘 수 있고 어떤 조합이 나와도 다이아몬드, 철, 돌의 개수를 알 수 있기 때문에 거스름돈 문제와 같은 방법으로 100 / 10 / 1 의 가치를 두었고

        int i = 0;
        int idx = 0;
        while (i < len) {
            switch (mineralFinal[i]) {
            case "diamond":
                value[idx] += 100;
                break;
            case "iron":
                value[idx] += 10;
                break;
            case "stone":
                value[idx] += 1;
            }
            if (i % 5 == 4)
                idx++;
            i++;
        }
        // 가장 많은 가치 - 피로도 가 있는 광물을 가장 좋은 곡괭이로 캐내야 하기 때문에 내림차순 정렬
        // ㅠㅠ 여기서 곡괭이로 모든 광물을 캘 수 없는 경우가 발생했다는 걸 알고 처음으로 다시 돌아가 minerals 배열을 잘라 주었음
        Arrays.sort(value, Collections.reverseOrder());
```

**피로도 계산하기**

이 부분은 간단하다. 곡괭이가 다이아몬드, 철, 돌 순으로 (좋은 순서대로) 주어졌기 때문에 하나씩 살펴보면서 모두 사용할 때까지 반복문으로 광물을 캔다.

```
int index = 0;
        for (int j = 0; j < 3; j++) {
            while (picks[j] > 0) {
                // 지금 사용하는 곡괭이가 무엇인지에 따라서 피로도 누적 정도가 다름
```

picks 의 인덱스를 바탕으로 곡괭이의 종류를 파악해서 피로도를 더해 준다.

아래는 철 곡괭이를 사용한 경우이다. 100으로 나눈 값으로 다이아몬드를 파악하여 피로도에 더해 주고, 10으로 나눈 값으로 철을 파악하여 피로도 더하고, 1로 나눈 값으로 돌을 파악하여 피로도에 더해 준다.

```
                } else if (j == 1) {
                    tired += (value[index] / 100) * 5;
                    value[index] %= 100;
                    tired += value[index] / 10;
                    value[index] %= 10;
                    tired += value[index];
                    value[index] %= 1;
```

while문을 빠져나와야 하기 때문에 %1 연산을 해주고 value를 0으로 만들어 줬다.

이렇게 피로도 덧셈을 끝냈다면 곡괭이 개수를 하나 빼주면 된다.

## Full Solution

```
import java.util.Arrays;
import java.util.Collections;

class Solution {
    public int solution(int[] picks, String[] minerals) {
        int tired = 0;
        // 쓸 수 있는 전체 곡괭이의 수를 구했어요
        int pickSum = 0;
        for (int pick : picks)
            pickSum += pick;

        // 그리고 곡괭이로 캘 수 있는 최대 광물 개수가 주어진 광물의 개수보다 더 작을 수도 있기 때문에 배열을 초기화해주기 위해 len을 초기화했습니다..
        int len;
        if (pickSum*5 < minerals.length) {
            len = pickSum*5;
        } else {
            len = minerals.length;
        }

        // 찐_최종_미네랄.java
        String[] mineralFinal = new String[len];
        for (int pick =0 ; pick <len; pick++) {
            mineralFinal[pick] = minerals[pick];
        }

        // 곡괭이 하나로 캘 수 있는 광물의 구간 (5씩 끊음)
        Integer[] value = new Integer[pickSum];
        Arrays.fill(value, 0);

        // 한 곡괭이로 5개를 캘 수 있고 어떤 조합이 나와도 다이아몬드, 철, 돌의 개수를 알 수 있기 때문에 거스름돈 문제와 같은 방법으로 100 / 10 / 1 의 가치를 두었고

        int i = 0;
        int idx = 0;
        while (i < len) {
            switch (mineralFinal[i]) {
            case "diamond":
                value[idx] += 100;
                break;
            case "iron":
                value[idx] += 10;
                break;
            case "stone":
                value[idx] += 1;
            }
            if (i % 5 == 4)
                idx++;
            i++;
        }
        // 가장 많은 가치 - 피로도 가 있는 광물을 가장 좋은 곡괭이로 캐내야 하기 때문에 내림차순 정렬
        // ㅠㅠ 여기서 곡괭이로 모든 광물을 캘 수 없는 경우가 발생했다는 걸 알고 처음으로 다시 돌아가 minerals 배열을 잘라 주었음
        Arrays.sort(value, Collections.reverseOrder());

        int index = 0;
        for (int j = 0; j < 3; j++) {
            while (picks[j] > 0) {
                // 지금 사용하는 곡괭이가 무엇인지에 따라서 피로도 누적 정도가 다름
                if (j == 0) {
                    // 다이아몬드
                    tired += value[index] / 100;
                    value[index] %= 100;
                    // 철
                    tired += value[index] / 10;
                    value[index] %= 10;
                    // 돌
                    tired += value[index];
                    value[index] %= 1;

                } else if (j == 1) {
                    tired += (value[index] / 100) * 5;
                    value[index] %= 100;
                    tired += value[index] / 10;
                    value[index] %= 10;
                    tired += value[index];
                    value[index] %= 1;

                } else if (j == 2) {
                    tired += (value[index] / 100) * 25;
                    value[index] %= 100;
                    tired += (value[index] / 10) * 5;
                    value[index] %= 10;
                    tired += value[index];
                    value[index] %= 1;

                }
                // 광물을 모두 다 캔 후 사용한 곡괭이 -1
                picks[j] -= 1;

                // 광물을 다 캤다면 다음 5개를 캐러 ㄱㄱ~ 이것 때문에 마지막에 %=1 연산을 해줌
                if (value[index] == 0)
                    index++;
            }
        }
        System.out.println(tired);
}
```
