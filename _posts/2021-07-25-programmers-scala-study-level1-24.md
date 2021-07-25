---

title: Programmers Scala Study (level 1.24)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 24. 정수를 내림차순으로 배치하기

## 문제 설명

sort numbers of each position in n

## Inputs

| Variable Name | type | meaning |
| ------------- | ---- | ------- |
| n             | Long | Integer |

## output

~~~scala
return Long // sorted numbers
~~~

## Conditions

* 1 ≤ n ≤ 8000000000

## Test cases

| n      | return |
| ------ | ------ |
| 118372 | 873211 |

## Solution

toString.map(asDigit).sorted.join.toInt 하면 될거 같은데?

했더니 런타임 에러가 나네 ㅋㅋㅋ 

아 리턴값 Long이네

~~~scala
def solution(n: Long): Long = {
  n.toString.sorted.reverse.toLong
}
~~~



## Study from Implementation

* string join
  * .mkString("조인할 때 사이에 들어갈거")
* 스트링도 소팅이 된다.
