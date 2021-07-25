---

title: Programmers Scala Study (level 1.16)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 16. 서울에서 김서방 찾기

## 문제 설명

string이 담긴 어레이에서 "Kim"이 담긴 인덱스를 리턴.

## Inputs

| Variable Name | type           | meaning            |
| ------------- | -------------- | ------------------ |
| seoul         | Vector[String] | Sir names in array |

## output

~~~scala
return s"김서방은 %d에 있다".format(index) // index -> where Kim is in the seoul
~~~

## Conditions

* seoul
  * length: 1~1000
  * each Sir name's length is 1~20
  * "Kim" is definitely in seoul array.

## Test cases

| seoul           | return              |
| --------------- | ------------------- |
| ["Jane", "Kim"] | "김서방은 1에 있다" |

## Solution

그냥 seoul에 indexOf함수 적용하면 되지 않나? 맞다~

~~~scala
def solution(seoul: Vector[String]): String = {
  return "김서방은 %d에 있다".format(seoul.indexOf("Kim"))
}
~~~

### Study from Implementation

~~~scala
def solution(s: String): Boolean = {
  if (s.length != 4 && s.length != 6) return false
  return s.forall(_.isDigit)
}
~~~



## Study from Implementation

* string formatting in scala

  * ```scala
    "%s %s, age %d".format(firstName, lastName, age)
    ```
