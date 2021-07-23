---

layout: post

title: Programmers Scala Study (level 1.7)

date: 2021-07-22 14:27:00 +0100

description: Programmers coding study with programming language Scala. The difficulty selected is level 1.

tags: [programming, study, scala]

---

# 7. 소수 만들기

## 문제 설명

주어진 숫자들 중 3개를 더해서 소수가 되는 경우의 수를 구해라

 ## Inputs

| Variable Name | type        | meaning |
| ------------- | ----------- | ------- |
| nums          | Vector[Int] | Numbers |

## output

~~~scala
return Int // nums에서 3개를 조합해서 나오는 소수의 개수
~~~

## Conditions

* nums
  * length: 3~50
  * value: 1~1000, no duplicates

## Test cases

| nums        | result |
| ----------- | ------ |
| [1,2,3,4]   | 1      |
| [1,2,7,6,4] | 4      |

## Solution

인덱스 3개 혹은 value 3개를 뽑아서 연산시 소수인지 확인후 boolean으로 변환

combination 생성기가 있으면 더 쉬울듯.

Prime number인지확인하는 방법의 수도 코드는 다음과 같다.

~~~pseudocode
if n <= 1
	return false
else if n == 2 or 3
	return true
else if n % 2 == 0 or n % 3 == 0
	return false

for (int i = 5; i^2 <= n; i += 6)
	if n % i == 0 or n % (i+2) == 0
		return false
		
return true
~~~

~~~scala
def isPrime(n: Int): Boolean = {
  if (n <= 1) return false
  else if (n == 2 || n == 3) return true
  else if (n%2 == 0 || n%3 == 0) return false
  else (5 to math.sqrt(n).toInt by 6)
  .forall(i => n % i != 0 
          && n % (i + 2) != 0)

}
def solution(nums: Vector[Int]): Int = {
  return nums.combinations(3).to(Vector)
  .map(nums => nums.sum)
  .map(s => isPrime(s))
  .count(x => x == true)
}
~~~



## Study from Implementation

* combination generating
  * combinations 메소드
  * 파라미터로 몇개 뽑을지 넣으면 된다.
  * Iterable이면 모두 사용가능한거 같다
* mkString 메소드
  * iterator반환되는 애를 출력할 수 있게 해준다.
* prime number check with scala

~~~scala
def isPrime(n: Int): Boolean = {
  if (n <= 1) return false
  else if (n == 2 || n == 3) return true
  else if (n%2 == 0 || n%3 == 0) return false
  else (5 to math.sqrt(n).toInt by 6) // 숫자 생성은 이렇게 (시작 to 끝 by 스텝사이즈)
  .forall(i => n % i != 0 
          && n % (i + 2) != 0)

}
~~~

