---

title: Programmers Scala Study (level 1.27)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 27. 짝수와 홀수

## 문제 설명

짝수인지 홀수인지 확인

## Inputs

| Variable Name | type | meaning    |
| ------------- | ---- | ---------- |
| num           | Int  | target num |

## output

~~~scala
return String // Even or Odd
~~~

## Conditions

* num
  * in range of Integer
  * 0 is even

## Test cases

| num  | return |
| ---- | ------ |
| 3    | "Odd"  |
| 4    | "Even" |

## Solution

~~~scala
def solution(num: Int): String = {
  if (num%2 == 0) "Even" else "Odd"
}
~~~

### Study from Implementation

