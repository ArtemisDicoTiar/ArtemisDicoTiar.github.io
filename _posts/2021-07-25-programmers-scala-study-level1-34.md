---

title: Programmers Scala Study (level 1.34)

categories:
  - Programming Study
last_modified_at: 2021-07-26

tags: [programming, study, scala]

---

# 34. x만큼 간격이 있는 n개의 숫자

## 문제 설명

정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴

## Inputs

| Variable Name | type | meaning      |
| ------------- | ---- | ------------ |
| x             | Int  | start number |
| n             | Int  | count        |

## output

~~~scala
return Vector[Long] // array of numbers
~~~

## Conditions

* x range: -10000000 ~ 10000000
* n ≤ 1000

## Test cases

| x    | n    | answer       |
| ---- | ---- | ------------ |
| 2    | 5    | [2,4,6,8,10] |
| 4    | 3    | [4,8,12]     |
| -4   | 2    | [-4, -8]     |

## Solution

while loop 쓰기 싫었는 데 써야겠다...

~~~scala
def solution(x: Int, n: Int): Vector[Long] = {
  var ans = Vector[Long]()
  var cnt: Int = n
  while (cnt > 0) {
    ans = ans :+ (x.toLong*cnt.toLong)
    cnt -= 1
  }
  return ans.reverse
}
~~~

### Study from Implementation
