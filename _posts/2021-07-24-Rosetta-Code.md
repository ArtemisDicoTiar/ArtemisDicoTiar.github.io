---

title: [Bookmark] Rosetta Code

categories:
  - Programming Study
last_modified_at: 2021-07-24 14:27:00 +0100

tags: [programming, study, bookmark]

---

# [로제타 코드](https://rosettacode.org/wiki/Rosetta_Code)

스칼라 공부하면서 찾은 좋은 사이트다.

처음엔 그냥 스칼라에서 뭐뭐하는 법 이런식으로 검색했다.

방금 전엔 스칼라로 약수 개수 확인하는 방법을 검색했다. (물론 머리속으로 해결책을 적긴했는 데 너무 스칼라스럽지 않아서 검색했는데 검색하길 잘했다. 아직 Functional Programming에 미숙하다 보니 자꾸 기존의 Procedural 혹은 Object-Oriented Programming으로 사고한다.)

그러다 찾았는데 내가 검색한 문제처럼 뭐뭐하는 법을 굉장히 다양한 프로그래밍 언어로 구현이 되어 있다. 

오픈 위키같은 형태라 여럼 사람들이 contribute하는 거 같다.

* 약수 개수 문제의 경우 78개의 언어로 작성 되어 있다. (어샘블리 언어는 물론 매트랩도 있다 ㅋㅋㅋ)

* 심지어 각 언어별로 구현 방법이 다양하면 각 방법별 특징을 설명해주면서 해결책이 나온다.
* 파이썬은 4가지 해결책이 있다. ㅋㅋㅋ (방금 쭉 읽었는데 좀 과하게 적었는데? Test케이스 다른 언어엔 없는 데 왜 있는 거야 ㅋㅋ)

나처럼 익숙해진 언어를 벗어나서 여러개의 다른 언어를 공부하거나 갈아타려는 사람들에게 좋은 거 같다.

스칼라 말고 고랭도 같이 공부하려 하는 데 스칼라 solution과 함께 고랭 solution 하나 첨부한다.

~~~scala
def properDivisors(n: Int) = (1 to n/2).filter(i => n % i == 0).length
~~~

~~~go
package main
 
func countProperDivisors(n int) int {
    if n < 2 {
        return 0
    }
    count := 0
    for i := 1; i <= n/2; i++ {
        if n%i == 0 {
            count++
        }
    }
    return count
}
 
~~~



### conclusion

Functional이 수학적으로 사고하는 데에만 익숙해지고 문제상황이 수학적인 해결책이 더 간단하면 이게 더 깔끔하고 보기도 좋고 사이드 이펙트도 확실히 없어 보인다.

( 그래서 안그래도 파이썬에서 람다식 자주 사용하는 데 스칼라 익숙해지면 스칼라로 이주할 수 있는 건 이주 해봐야겠다. :) )
