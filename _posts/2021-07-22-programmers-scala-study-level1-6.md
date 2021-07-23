---

layout: post

title: Programmers Scala Study (level 1.6)

date: 2021-07-22 14:27:00 +0100

description: Programmers coding study with programming language Scala. The difficulty selected is level 1.

tags: [programming, study, scala]

---

# 6. K번째 수

## 문제 설명

**주어진 배열**을 주어진 **두개의 인덱스**에 맞춰 시작과 끝을 잡아 자르고 **정렬**한뒤 그 배열의 **특정 순서의 값**을 알아내라

 ## Inputs

| Variable Name | type                | meaning                     |
| ------------- | ------------------- | --------------------------- |
| array         | Vector[Int]         | Numbers                     |
| commands      | Vector[Vector[Int]] | command (start, end, index) |

## output

~~~scala
return Vector[Int](result1, result2, ...) // each result is deduced by each command
~~~



## Conditions

* array
  * length: 1~100
  * value: 1~100
* commands
  * length: 1~50
  * each command length: 3

## Test cases

| array                 | commands                          | return    |
| --------------------- | --------------------------------- | --------- |
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

## Solution

slice하는 함수를 찾자 아마도 이름 그대로 일거 같긴한데.

slice뒤에 sort하고 take로 해당 인덱스의 값을 가져가면 될듯.

commands에 map함수를 걸면 될듯.

~~~scala
def solution(array: Vector[Int], commands: Vector[Vector[Int]]): Vector[Int] = {
  return commands.map(command => array.slice(command(0)-1, command(1)).sorted.apply(command(2)-1))
}
~~~



## Study from Implementation

None.
