---

title: Programmers Scala Study (level 1.9)

categories:
  - Programming Study
last_modified_at: 2021-07-24 14:27:00 +0100

tags: [programming, study, scala]

---

# 9. 약수의 개수와 덧셈

## 문제 설명

두 정수 사이의 모든 수중 약수가 짝수인 수는 더하고 홀수인 수는 빼서 총합을 출력.

## Inputs

| Variable Name | type | meaning      |
| ------------- | ---- | ------------ |
| left          | Int  | start number |
| right         | Int  | end number   |

## output

~~~scala
return Int // sum of the numbers based on the following condition
~~~

## Conditions

* number range
  * 1 ≤ left ≤ right ≤ 1000 
* summation process
  * divisor even → sum += num, divisior odd → sum -= num

## Test cases

| left | right | result |
| ---- | ----- | ------ |
| 13   | 17    | 43     |
| 24   | 27    | 52     |

## Solution

숫자 range로 Vector 생성후 map함수로 해당 숫자의 약수 개수 확인후 해당 숫자 음수 혹은 양수 처리. 최종 벡터 sum

~~~scala
def isEvenDivisor(num: Int): Boolean = ((1 to num/2).filter(i => num % i == 0).length + 1) % 2 == 0
def solution(left: Int, right: Int): Int = {
  return (left to right).map(num => if (isEvenDivisor(num)) num else -num).sum
}
~~~



## Study from Implementation

* 시작과 끝을 알고 있는 숫자 리스트를 더 쉽게 생성할 수 있다.
  * 그냥 (start to end by step) 이라고 적으면 된다.
