---
title: JavaScript Tip6

categories:
  - Programming Study
  - JavaScript

last_modified_at: 2021-09-13

tags: [programming, study, javascript, js]

---

# Tip6. Includes()로 존재 여부를 확인하라

## Rough Reading

어레이에 특정 값이 있는 지 여부를 확인 할 수 있는 메소드가 여러가지 있다. 

1. `어레이.indexOf(검색 할 값)`

   1. 이 메소드는 어레이에 해당 값이 있으면 해당 값의 인덱스 값이
   2. 없다면 -1이 반환된다.
   3. 문제:
      1. 이 기능을 사용하는 경우는 0번째에 값이 있는 경우 문제가 될 수 있다.
      2. 모든 언어에서가 그렇듯, 0은 false, 1은 true로 처리되는 데
      3. 로직을 잘못 작성하게 되면 0번째에 값이 있는데 실수로 false로 처리할 수도 있다.
      4. 이런 실수 없이 처리할 수 있는 메소드가 다음 메소드다

2. `어레이.includes(검색 할 값)`

   1. 이 메소드는 직관적으로 있으면 true, 없으면 false를 준다.

   2. 혹여나 인덱스 값이 필요하더라도 true가 반환된 경우 인덱스를 찾으면 된다.

      

## Tips

indexOf메소드는 includes에서 true가 반환되면 사용하자

## Summary

* 어레이에서 값의 존재 여부는 includes메소드를 사용하자.

