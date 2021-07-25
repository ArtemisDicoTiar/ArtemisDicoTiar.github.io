---

title: Programmers Scala Study (level 1.13)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 13. 문자열 내 마음대로 정렬하기

## 문제 설명

문자열이 담긴 어레이가 주어질때 각 문자열에서 원하는 인덱스의 문자열을 기준으로 어레이를 정렬하고 그 값을 리턴한다.

## Inputs

| Variable Name | type           | meaning                     |
| ------------- | -------------- | --------------------------- |
| string        | Vector[String] | words                       |
| n             | Int            | target character (n, index) |

## output

~~~scala
return Vector[String] // sorted array
~~~

## Conditions

* strings
  * length: 1~50
  * all characters are on lowercase
  * each word's length is 1~100
  * all words' length is larger than "n"
* if same character is selected on nth index of the word, the word is sorted based on dictionary. (그냥 같으면 사전적 정렬하겠다.)

## Test cases

| strings                 | n    | return                  |
| ----------------------- | ---- | ----------------------- |
| ["sun", "bed", "car"]   | 1    | ["car", "bed", "sun"]   |
| ["abce", "abcd", "cdx"] | 2    | ["abcd", "abce", "cdx"] |

## Solution

그냥 strings를 sortBy 해서 정렬하면 될듯.

첫번째 기준을 nth index,  두번째 기준으로 그냥 그 단어 그자체 (사전 기준).

~~~scala
def solution(strings: Vector[String], n: Int): Vector[String] = {
  return strings.sortBy(word => (word(n), word))
}
~~~



## Study from Implementation

None
