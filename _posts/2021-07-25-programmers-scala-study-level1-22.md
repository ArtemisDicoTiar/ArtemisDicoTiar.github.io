---

title: Programmers Scala Study (level 1.22)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 22. 자릿수 더하기

## 문제 설명

정수가 주어졌을때 각 자릿수의 수를 더한다.

## Inputs

| Variable Name | type | meaning        |
| ------------- | ---- | -------------- |
| n             | Int  | integer number |

## output

~~~scala
return Int // sum of number n's each position.
~~~

## Conditions

* n= ~100,000,000 

## Test cases

| n     | return      |
| ----- | ----------- |
| 12345 | [5,4,3,2,1] |

## Solution

일단 그냥 스트링으로 변환하고 map해서 digit으로 변환 sum하자.

~~~scala
def solution(n: Int): Int = {
  n.toString.map(_.asDigit).sum
}
~~~

### Study from implementation

- integer to string은
  - .toString하면된다.
- char to int는
  - .asDigit하면 된다.
