---

title: Programmers Scala Study (level 1.10)

categories:
  - Programming Study
last_modified_at: 2021-07-24 14:27:00 +0100

tags: [programming, study, scala]

---

# 10. 2016년

## 문제 설명

2016년 a월 b일의 요일은?

## Inputs

| Variable Name | type | meaning |
| ------------- | ---- | ------- |
| a             | Int  | Month   |
| b             | Int  | Date    |

## output

~~~scala
return String // Day of (month of a / date of b)
~~~

## Conditions

* 2016년은 윤년이다
* a, b 는 실존하는 날짜만 주어진다.

## Test cases

| a    | b    | result |
| ---- | ---- | ------ |
| 5    | 24   | "TUE"  |

## Solution

윤년이면 2월이 29일까지 있는 해이다.

2016년 1월 1일은 금요일이다.

~~~scala
def solution(a: Int, b: Int): String = {
  val dates = Vector[Int](31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31)
  val days = Vector[String]("FRI", "SAT", "SUN", "MON", "TUE", "WED", "THU")

  val diffDates = (1 to a-1).map(month => dates(month-1)).sum + b - 1

  return days(diffDates%7)
}
~~~



## Study from Implementation

None
