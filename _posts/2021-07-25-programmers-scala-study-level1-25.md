---

title: Programmers Scala Study (level 1.25)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 25. 정수 제곱근 판별

## 문제 설명

주어진 숫자가 어떤수의 제곱인지 확인하고 제곱이면 그 수에 1더한 수를 리턴 아니면 -1.

## Inputs

| Variable Name | type | meaning |
| ------------- | ---- | ------- |
| n             | Long | Integer |

## output

~~~scala
return Long // processed num
~~~

## Conditions

* 1 ≤ n ≤ 50000000000000

## Test cases

| n    | return |
| ---- | ------ |
| 121  | 144    |
| 3    | -1     |

## Solution

그냥 if else쓰면 될듯.

~~~scala
def solution(n: Long): Long = {
  val rooted = math.sqrt(n).toLong
  if (rooted * rooted == n) return ((rooted+1) * (rooted+1))
  else return -1
}
~~~

### Study from Implementation

* 스칼라에서 제곱근은 
  * math.sqrt에 있다.
