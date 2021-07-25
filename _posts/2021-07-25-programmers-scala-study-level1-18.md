---

title: Programmers Scala Study (level 1.18)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 18. 문자열을 정수로 바꾸기

## 문제 설명

문자열 숫자를 숫자로 변환

## Inputs

| Variable Name | type   | meaning          |
| ------------- | ------ | ---------------- |
| s             | String | String of number |

## output

~~~scala
return Int // converted number
~~~

## Conditions

* s
  * length: 1~5
  * there can be sign at the beginning
  * does not start with '0' (ZERO)

## Test cases

| s       | return |
| ------- | ------ |
| "1234"  | 1234   |
| "-1234" | -1234  |

## Solution

이런 기능을 하는 함수가 분명 있을 텐데 (atoi, itoa처럼) 그거 그냥 쓰면 되는 거 아닌가? 맞다~

그냥 .toInt하면 끝이다.

~~~scala
def solution(s: String): Int = {
  return s.toInt
}
~~~

## Study from Implementation

* string of integer to integer
  * .toInt
