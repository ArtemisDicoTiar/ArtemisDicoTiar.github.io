---

title: Programmers Scala Study (level 1.15)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 15. 문자열 다루기 기본

## 문제 설명

주어진 문자열이 숫자로만 구성되어 있는지 확인해라.

## Inputs

| Variable Name | type   | meaning                                    |
| ------------- | ------ | ------------------------------------------ |
| s             | String | string combination of number and character |

## output

~~~scala
return Boolean // is number or not?
~~~

## Conditions

* s length is 1~8, [4 or 6]

## Test cases

| s      | return |
| ------ | ------ |
| "a234" | false  |
| "1234" | true   |

## Solution

forall로 s에 isDigit적용하면 끝? 끝인줄 알았더니 조건으로 길이를 확인해야한다.

~~~scala
def solution(s: String): Boolean = {
  if (s.length != 4 && s.length != 6) return false
  return s.forall(_.isDigit)
}
~~~



## Study from Implementation

* 문자열 숫자인지 확인 함수: "문자열".isDigit
* Iterable전체 적용: <iterable>.forall(함수)
