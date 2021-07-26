---

title: Programmers Scala Study (level 1.32)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 32. 핸드폰 번호 가리기

## 문제 설명

주어진 전화번호 String에서 가장 뒤 4자리만 표기하고 나머지는 *로 바꾼다.

## Inputs

| Variable Name | type   | meaning                |
| ------------- | ------ | ---------------------- |
| phone_number  | String | string to be converted |

## output

~~~scala
return String // converted string
~~~

## Conditions

* s
  * length: 4~20

## Test cases

| phone_number  | return        |
| ------------- | ------------- |
| "01033334444" | "*******4444" |
| "027778888"   | "*****8888"   |

## Solution

map함수로 뒤쪽에 있는 인덱스인지 확인하고 *로 치환 여부 결정.

~~~scala
def solution(phone_number: String): String = {
  phone_number.zipWithIndex
  .map{case(num, idx) => if (idx < phone_number.length-4) '*' else num}.mkString("")
}
~~~

### Study from Implementation

