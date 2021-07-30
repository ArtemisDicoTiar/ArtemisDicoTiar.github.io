---

title: Programmers Scala Study (level 2.5)

categories:
  - Programming Study
last_modified_at: 2021-07-30

tags: [programming, study, scala]

---

# 5. 소수 찾기

## 문제 설명

숫자가 적힌 문자열을 조합해서 만들수 있는 소수의 개수를 구하시오.

## Inputs

| Variable Name | type   | meaning         |
| ------------- | ------ | --------------- |
| numbers       | String | numbers on note |

## output

~~~scala
return Int // number of prime numbers can be made with "numbers"
~~~

## Conditions

* numbers
  * lenght: 1~7
  * values → number: 0~9
  * eg) "013" → means number can be built with 0, 1 and 3
  * eg) "011" = "11"

## Test cases

| numbers | return |
| ------- | ------ |
| "17"    | 3      |
| "011"   | 2      |

## Solution

### Idea1

퍼뮤테이션으로 인덱스번호들을 생성하고, 해당 인덱스의 숫자들을 numbers에서 가져옴.

조합한 숫자를 toNum한 뒤에 소수인지 확인.

~~~scala
def isPrime(num: Int): Boolean = {
  if (num <= 1) false
  else if (num == 2) true
  else !(2 to (num-1)).exists(x => num % x == 0)
}
def solution(numbers: String): Int = {
  return (1 to numbers.length)
  .map(cnt => numbers.combinations(cnt).toVector)
  .flatten
  .map(opts => opts.toString.permutations.toVector)
  .flatten
  .map(num => num.toInt)
  .toSet.toVector
  .map(num => isPrime(num))
  .count(v => v == true)
}
~~~

성공! XD

### Study from Implementation

- Iterable에서 유용한 함수 두개
  - permutations
  - combinations
    - 파라미터로 개수를 넘기면 해당 개수로 골라서 수행한다.
  - 그냥 리스트나 벡터 뒤에 해당 메소드를 달기만 하면 생성된다.
  - 
