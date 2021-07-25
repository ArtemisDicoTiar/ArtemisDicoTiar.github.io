---

title: Programmers Scala Study (level 1.11)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 11. 나누어 떨어지는 숫자 배열

## 문제 설명

어레이에 담긴 숫자 중 divisor로 나누어덜어지는 값을 오름차순으로 정렬한 배열을 리턴.

divisor로 나눠지는 숫자가 없다면 -1을 배열에 담아 리턴.

## Inputs

| Variable Name | type        | meaning |
| ------------- | ----------- | ------- |
| arr           | Vector[Int] | Numbers |
| divisor       | Int         | Divisor |

## output

~~~scala
return Vector[Int] // ascending order sorted element that is divisable with divisor
~~~

## Conditions

* arr 에는 자연수만 있다.
* arr에 담긴 숫자에 중복은 없다.
* divisor도 자연수다.
* arr의 길이는 1 이상.

## Test cases

| arr           | divisor | return        |
| ------------- | ------- | ------------- |
| [5, 9, 7, 10] | 5       | [5, 10]       |
| [2, 36, 1, 3] | 1       | [1, 2, 3, 36] |
| [3,2,6]       | 10      | [-1]          |

## Solution

arr에 필터를 걸고 sort하면 끝. 길이가 0이면 -1을 리턴하면 되는데 if문으로 확인하는 거 좋은 건가...?

그냥 if 문 사용하는 게 최선의 해결책이네 ㅋㅋ

~~~scala
def solution(arr: Vector[Int], divisor: Int): Vector[Int] = {
  return if (arr.filter(v => v % divisor == 0).sorted.length != 0) arr.filter(v => v % divisor == 0).sorted else Vector[Int](-1)
}
~~~



## Study from Implementation

None
