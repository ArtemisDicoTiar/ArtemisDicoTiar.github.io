---
title: JavaScript Tip3

categories:
  - Programming Study
  - JavaScript

last_modified_at: 2021-09-11

tags: [programming, study, javascript, js]

---

# Tip3. 블록 유효 범위 변수로 정보를 격리하라

## Issues



## Rough Reading

for 문을 작성할 때 잘못된 변수를 선택하는 실수가 있다. (eg. for 블록 외부의 변수를 내부에서 사용.)

eg.

~~~javascript
function addClick(items) {
  for (var i = 0; i < items.length; i++) {
    items[i].onClick = function () {
      return i;
    }
  }
  return items;
}

const example = [{}, {}]
const clickSet = addClick(example)
clickSet[0].onClick()

// clickSet의 어떤 요소를 선택하더라도 items.length가 반환된다.
~~~

유효범위의 문제로 생긴다.

var로 할당한 변수는 함수 유효 범위를 따른다 (정확히는 어휘적 유효 범위). 그렇기 때문에 함수 내에 할당된 마지막 값을 참조하게 된다.

> 무슨 말인가 하고 생각해보니: for loop을 다 돈 시점에 (예시 길이: 3) items의 형태는 다음과 같다.
>
> [{onClick: () ⇒ return 1}]
>
> [[{onClick: () ⇒ return 2}, {onClick: () ⇒ return 2}]
>
> [[{onClick: () ⇒ return 3}, {onClick: () ⇒ return 3}, {onClick: () ⇒ return 3}]
> 이런식으로 흐르게 된다. 즉, i값이 각 for loop마다 사용되고 사라지는 게 아니라 계속해서 i를 반환하게 설정되어 있기 때문에 마지막에서 할당되는 3이 리턴된다.

이를 해결하는 방법은 크게 3가지가 있다. 그렇지만 이 방법이 아닌 다른 쉬운 방법으로도 해결할 수 있다.

1. 클로져: 다른 함수가 사용할 수 있도록 함수 내부에서 변수를 생성하는 것.
2. 고차 함수: 다른 함수를 반환하는 함수 (함수형 프로그래밍에서 자주 보이던 그 개념.)
3. 즉시 실행 함수: () ⇒ {}

쉬운 해결책은 let을 사용하는 것이다.

let은 블록 유효범위를 따르기 때문에 for loop을 돌면서 onClick에 해당 값을 할당하면 다음 함수 블록에는 영향을 줄 수 없다.

쉽게 생각해서 let은 해당 함수내의 값을 잠궈 버린다. 

아래 그림을 보면 쉽게 이해될 것이다.

### var를 사용했을 때

![js_tip3_var](/assets/post/js_tip3_var.png)

### let을 사용했을 때

![js_tip3_let](/assets/post/js_tip3_let.png)

이런 이유로 var는 최대한 기피하고 let을 사용하자.

## Tips

var는 최대한 기피하고 let을 사용하자.

## Summary

* var를 사용해서 생긴 문제는 어려운 해결책 3개, 쉬운 해결책 1개를 사용해볼수 있다.
  * 클로져 함수
  * 고차 함수
  * 즉시 실행 함수
  * **var → let**

