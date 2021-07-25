---

title: Programmers Scala Study (level 1.14)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 14. 문자열 내림차순으로 배치하기

## 문제 설명

문자열을 큰것부터 작은 순으로 정렬해서 새로운 문자열을 생성.

대문자를 작은거, 소문자를 큰거로 간주한다.

알파벳순서로 큰게 앞으로 작은게 뒤로 와야한다.

## Inputs

| Variable Name | type   | meaning                                      |
| ------------- | ------ | -------------------------------------------- |
| s             | String | string combination of upper and lower cases. |

## output

~~~scala
return String // sorted string
~~~

## Conditions

* s length is larger than 0

## Test cases

| s         | return    |
| --------- | --------- |
| "Zbcdefg" | "gfedcbZ" |

## Solution

대문자 모으고 소문자 모은뒤에 각각을 역 정렬한 다음에 소문자 + 대문자 하면 끝

~~~scala
def solution(s: String): String = {
  var up = ""
  var low = ""
  s.foreach(c => if (c.isUpper) up += c else low += c)

  return low.sorted.reverse + up.sorted.reverse
}
~~~



## Study from Implementation

* 대문자 확인 함수: "문자열".isUpper
