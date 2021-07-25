---

title: Programmers Scala Study (level 1.23)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 23. 자연수 뒤집어 배열로 만들기

## 문제 설명

자연수 n을 뒤집어 각자리를 원소로 갖는 배열을 리턴.

## Inputs

| Variable Name | type | meaning       |
| ------------- | ---- | ------------- |
| n             | Long | target number |

## output

~~~scala
return Vector[Int] // array of reverse position of number n
~~~

## Conditions

* n= ~10,000,000,000

## Test cases

| n     | return      |
| ----- | ----------- |
| 12345 | [5,4,3,2,1] |

## Solution

이번 문제도 역시 그냥 스트링으로 변환 map에서 asDigit 하고 reverse.

했는데 안된다. 결과로 ArraySeq가 나와서 타입이 안 맞다. Vector로 어떻게 casting하지?

~~~scala
def solution(n: Long): Vector[Int] = {
  n.toString.map(_.asDigit).reverse.toVector
}
~~~

### Study from implementation

- ArraySeq to Vector
  - 그냥 간단하게 .toVector 다.
