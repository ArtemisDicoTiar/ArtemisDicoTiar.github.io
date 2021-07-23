---

layout: post

title: Programmers Scala Study (level 1.4)

date: 2021-07-22 14:27:00 +0100

description: Programmers coding study with programming language Scala. The difficulty selected is level 1.

tags: [programming, study, scala]

---

# 4. 음양 더하기

## 문제 설명

정수 리스트에 부호 리스트를 적용해서 합을 구해라.

 ## Inputs

| Variable Name | type            | meaning                    |
| ------------- | --------------- | -------------------------- |
| absolutes     | Vector[Int]     | numbers that are absoluted |
| signs         | Vector[Boolean] | sign for number            |

## output

~~~scala
return Int // Sum of numbers
~~~

## Conditions

* absolutes
  * length: 1~1000
* signs
  * same length of absolutes

## Test cases

| absolutes  | signs                | result |
| ---------- | -------------------- | ------ |
| `[4,7,12]` | `[true,false,true]`  | 9      |
| `[1,2,3]`  | `[false,false,true]` | 0      |

## Solution

그냥 absolutes랑 signs  zip한뒤에 reduce하면 될듯.

~~~scala
def solution(absolutes: Vector[Int], signs: Vector[Boolean]): Int = {
        return absolutes.zip(signs).map(row => if (row._2) row._1 else -row._1).sum
    }
~~~

생각대로 됨. zip하고 map해서 숫자에 음양 붙이고 해당 벡터 전체의 sum 구하면 끝.

## Study from Implementation

* Iterable의 합은 .sum을 붙이면 된다.
