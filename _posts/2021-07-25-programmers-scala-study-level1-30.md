---

title: Programmers Scala Study (level 1.30)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 30. 평균 구하기

## 문제 설명

정수 어레이의 평균을 구하시오.

## Inputs

| Variable Name | type        | meaning           |
| ------------- | ----------- | ----------------- |
| arr           | Vector[Int] | array of integers |

## output

~~~scala
return Double // average
~~~

## Conditions

* arr
  * length: 1~100
  * value: -10 000 ~ 10 000

## Test cases

| arr       | return |
| --------- | ------ |
| [1,2,3,4] | 2.5    |
| [5,5]     | 5      |

## Solution

sum/length

단, sum한 결과를 더블로 타입 케스팅해야 리턴값이 더블로 맞게 나온다.

~~~scala
def solution(arr: Vector[Int]): Double = {
  return arr.sum.toDouble / arr.length
}
~~~

### Study from Implementation

