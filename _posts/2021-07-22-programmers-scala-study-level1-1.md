---

layout: post

title: Programmers Scala Study (level 1.1)

date: 2021-07-22 14:27:00 +0100

description: Programmers coding study with programming language Scala. The difficulty selected is level 1.

tags: [programming, study, scala]

---

# 1. 로또의 최고 순위와 최저 순위

## 문제 설명

로또는 45개의 숫자에서 6개를 뽑아 몇개가 일치하는 지에 따라 순위를 정하는 방식의 복권이다.

eg.

|  순위   | 당첨 내용                  |
| :-----: | -------------------------- |
|    1    | 6개 숫자 모두 일치         |
|    2    | 5개 숫자가 일치            |
|    3    | 4개의 숫자가 일치          |
|    4    | 3개의 숫자가 일치          |
|    5    | 2개의 숫자가 일치          |
| 6(Fail) | 1개 혹은 0개의 숫자가 일치 |

문제상황에서 동생이 자신의 로또 일부분에 낙서를 해서 못 알아보게 되었다고 한다.

(*알아볼수 없는 숫자는 0으로 표시되어 있다.*)

그래서 알아볼수 있는 숫자들로 자신의 최고 점수와 최저 점수를 알아보려고 한다.

## inputs

| Variable Name | Type                | Meaning              |
| ------------- | ------------------- | -------------------- |
| lottos        | (array) Vector[Int] | 구매한 로또의 숫자들 |
| win_nums      | (array) Vector[Int] | 당첨 번호들          |

## output

~~~Scala
return Vector[Int, Int] // Max winning rank, Min winning rank
~~~

## 조건 (Condition)

* lottos
  * length: 6
  * values: 0 ~ 45
    * 0: unrecognisable Number
    * Other than 0 cannot be repeated.
    * The array may not be sorted.
* win_nums
  * length: 6
  * values: 1 ~ 45
  * The numbers are not repeated.
  * The array may not be sorted.
* 일치 여부에서 순서와 상관없다

## Test Cases

| lottos                | win_nums                 | result |
| --------------------- | ------------------------ | ------ |
| [44, 1, 0, 0, 31, 25] | [31, 10, 45, 1, 6, 19]   | [3, 5] |
| [0, 0, 0, 0, 0, 0]    | [38, 19, 20, 40, 15, 25] | [1, 6] |
| [45, 4, 35, 20, 3, 9] | [20, 9, 3, 45, 4, 35]    | [1, 1] |

## Solution

최저 점수는 알아볼수 없는 숫자도 틀렸다고 가정. → 알아볼수 있는 숫자들로만 매칭된 개수 확인

최고 점수는 알아볼수 없는 숫자들도 모두 맞췄다고 가정 → 최저 점수 매칭 + 알아볼수 없는 숫자



### Study from Implementation

* How to check "num in array"

파이썬은 A in B_list 하면 B_list에 A가 있는 지를 Bool로 알려준다. 스칼라는 어떻게 해야하나

Vector에 exists라는 함수가 있다. 파라미터로 찾을 값을 넣으면 Boolean으로 반환한다. 아래와 같은 형태로 작성하면 된다.

~~~scala
win_nums.exists(v => v == 31)
~~~

각 값의 존재 여부를 map함수랑 위에서 알게된 exist함수를 엮어서 짜보자

~~~scala
win_nums.map(num => lottos.exists(lotto => lotto == num))
~~~



### final solution code

0개와 1개 매칭을 하나로 묶어야해서 조건문을 추가했다.

~~~scala
def solution(lottos: Vector[Int], win_nums: Vector[Int]): Vector[Int] = {
        var unknown_count = lottos.count(_ == 0)
        var match_count = win_nums.map(num => lottos.exists(lotto => lotto == num))
                                  .count(_ == true)
        
        var max_rank = if ((unknown_count+match_count) == 0) 6 else 7-(unknown_count+match_count)
        var min_rank = if (match_count == 0) 6 else 7-(match_count)
        
        return Vector[Int](max_rank, min_rank)
    }
~~~