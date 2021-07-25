---

title: Programmers Scala Study (level 1.17)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 17. 수박수박수박수박수박수?

## 문제 설명

길이만큼 수박을 출력, 홀수가 인풋으로 들어오면 "수"로 끝내고 짝수면 "박"으로 끝내고

## Inputs

| Variable Name | type | meaning |
| ------------- | ---- | ------- |
| n             | Int  | number  |

## output

~~~scala
return String // multiple of 수박
~~~

## Conditions

* n
  * length: ~10 000

## Test cases

| n    | return     |
| ---- | ---------- |
| 3    | "수박수"   |
| 4    | "수박수박" |

## Solution

n/2한 만큼 "수박"출력, n%2가 1이면 "수"출력

~~~scala
def solution(n: Int): String = {
  return "수박" * (n/2) + "수" * (n%2)
}
~~~

## Study from Implementation

* string multiplication
  * 파이썬이랑 동일하게 "문자열" * 반복횟수 하면 반복횟수만큼 문자열이 반복된다.
* Division
  * 파이썬이랑 동일하다
  * / → 몫
  * % → 나머지
