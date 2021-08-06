---
title: Programmers Scala Study (level 2.7)

categories:
  - Programming Study
last_modified_at: 2021-08-06

tags: [programming, study, scala]

---

# 7. 예상 대진표

## 문제 설명

토너먼트를 진행한다. N명의 참가자, A번째의 참가자와 B번째의 참가자가 몇번째 라운드에 만나는 가?

이때 바라보는 A, B 플레이어는 항상 이긴다고 가정.

## Inputs

| Variable Name | type | meaning                             |
| ------------- | ---- | ----------------------------------- |
| n             | Int  | number of players                   |
| a             | Int  | index of player a (human index: 1~) |
| b             | Int  | index of player b (human index: 1~) |

## output

~~~scala
return Int // k th round that player a and b compete.
~~~

## Conditions

* n
  * 2^1 ~ 2^20 (natural number)
  * always given as 2^k. (therefore, unearned victory will never happen)
* a, b
  * ~ n (natural number)
  * a =/ b

## Test cases

| N    | A    | B    | answer |
| ---- | ---- | ---- | ------ |
| 8    | 4    | 7    | 3      |

## Solution

### Idea1

손으로 끄적거리면서 생각해보니깐 이 문제는 간단하게 다음 수식에서 최대 k_n값을 찾는 거다.
$$
a = 2^0 \times k_{a0} + 2^1 \times k_{a1} + ... + 2^n \times k_{an} \\
b = 2^0 \times k_{b0} + 2^1 \times k_{b1} + ... + 2^n \times k_{bn}
$$
a와 b의 컴퓨터 인덱스 (0~)을 위의 수식대로 표현한다고 할때, n의 최대 값을 구하면 된다.

위의 수식은 사실상 2진수 표현이기 때문에 그냥 각 수를 2진수로 구한뒤에 최대 길이를 라운드로 리턴하면 된다!

10진수 → 2진수 함수가 있는 지만 확인! 없으면 구현.

처음에 틀렸는데 보니깐 컴퓨터 인덱스로 변환안했다 ㅠㅠ ㅋㅋㅋ

~~~scala
object Solution {
    def solution(n: Int, a: Int, b: Int): Int = {
        Vector[(Int)]((a-1).toBinaryString.length, (b-1).toBinaryString.length).max
    }
}
~~~

그랬는데도 틀린다 ㅠㅠ 이렇게 풀면 안되나 보다...

### Idea2

다른사람들 풀이를 슬쩍 보니 재귀 함수로 푼다... 왜지...? 뭐하러..?

둘이 같아질때까지 2로 나눈데 왜...? → 아마도 큰수의 경우 바이너리로 변환하는 게 효율적인 문제 or 올바르지 않게 변환한 경우가 생기나보다.

~~~scala
import scala.annotation.tailrec
object Solution {
    def solution(n: Int, a: Int, b: Int): Int = {
        @tailrec
        def upSearch(a: Int, b: Int, depth: Int = 1): Int = if(a/2 == b/2) depth else upSearch(a/2, b/2, depth+1)

        upSearch(a-1, b-1)
      
    }
}
~~~

일단 @tailrec 이라는 어노테이션을 단다.

### Study from Implementation

- integer를 binary로 변환하는 함수
  - .toBinaryString
    - 정수형에 사용가능
    - 리턴타입은 문자열
- @scala.annotation.tailrec
  - tail-recursive를 표시
  - 재귀함수에 적용하면 컴파일러가 꼬리 재귀로 최적화한다.
  - 아무때나 사용하면 안된다. 에러가 발생하기도 함.
  - 머리 재귀로 구현했을 때 stackover flow가 발생하는 경우에 꼬리 재귀로 구현해서 해결 할 수도 있다.
  - [참고](https://knight76.tistory.com/entry/scala-%EA%BC%AC%EB%A6%AC-%EC%9E%AC%EA%B7%80tail-recursion%EC%99%80-tailrec)
  - [Trampoline이라는 것도 있다](https://www.secmem.org/blog/2020/04/22/tail-recursion-and-trampoline-in-scala/)
- Tail-recursive
  - 그냥 재귀함수 작성시에는 함수가 함수를 콜하는 게 쌓인다.
    - 연산 결과를 어디에 두지 않고 무작정 쌓인다. 그래서 스택에 계속 쌓이다 stack overflow발생.
  - 대신 tail-recursive하게 적으면
    - 연산 결과를 어딘가에 두고 함수를 호출하게 된다. → 그러면 무작정 끝까지 함수를 쌓지 않아도 됨.

- Trampoline
  - [이 논문](http://blog.higher-order.com/assets/trampolines.pdf)을 다들 참고 하라고 한다.
  - 그냥 하나의 포스트로 빼서 읽어야겠다.
