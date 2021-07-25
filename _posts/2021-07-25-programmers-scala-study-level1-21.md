---

title: Programmers Scala Study (level 1.21)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 21. 이상한 문자 만들기

## 문제 설명

문자열의 짝수번재 알파벳은 대문자로, 홀수번째는 소문자로 변환.

## Inputs

| Variable Name | type   | meaning                         |
| ------------- | ------ | ------------------------------- |
| s             | String | English words in all lower case |

## output

~~~scala
return String // converted string
~~~

## Conditions

* 변환시 각 단어의 홀짝 인덱스로 처리해야한다.
* 첫번째 글자는 0번째인데 이를 짝수로 처리한다.

## Test cases

| s                 | return            |
| ----------------- | ----------------- |
| "try hello world" | "TrY HeLlO WoRlD" |

## Solution

range로 1부터 값을 생성한 뒤에 divisor인지 확인해서 filter 하고 sum

했는데 안된다.

질문을 좀 읽어보니 뒤에 blankspace가 뒤에 주루룩 붙은 경우땜에 생기는 문제란다. 뒤에 붙는 경우는 지우게끔

~~~scala
.split(" ", -1) 
~~~

뒤에 -1을 붙인다.

~~~scala
def solution(s: String): String = {
  return s.split(" ", -1)
  .map(word => 
       word.zipWithIndex.map{case (char, idx) => if (idx%2 == 0) char.toUpper else char.toLower}.mkString("")
      )
  .mkString(" ")
}
~~~

### Study from Implementation

* string과 char의 대소문자화가 다르다
  * string
    * toUpperCase()
    * toLowerCase()
  * char
    * toUpper
    * toLower
