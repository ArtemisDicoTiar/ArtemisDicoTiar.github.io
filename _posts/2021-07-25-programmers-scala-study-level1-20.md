---

title: Programmers Scala Study (level 1.20)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 20. 약수의 합

## 문제 설명

정수 n의 약수를 모두 더한 값을 리턴.

## Inputs

| Variable Name | type | meaning        |
| ------------- | ---- | -------------- |
| n             | Int  | integer number |

## output

~~~scala
return Int // sum of divisors of "n"
~~~

## Conditions

* n= 0~3000

## Test cases

| n    | return |
| ---- | ------ |
| 12   | 28     |
| 5    | 6      |

## Solution

range로 1부터 값을 생성한 뒤에 divisor인지 확인해서 filter 하고 sum

~~~scala
def solution(n: Int): Int = {
  return (1 to n).filter(num => n % num == 0).sum
}
~~~

