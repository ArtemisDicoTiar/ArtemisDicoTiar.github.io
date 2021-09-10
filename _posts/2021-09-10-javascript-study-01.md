---
title: Tip1. const로 변하지 않는 값을 표현하라.

categories:
  - Programming Study
  - JavaScript

last_modified_at: 2021-09-10

tags: [programming, study, javascript, js]

---

# Tip1. const로 변하지 않는 값을 표현하라.

## Words

### ECMAScript # (ES #)

ES6, ES5같은게 이걸 의미하는 거다. 자바스크립트 기술 명세서. 파이썬으로 치면 PEP517같은 것.

ES5, 6에서 주요한 문법이 변경되었다. 명세는 매년 갱신된다. 

사람마다 ES6 혹은 ES2016 으로 부르곤 한다.

## Rough Reading

`const` 를 이용해 재할당을 피하고 우리의 의도를 다른사람들에게 전달하는 방법

모던 자바스크립트에서는 새로운 변수 선언 방법을 제안했다.

1. `var` 

2. `let` 

3. `const` 

   1. 가장 적은 것을 할 수 있다. 

   2. 그래서 대부분의 경우에는 const가 좋다. 

   3. 코드를 읽기 쉽게 만들어준다.

   4. **<u>블록 문맥 내에서 재할당 할 수 없는 변수 선언</u>**이다.

      1. 즉 define하면 변경이 안된다.
      2. 근데 이게 immutable을 뜻하는 건 아니다.
      3. 무슨 말이냐면 const Arr[3] 이렇게 선언해도 어레이 내의 값을 수정할 수 있다는 것이다.

   5. 다른 언어에 익숙하면 이런 변수 선언이 추천대상인게 이상할 수 있다.

      1. 왜냐하면 보통의 언어에서는 상수할당을 **대문자** 로 그리고, **불변값**에 하기 때문.

         ~~~c
         const int PI=3.14;
         ~~~

   6. 근데 어떤 변수를 신경쓰지 않아도 되는 지를 잘 표현해주면 이후에 코드를 보는 데 편해진다.

eg.

~~~javascript
// with const
const taxRate = 0.1
const total = 100 + (100 * taxRate)
// 줄 건너 뛰기~
return `구매 금액은 ${total}입니다.`
~~~

위 코드에서는 구매 금액 110인 것을 정확하게 알수 있다. 왜냐하면 해당 변수를 const로 선언해 재할당 할 수 없는 것을 보였기 때문. 반면.

~~~javascript
// with var
var taxRate = 0.1
var total = 100 + (100 * taxRate)
// 줄 건너 뛰기~
return `구매 금액은 ${total}입니다.`
~~~

위 코드는 var를 사용함으로써 재할당 가능함을 보였고 이로 인해 "줄 건너 뛰기" 내에서 해당 값이 변경되었는 지 아닌지를 전부 확인해줘야 결과를 알 수 있다.

~~~javascript
// with const & let
const taxRate = 0.1
const shipping = 5.00
let total = 100 + (100 * taxRate) + shippping
// 줄 건너 뛰기~
return `구매 금액은 ${total}입니다.`
~~~

위와 같이 코드를 작성한 경우, taxRate와 shipping이 const로 선언되어 재할당 불가함을 보였지만 total은 let으로 선언되어 해당 값이 변동 될 수 있음을 보였다. 고로 total값이 유지되는 지를 확신할 수 없다.



**<u>고로 const를 자주 사용해서 유지되는 값을 할당하고, let을 드물게 사용하면 변경되는 부분들을 예측 할 수 있어진다.</u>**



> **<u>주의</u>** 해야하는 점은 const는 불변값 할당이 아니다라는 점이다.

eg. 

~~~javascript
const discountable = []
// skipping
for (let i = 0; i < cart.length; i++) {
  if (cart[i].discountAvailable) {
    discountable.push(cart[i])
  }
}
~~~

위와 같은 코드가 있을 때, discountable이 const로 선언되었지만 여전히 배열에 값을 추가할 수 있다.

이런 특징은 앞에서 말한 값의 유지불가라는 문제를 발생시킨다.

그래서 결국 **mutation을 피할 수 있으면 피하자** 라는 것이 최선이다.

(*람다식 같이 적으면 해결되나 싶은 생각이 들었는데 책 바로 밑에 나온다.)

~~~javascript
const discountable = cart.filter(item => item.discountAvailable)
~~~

이런식으로 함수형 프로그래밍을 해두면 discountable을 mutate하지 않고 cart.filter(...)의 결과를 바로 할당하니 (물론 바로 할당이라기 보단 promise를 넘겨주게 되겠지만) 

## Summary

* const를 최대한 사용하자.
* 최대한 값을 immutable하게 하자.
* loop를 돌며 값을 순회해야하는 경우에는 scala에서 공부했던것처럼 functional하게 작성하자.

