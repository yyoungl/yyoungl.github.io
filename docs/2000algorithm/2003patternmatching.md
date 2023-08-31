---
layout: default
title: 패턴 매칭 - 브루트 포스, 보이어 무어
nav_order: 2003
parent: Algorithm
---

# 패턴 매칭

---

## 패턴 매칭에 사용되는 알고리즘들

- 고지식한 패턴 검색 알고리즘 ex) 브루트 포스
- 카프-라빈 알고리즘
- KMP 알고리즘
- 보이어-무어 알고리즘

## 고지식한 알고리즘 (Brute-Force)

- 본문 문자열을 처음부터 끝까지 차례대로 순회하면서 패턴 내의 문자들을 일일이 비교하는 방식으로 동작

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F73tSi%2FbtssIpw9EVS%2FCdl8Q8rF3moQKbMdBgWSO0%2Fimg.png)

### 알고리즘 설명

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJyJop%2FbtssHDvvqeN%2F48MUPcXzETSSKfdNgUJFKk%2Fimg.png)

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcE1mPW%2FbtssDRgTDvu%2FInTEMHEhk3rgy07uKuzvc1%2Fimg.png)

### 고지식한 패턴 검색 알고리즘

```
// p[] : 찾을 패턴 -iss
// t[] : 전체 텍스트 - This iss a book
// M : 찾을 패턴의 길이
// N : 전체 텍스트의 길이
// i : t의 인덱스
// j : p의 인덱스

BruteForce(char[] p, char[] t) {
    i = 0, j = 0
    while(j<M and i<N) {
        if (t[i] != p[j])
            i = i-j;
            j=-1;
        i = i+1, i=j+1
    }
    if (j==M) return i-M;
    else return -1;
}
```

### 고지식한 패턴 알고리즘의 시간 복잡도

- 최악의 경우 시간 복잡도는 텍스트의 모든 위치에서 패턴을 비교해야 하므로 O(MN)이 됨
- 예시에서는 최악의 경우 약 10,000\*80 = 800,000 번의 비교가 일어난다
- 비교 횟수를 줄일 수 있는 방법은 없는가?

## 보이어 무어 알고리즘

- 오른쪽에서 왼쪽으로 비교
- 대부분의 상용 소프트웨어에서 채택하고 있는 알고리즘
- 보이어-무어 알고리즘은 패턴의 오른쪽 끝에 있는 문자가 불일치하고 이 문자가 패턴 내에 존재하기 않는 경우, 이동 거리는 무려 패턴의 길이만큼이 된다

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAylMi%2FbtssBmuWEGm%2FHzuoHy4hkppfFusuuHlNMk%2Fimg.png)

**오른쪽 끝에 있는 문자가 불일치 하고 이 문자가 패턴 내에 존재할 경우**

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMdS3L%2Fbtssvgh6ecW%2FOrTApSW37fGva8qlHsKU7K%2Fimg.png)

### 보이어-무어 알고리즘 예

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6fEpG%2FbtssvXWURsY%2F1w9nvxsVuNDhYS8eOJ9xQ1%2Fimg.png)
