---

title: Programmers Scala Study (level 1.28)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 28. 최대공약수와 최소공배수

## 문제 설명

두수의 최대공약수와 최소공배수 리턴.

## Inputs

| Variable Name | type | meaning |
| ------------- | ---- | ------- |
| n             | Int  | num1    |
| m             | Int  | num2    |

## output

~~~scala
return Vector[Int](GCD, LCM) // Even or Odd
~~~

## Conditions

* n & m
  * 1~1000000

## Test cases

| n    | m    |
| ---- | ---- |
| 3    | 12   |
| 2    | 5    |

## Solution

$$
lcm(a,b) = {|a \cdot b| \over gcd(a,b)}
$$

~~~pseudocode
def gcd(a, b)
	if (b == 0) return a
	else gcd(a, a%b)
~~~

~~~scala
def gcd(a: Int, b: Int): Int = if(b == 0) a else gcd(b, a%b)
def lcm(a: Int, b: Int): Int = (a*b) / gcd(a, b)
def solution(n: Int, m: Int): Vector[Int] = {
  return Vector[Int](gcd(n, m), lcm(n, m))
}
~~~

### Study from Implementation

