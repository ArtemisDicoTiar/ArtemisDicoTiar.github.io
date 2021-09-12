---
title: JavaScript Tip4

categories:
  - Programming Study
  - JavaScript

last_modified_at: 2021-09-11

tags: [programming, study, javascript, js]

---

# Tip4. 템플릿 리터럴로 변수를 읽을 수 있는 문자열로 변환하라

## Rough Reading

쉽게 말해, `studentNumber + ':' + studentName + '(' + studentUnOfficialName + ')'` 이런식으로 적지 말라는 거다.

파이썬에서도 저렇게 작성하면 보기 힘들기 때문에 2~3가지의 방법으로 문자열을 작성한다.

1. `"{}: {}({})".format(studentNumber, studentName, studentUnOfficialName)`
   1. `"{number}: {name}({unOfficialName})".format(number=studentNumber, name=studentName, unOfficialName=studentUnOfficialName)`
2. `f"{studentNumber}: {studentName}({studentUnOfficialName})"`

이렇게 3가지 같은 2가지 해결책이다. (개인적으로는 format을 쓸때 중괄호에 변수 이름을 적어주는 게 덜 헷갈린다.)

내가 제일 선호하는 방식은 f-string이다. 번거롭게 "어떤 변수가 어디에 어떻게 넣어라 그리고 포~~맷 그 변수 값이 이거다"라고 하는 것보다 그냥 직관적이게 "자 이 자리의 변수값은 이거로 어쩌구 저쩌구 변수값."라고 쓰는 게 나아보인다.

근데 이런 기능이 자바스크립트에도 있다 그걸 템플릿 리터럴이라고 부르며  " **`** "백틱(:back-tick, 혹은 백 코테이션: back-quotation)으로 문자열을 만들면된다. (평소 사용하던 작은, 큰 따옴표 대신에 사용)

변수를 넣고 싶거든 `${변수 이름}` 하고 사용하면 된다. 

파이썬 f-string이나 format과 동일하게 중괄호 내에 연산을 실행할 수도 있다.

다만 저렇게 중괄호에 로직이 들어가면 한번에 보기도 힘들 뿐만 아니라 이해하기도 힘들다. 그러니 중요하고 복잡한 로직은 밖에서 처리하고 값만 출력하자.

이 기능은 프런트나 백엔드 로직 작성시 URL 을 꽤 자주 적는 데 그 때 유용한다. (query나 path를 변수값으로 직관적이게 적을 수 있다.)

## Tips

문자열에 변수가 들어가거든 템플릿 리터럴을 사용하자

## Summary

* \` ${studentNumber}: ${studentName}(${studentUnOfficialName}) \` 

