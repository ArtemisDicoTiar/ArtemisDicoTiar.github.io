---

title: Programmers Scala Study (level 1.12)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 12. 두 정수 사이의 합

## 문제 설명

주어진 두개의 정수 사이의 합을 리턴.

## Inputs

| Variable Name | type | meaning |
| ------------- | ---- | ------- |
| a             | Int  | start   |
| b             | Int  | end     |

## output

~~~scala
return Int // sum of integers between a and b
~~~

## Conditions

* a 와 b가 동일한 경우 그 수를 리턴.
* -10 000 000 ≤ a (b) ≤ b (a) ≤ 10 000 000
* order of a and b is not decided.

## Test cases

| a    | b    | return |
| ---- | ---- | ------ |
| 3    | 5    | 12     |
| 3    | 3    | 3      |
| 5    | 3    | 12     |

## Solution

처음엔 어레이를 생성해서 계산할까 했는 데 수학적 해결방안이 있을 거 같다.

수학적해결책인
$$
\begin{align*}
{(a+b)\over2}\times(abs(a-b)+1)
\end{align*}
$$
이런 수식을 구현했는데 테스트 케이스의 1/3정도가 틀린다.

그러다 우연히 확인한 solution함수의 리턴 타입이 Long이다..

타입 문제인가 싶어서 a 랑 b를 Long으로 타입캐스팅했더니 풀린다 ㅋㅋㅋㅋㅋ 

너무 파이썬만 했더니 타입의 중요성을 잊고 있었다. 아마도 그냥 계산하면 Int로 다운캐스팅해서 계산하는 데 그러면 오버플로우가 일어나서 계산값이 틀리는 거 같다.

~~~scala
def solution(a: Int, b: Int): Long = {
  return (a.asInstanceOf[Long] + b.asInstanceOf[Long]) * ((a-b).abs+1) / 2
}
~~~



## Study from Implementation

- type cast in scala
  - A.asInstanceOf[<casting type>]
