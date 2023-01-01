---
title: '[프로그래머스] LV.2 테이블 해시 함수 (JS)'
date: 2023-01-01 20:45:50
category: algorithm
thumbnail: { thumbnailSrc }
draft: false
---

[문제출처](https://school.programmers.co.kr/learn/courses/30/lessons/147354)

## 정답 코드

```js
function solution(data, col, row_begin, row_end) {
  data.sort((a, b) => {
    if (a[col - 1] === b[col - 1]) return b[0] - a[0]
    return a[col - 1] - b[col - 1]
  })

  const S_Arr = new Array(data.length).fill(0).map((_, idx) => {
    return data[idx].reduce((a, c) => a + (c % (idx + 1)), 0)
  })

  const result = S_Arr.slice(row_begin - 1, row_end).reduce((a, c) => a ^ c)

  return result
}
```

## 해결방법

복잡해 보이는 문제이지만 예시와 문제를 잘 읽으면 쉽게 해결할 수 있다.  
`sort()` 내부함수에서 조건을 따져서 sorting을 수행했다.

또한 `reduce()` 함수를 잘 활용해서 문제의 정답을 계산하였다.

> js에서 bitwise XOR의 연산자는 `^`임을 기억하자.

### 프로그래머스

| 순위  | 점수    | 해결한 문제 |
| ----- | ------- | ----------- |
| 549위 | 1,627점 | 244개       |
