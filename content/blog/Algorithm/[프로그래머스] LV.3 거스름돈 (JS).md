---
title: '[프로그래머스] LV.3 거스름돈 (JS)'
date: 2022-12-21 19:12:07
category: algorithm
thumbnail: { thumbnailSrc }
draft: false
---

[문제출처](https://school.programmers.co.kr/learn/courses/30/lessons/12907)

## 정답 코드

```js
function solution(n, money) {
  const DIVISOR = 1000000007

  const dp = new Array(n + 1).fill(0)
  dp[0] = 1
  money.forEach(el => {
    for (let i = el; i < n + 1; i++) {
      dp[i] += dp[i - el]
    }
  })

  return dp[n] % DIVISOR
}
```

## 해결방법

[참고 블로그 글](https://taesung1993.tistory.com/74)

LV.3 중에서도 난이도가 꽤 높은 문제였다.  
여러가지 블로그 풀이를 참고했지만 위 링크글이 가장 깔끔하게 설명해주어서 첨부했다.

해당 문제는 **DP문제**이다.  
해결 방법을 떠올리는 것은 어렵지만 실제 코드는 생각보다 간단하다.

dp배열은 `n + 1`크기로 생성해준다.  
money가 가지고 있는 화폐 크기별로 전체 순환을 한다.

> dp[i] += dp[i - el]

위 점화식이 나오게된 배경을 이해하는데에 어려움이 있었다.

간단하게 설명하자면, 알고리즘은 2중 순환구조를 가지게되는데, 2번째 순환은 최소 한개의 `el`을 가지는 순번 이후부터 탐색을 한다.(i가 el부터 시작하는 이유)

사실 문제에 대해서 이해를 하기 위해서는 시각자료가 꼭 필요할 것 같다.  
그래서 위 링크의 블로그를 참고하는게 이해를 위한 가장 쉬운 방법이다.

DP를 가지고도 이렇게 복잡한 구조의 생각을 필요로하는 문제가 있다는 것을 알았고
사고의 확장을 경험한 문제였다.

### 프로그래머스

| 순위  | 점수    | 해결한 문제 |
| ----- | ------- | ----------- |
| 528위 | 1,626점 | 243개       |
