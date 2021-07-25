---

title: Programmers Scala Study (level 1.26)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 26. 제일 작은 수 제거하기

## 문제 설명

주어진 숫자 어레이에서 제일 작은 수를 pop

만약 pop후 배열이 비어있으면 -1을 담아서 리턴

## Inputs

| Variable Name | type        | meaning          |
| ------------- | ----------- | ---------------- |
| arr           | Vector[Int] | array of numbers |

## output

~~~scala
return Vector[Int] // processed nums
~~~

## Conditions

* arr
  * length: 1~
  * no duplicates.

## Test cases

| arr       | return  |
| --------- | ------- |
| [4,3,2,1] | [4,3,2] |
| [10]      | [-1]    |

## Solution

어레이에 필터링 하고 길이 if else로 확인.

~~~scala
def solution(arr: Vector[Int]): Vector[Int] = {
  val res = arr.filter(v => v != arr.min)

  return if (res.length == 0) Vector[Int](-1) else res
}
~~~

### Study from Implementation

