---

layout: post

title: Programmers Scala Study (level 1.5)

date: 2021-07-22 14:27:00 +0100

description: Programmers coding study with programming language Scala. The difficulty selected is level 1.

tags: [programming, study, scala]

---

# 5. 내적

## 문제 설명

a 벡터와 b 벡터의 내적을 구하시오

 ## Inputs

| Variable Name | type        | meaning             |
| ------------- | ----------- | ------------------- |
| a             | Vector[Int] | mathematical vector |
| b             | Vector[Int] | mathematcial vector |

## output

~~~scala
return Int // a \dot b
~~~



## Conditions

* length of a & b: 1~1000
* all numbers in a & b → -1000~1000

## Test cases

| a           | b             | result |
| ----------- | ------------- | ------ |
| `[1,2,3,4]` | `[-3,-1,0,2]` | 3      |
| `[-1,0,1]`  | `[1,0,-1]`    | -2     |

## Solution

1. 내적 관련 함수가 있나 보자. 데이터 타입 이름이 벡터인데 있을 거 같다.
   1. product라는 함수가 있어서 dot product인줄 알았더니 해당 Iterable에 있는 모든 수의 곱이다.
2. 없으면 그냥 zip하고 map으로 곱하고 sum으로 합하면 된다.
   1. 그냥 이거로 해결해야겠다.

~~~scala
def solution(a: Vector[Int], b: Vector[Int]): Int = {
  return a.zip(b).map(nums => nums._1 * nums._2).sum
}
~~~



## Study from Implementation

* 데이터 타입 이름이 벡터라 dot product, cross product 정도는 내장으로 구현되어 있을 줄 알았더니 없더라..
