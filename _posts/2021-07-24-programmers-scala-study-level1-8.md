---

title: Programmers Scala Study (level 1.8)

categories:
  - Programming Study
last_modified_at: 2021-07-24 14:27:00 +0100

tags: [programming, study, scala]

---

# 8. 모의 고사

## 문제 설명

수포자 3명이 시험 문제를 다른 패턴에 맞춰 찍는다. 이때 최고 점수를 받은 사람의 번호를 리턴.

단, 동일 점수가 여럿일 경우, 순서대로 출력

## Inputs

| Variable Name | type        | meaning      |
| ------------- | ----------- | ------------ |
| answers       | Vector[Int] | Answer sheet |

## output

~~~scala
return Vecotor[Int] // highest score student numbers
~~~

## Conditions

* answer 
  * length: ~ 10 000
  * values: 1, 2, 3, 4, 5
* return value
  * if same score students exist ⇒ sort by their index number

## Test cases

| answers     | return  |
| ----------- | ------- |
| [1,2,3,4,5] | [1]     |
| [1,3,2,4,2] | [1,2,3] |

## Solution

각 학생별 찍는 패턴을 벡터로 저장. 해당 학생들을 하나의 벡터로 저장.

학생들 벡터에 map함수 적용, map안에서 answers map적용.

~~~scala
def solution(answers: Vector[Int]): Vector[Int] = {
  val students = Vector(
    Vector(1, 2, 3, 4, 5),
    Vector(2, 1, 2, 3, 2, 4, 2, 5),
    Vector(3, 3, 1, 1, 2, 2, 4, 4, 5, 5)
  )

  val scores = students.map(student => 
                            answers.zipWithIndex.map{case (answer, index) => 
                              if (answer == student(index%student.length)) 1 else 0
                            }.sum
                           ).zipWithIndex.sortBy{case (correct, index) => (-correct, index)}

  return scores.filter{case(score, idx) => score == scores(0)._1}
  .map{case(score, idx) => idx+1}
}
~~~



## Study from Implementation

* Iterable에 사용할 수 있는 sortBy라는 함수가 있다.
  * bracket 안에 먼저 적는 변수가 우선적으로 처리된다. 
  * 각 변수별로 reverse 적용 여부는 -를 다는 것으로 쉽게 해결될 수 있다. (아닌 케이스도 있을 수 있으니 주의)
* 벡터 안에 튜플 형태로 값이 저장된 경우
  * map, filter등의 함수로 값을 깔때
    * {중괄호를 사용하고} case (변수 1번 이름, 변수 2번 이름, ...) 이런식으로 적던지 아니면
    * (소괄호 열고) 변수이름 (eg. row) 적고 ⇒ row._1, 이런식으로 언더스코어 n번째로 처리해야한다. (이때는 컴퓨터 인덱스가 아니라 사람 서수이다. **!주의!**)
