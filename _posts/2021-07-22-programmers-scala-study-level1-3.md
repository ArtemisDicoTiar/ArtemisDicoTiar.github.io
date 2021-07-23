---

layout: post

title: Programmers Scala Study (level 1.3)

date: 2021-07-22 14:27:00 +0100

description: Programmers coding study with programming language Scala. The difficulty selected is level 1.

tags: [programming, study, scala]

---

# 3. 체육복

## 문제 설명

도둑이 들어 체육복을 도난 당했다. 여벌의 체육복 있는 학생들이 도난 당한 친구들에게 빌려준다. (여벌 체육복이 있는 게 신기한데?) 

단, 학생들의 번호는 체격순으로 매겨져있기 때문에 바로 앞이나 바로 뒷 번호 학생만이 빌려줄수 있다.

체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 빌려서 최대한 많은 학생들이 수업을 듣게 하려한다.

이때 수업을 들을 수 있는 최대 학생수는?

 ## Inputs

| Variable Name | type        | meaning                                   |
| ------------- | ----------- | ----------------------------------------- |
| n             | Int         | Number of students                        |
| lost          | Vector[Int] | indices of student who lost their clothes |
| reserve       | Vector[Int] | indices of student who has extra clothes  |

## output

~~~scala
return Int // Maximum number of students who can listen to the PE class
~~~



## Conditions

* n
  * 2~30
* lost
  * length: 1~n 
  * no duplicate numbers
* reserve
  * length: 1~n
  * no duplicate numbers
* ! there is a possibility that student who has extra lost their clothes.
  * if this is the case, this student can lend their clothes

## Test cases

| n    | lost   | reserve   | return |
| ---- | ------ | --------- | ------ |
| 5    | [2, 4] | [1, 3, 5] | 5      |
| 5    | [2, 4] | [3]       | 4      |
| 3    | [3]    | [1]       | 2      |

## Solution

일단 len(reserve) - len(lost) 을 계산했을떄 이게 양수면 n명만큼의 학생들이 수업을 들을 "수도" 있다.

만약 음수라면 n + (위에서 계산한 값) 만큼의 학생들만큼만 수업을 들을 "가능성"이 있다.



당장 생각나는 풀이는 그냥 쭉 iterate하면서 내가 lost인지 확인하고 lost면 주변에 여유분 있는 지 확인하고.

이었는데 굳이 그럴필요 없을 거 같다 그냥 lost만 봐도 될듯.

1. lost만 보는 데 주변에 reserve가 있는 지 확인.
   1. 주변에 있다면 그 주변을 reserve에서 pop.
   2. ! 단, 양쪽 다 있으면 앞쪽으로 뽑자. (lost가 sorted되어 있어서 앞쪽을 뽑아야 뒤에서 필요할 때 제공해줄 수 았다.)

이 로직이면 해결될거 같은데...?

### 1차 solution

~~~scala
	def getSupport(n: Int, idx: Int, reserve: Vector[Int]): Vector[Int] = {
        if (idx == 1) { // init
            return reserve.filterNot(_ == idx+1)
        } else if (idx == n) { // last
            return reserve.filterNot(_ == idx-1)
        } else {
            if (reserve.exists(v => v == idx-1)) return reserve.filterNot(_ == idx-1)
            if (reserve.exists(v => v == idx+1)) return reserve.filterNot(_ == idx+1)
        }
        return reserve
    }
    
    def solution(n: Int, lost: Vector[Int], reserve: Vector[Int]): Int = {
        var reliefedNum = reserve.length - lost.foldLeft(reserve)((reserve, lostStudent) => getSupport(n, lostStudent, reserve)).length
        
        return n - (lost.length - reliefedNum)
    }
~~~

체육복을 빌릴수 있는 학생 수를 "getSupport"함수를 lost.foldLeft를 이용해서 적용해서 구했다. (조건에 충족되는 학생수만 도출됨.)

도움 받은 학생수를 도난 당한 학생수에서 빼면 수업을 들을 수 없는 학생수가 나온다. 전체 학생수인 n에서 빼면 수업들을 수 있는 학생수 나옴.



인데... 정확도에서 75%가 나온다. 분명 edge case를 handling 못했다. 

인줄 알았는데 문제 어디에도 lost, reserve가 정렬되서 제공된다는 말이 없다. 

ㅋㅋㅋㅋㅋㅋ 문제를 꼼꼼히 읽어야겠다. 일단 sorted적용.

### 2차 solution

단순히 lost.sorted.foldLeft로 바꿨다. 왜냐면 어차피 reserve 에서 있는 지 없는 지를 확인하기 때문에.

여전히 틀린다. 뭐가 문제지

Test case 추가

5, [2, 3, 4], [3, 4, 5] → 4

아 맞다... 가지고 있는 애가 도난당하는 거 깜빡했다. → 이거로 각 벡터 정리하는 로직 추가하고 다시하면 될듯

### 3차 solution

여분 가지고 있는 애가 도난당한 경우 로직 추가하니깐 해결! :)

~~~scala
def getSupport(n: Int, idx: Int, reserve: Vector[Int]): Vector[Int] = {
  if (idx == 1) { // init
    return reserve.filterNot(_ == idx+1)
  } else if (idx == n) { // last
    return reserve.filterNot(_ == idx-1)
  } else {
    if (reserve.exists(v => v == idx-1)) return reserve.filterNot(_ == idx-1)
    if (reserve.exists(v => v == idx+1)) return reserve.filterNot(_ == idx+1)
  }
  return reserve
}

def solution(n: Int, lost: Vector[Int], reserve: Vector[Int]): Int = {
  var updated_lost = lost.filterNot(idx => reserve.exists(v => v == idx))
  var updated_reserve = reserve.filterNot(idx => lost.exists(v => v == idx))

  var reliefedNum = updated_reserve.length - updated_lost.sorted.foldLeft(updated_reserve)((updated_reserve, lostStudent) => getSupport(n, lostStudent, updated_reserve)).length

  return n - (updated_lost.length - reliefedNum)
}
~~~



### 추가 수정! Idea from Others

~~~scala
var updated_lost = lost.filterNot(idx => reserve.exists(v => v == idx))
var updated_reserve = reserve.filterNot(idx => lost.exists(v => v == idx))
~~~

이 두개를 필터링 하지 않고 set의 diff로 구하는 방법도 있다.

~~~scala
var updated_lost = lost.diff(reserve)
var updated_reserve = reserve.diff(lost)
~~~



## Study from Implementation

* Vector 등의 Iterable의 길이는 "Iterable".length로 구한다.
* Iterable의 정렬은 "Iterable".sorted다.
* Iterable에서 조건에 해당되는, 되지 않는 애들만 거르려면 filter, filterNot을 사용하면 된다. (bracket안에는 조건 넣기, Boolean이 output인 함수를 넣으면 된다.)

