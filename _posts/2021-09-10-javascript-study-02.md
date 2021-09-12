---
title: Javascript Tip2

categories:
  - Programming Study
  - JavaScript

last_modified_at: 2021-09-10

tags: [programming, study, javascript, js]

---

# Tip2. let과 const의 유효 범위 충돌을 줄여라

## Words



## Rough Reading

**값이 변경되는 경우 let이 가장 좋은 선택이다.**

재할당이 가능하다는 점에서 var과 비슷하다. 하지만 다음과 같은 차이가 있다.

| var                              | let                          |
| -------------------------------- | ---------------------------- |
| 어휘적 유효 범위 (lexical scope) | 블록 유효 범위 (block scope) |

블록 유효 범위 변수: if 혹은 for loop 내에만 존재 → 즉 블록 밖에서 블록 안의 변수에 접근 불가

eg.

~~~javascript
function getLowestPrice(item) {
  var count = item.inventory
  var price = item.price
  if (item.salePrice) {
    var count = item.saleInventory
    if (count > 0) {
      price = item.salePrice
    }
  }
  if (count) {
    return price
  }
  return 0
}
~~~

위 코드에는 버그가 있다. if 블럭 외부의 count를 블럭 내부에서 재할당함에 따라 이후 로직에서 의미하는 count가 외부의 값인지 내부의 값인지 꼬이게 된다.

| inventory | price | salePrice | saleInventory | return Value                                                 |
| --------- | ----- | --------- | ------------- | ------------------------------------------------------------ |
| 0         | 3     | 0         | 0             | 0 (재고 없음)                                                |
| 3         | 3     | 2         | 1             | 2 (할인 가격)                                                |
| 3         | 3     | 2         | 0             | 0 (할인중이지만 할인 제품이 없다. 그러나 원래 제품이 있기 때문에 3이 나와야함.) |



eg → 올바르게 수정된 버전

~~~javascript
function getLowestPrice(item) {
  let count = item.inventory
  let price = item.price
  if (item.salePrice) {
    let count = item.saleInventory
    // 여기서 선언된 count는 외부의 count와 분리된다.
    if (count > 0) {
      price = item.salePrice
    }
  }
  if (count) {
    return price
  }
  return 0
}
~~~

이렇게만 수정해도 충분하지만 const역시 블럭단위 할당이며, 재할당을 하지 않기 때문에 const가 더 올바른 표현일 수 있다.

~~~javascript
function getLowestPrice(item) {
  const count = item.inventory
  const price = item.price
  if (item.salePrice) {
    const count = item.saleInventory
    // 여기서 선언된 count는 외부의 count와 분리된다.
    if (count > 0) {
      price = item.salePrice
    }
  }
  if (count) {
    return price
  }
  return 0
}
~~~



## Tips

let과 const에는 보호기능이 있다. → **같은 이름의 변수로는 다시 선언할 수 없는 것.**

그렇기 때문에 var보다는 let을 사용해서 변수 재선언을 TypeError로써 막을 수 있다.



## Summary

* 되도록이면 const 사용
* 변수 재할당이 필요하면 되도록 let 사용
* const, let은 블럭 단위 할당이므로 블럭간 동일 변수명을 사용해도 충돌을 막을 수 있다.
* const, let은 재선언이 불가하므로 runtime에 TypeError로 에러를 잡을 수 있다.
