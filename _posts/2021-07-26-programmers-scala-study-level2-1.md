---

title: Programmers Scala Study (level 2.1)

categories:
  - Programming Study
last_modified_at: 2021-07-26

tags: [programming, study, scala, DFS, BFS]

---

# 1. 타겟 넘버

## 문제 설명

n개의 양의 정수가 어레이에 담겨 주어질때 해당 숫자들을 적절히 더하고 빼서 타겟 숫자를 구할 수 있는 경우의 수를 찾아라.

## Inputs

| Variable Name | type        | meaning           |
| ------------- | ----------- | ----------------- |
| numbers       | Vector[Int] | positive integers |
| target        | Int         | target number     |

## output

~~~scala
return Int // total possibilities of getting target number with numbers
~~~

## Conditions

* numbers
  * length: 2~20
  * value: 1~50
* target
  * value: 1~1000

## Test cases

| numbers         | target | return |
| --------------- | ------ | ------ |
| [1, 1, 1, 1, 1] | 3      | 5      |

## Solution

단계 올라오니 어렵네 ㅋㅋㅋ

트리 구조로 생각해보자.

앞에서 값을 하나씩 꺼내서 타겟에서 빼거나 더한다

길이가 0이되었을 때 목표치가 0이 되면 정답 +1 아니면 0

길이가 여전히 남아있을 경우 함수 다시적용

~~~scala
def solution(numbers: Vector[Int], target: Int): Int = {
  def sol(arr: Vector[Int], goal: Int): Int = {
    return if (arr.length == 0) {
      if (goal == 0) 1
      else 0
    } else sol(arr.slice(1, arr.length), goal-arr(0)) + sol(arr.slice(1, arr.length), goal+arr(0))
  }

  sol(numbers, target)
}
~~~

### Study from Implementation
