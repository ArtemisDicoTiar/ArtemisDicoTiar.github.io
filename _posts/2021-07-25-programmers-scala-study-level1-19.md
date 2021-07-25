---

title: Programmers Scala Study (level 1.19)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 19. 시저암호

## 문제 설명

n에 주어진 숫자만큼 문자열을 shift시키면 된다.

## Inputs

| Variable Name | type   | meaning               |
| ------------- | ------ | --------------------- |
| s             | String | string to be cyphered |
| n             | Int    | shifting number       |

## output

~~~scala
return String // encrypted string
~~~

## Conditions

* blank space remains as blank space
* s
  * combination of lower, upper case + blank space
  * length: ~8000
* 1 ≤ n ≤ 25

## Test cases

| s       | n    | result  |
| ------- | ---- | ------- |
| "AB"    | 1    | "BC"    |
| "z"     | 1    | "a"     |
| "a B z" | 4    | "e F d" |

## Solution

그냥 주어진 스트링을 map으로 돌면서 해당 알파벳의 인덱스를 찾고 n만큼 shift한 인덱스의 알파벳을 찾으면 됨.

~~~scala
def solution(s: String, n: Int): String = {
  val alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
  val alphabetLower = alphabet.toLowerCase()
  return s.map(char => 
               if (char == ' ') ' '
               else if (char.isUpper) alphabet((alphabet.indexOf(char) + n) % alphabet.length)
               else alphabetLower((alphabetLower.indexOf(char) + n) % alphabet.length)
              )
}
~~~

## Study from Implementation

* string case converting
  * .toLowerCase()
  * .toUpperCase()
