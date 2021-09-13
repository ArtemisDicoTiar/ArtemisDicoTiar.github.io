---
title: JavaScript Tip5

categories:
  - Programming Study
  - JavaScript

last_modified_at: 2021-09-11

tags: [programming, study, javascript, js]

---

# Tip5. 배열로 유연한 컬렉션을 생성하라

## Rough Reading

원래 자바스크립트에서 데이터 컬렉션을 다루는 구조는

1. 배열 (Array)
2. 객체 (Object)

모던 자바스크립트에는

1. Map
2. Set
3. WeakMap
4. WeakSet
5. Object
6. Array

### Array

여기서 어떤 작업(추가, 제거, 정렬, 필터링, 교체 등)이던 가능해야한다면 어레이가 제일 적합한 선택일 것이다.

`.map(), .filter(), .reduce()` 등의 배열 메소드를 사용해서 배열의 값을 변경, 갱신 할 수 있다.

### Object

객체를 순회하기 위해서는 `Object.keys()`를 실행해서 돌면된다.

객체를 순회할 때도 어레이가 사용된다.

이처럼 어레이가 어디서나 사용되는 데 이는 어레이에 iterable이 내장되어 있기 때문.

### Object to Array

파이썬에서는 dictionary를 2D List로 변환하려면 `dict.items()`를 사용하면 된다.

비슷한 기능이 자바스크립트에도 있는 데 `Object.entries()`를 사용하면 된다.

ES5, 6에서 가장 많이 추가, 변경된 내용이 어레이였다고한다. 

그만큼 어레이가 제일 핵심적인 데이터 컬렉션이고, 어레이만 정확하게 잘 사용하면 원하는 기능 구현에 무리가 없다.



## Tips

어레이가 대부분의 상황에 잘 맞는 데이터 컬렉션이다.



## Summary

* 어떤 컬렉션을 써야할 지 잘 모르겠다면 어레이를 쓰자.

