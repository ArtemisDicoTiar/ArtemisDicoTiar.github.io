---

title: Programmers Scala Study (level 1.31)

categories:
  - Programming Study
last_modified_at: 2021-07-26

tags: [programming, study, scala]

---

# 31. 하샤드 수

## 문제 설명

주어진 수가 하샤드 수인지 판별

하샤드 수는 주어진수가 주어진수의 각 자릿수의 합으로 나눠져야한다.

## Inputs

| Variable Name | type | meaning       |
| ------------- | ---- | ------------- |
| x             | Int  | target number |

## output

~~~scala
return Boolean // isHashad num?
~~~

## Conditions

* x
  * 1~10 000

## Test cases

| arr  | return |
| ---- | ------ |
| 10   | true   |
| 12   | true   |
| 11   | false  |
| 13   | false  |

## Solution

각 자릿수 합은 string으로 변환하고 더하면 된다.

~~~scala
def solution(x: Int): Boolean = {
  x % x.toString.map(_.asDigit).sum == 0
}
~~~

### Study from Implementation
