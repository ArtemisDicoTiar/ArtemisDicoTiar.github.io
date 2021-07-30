---

title: Programmers Scala Study (level 2.3)

categories:
  - Programming Study
last_modified_at: 2021-07-29

tags: [programming, study, scala]

---

# 3. 기능개발

## 문제 설명

새로운 기능 개발을 진행하고 있다. 이때 기능 개발이 100%가 되어야 서비스에 적용될 수 있다.

각 기능 개발의 현 진행상황과 속도가 다르다.

각 기능별 어레이가 개발현상황, 속도, 두개가 주어진다.

이때 앞선 기능 개발이 완료되어야 기능 배포가 가능하다.

각 배포 스테이지별 몇개 기능이 배포되는 지 어레이로 리턴.

## Inputs

| Variable Name | type        | meaning                          |
| ------------- | ----------- | -------------------------------- |
| progresses    | Vector[Int] | current progress                 |
| speeds        | Vector[Int] | each feature's development speed |

## output

~~~scala
return Vector[Int] // deployable features on every stage.
~~~

## Conditions

* progresses & speeds
  * length: ~100
  * progress - values: <100 (cannot be given as 100% → this means the feature is already developed)
  * speeds - values: ≤ 100
  * deploy/day only (at the end of day.)
    * eg. current progress: 95%, speed: 4%/day → 2days later deployable.

## Test cases

| progresses               | speeds                 | return    |
| ------------------------ | ---------------------- | --------- |
| [93, 30, 55]             | [1, 30, 5]             | [2, 1]    |
| [95, 90, 99, 99, 80, 99] | [1, 1, 1, 1, 1, 1]     | [1, 3, 2] |
| [40, 93, 30, 55, 60, 65] | [60, 1, 30, 5 , 10, 7] | [1,2,3]   |
| [5, 5, 5]                | [21, 25, 20]           | [3]       |
| [20, 99, 93, 30, 55, 10] | [5, 10, 1, 1, 30, 5]   | [3, 3]    |

## Solution

### Idea1

일단, progresses랑 speeds zip해서 개발완료까지 필요한 day를 측정.

앞에서부터 돌면서 최대값을 업데이트하면서 최대값보다 작으면 카운터 돌림.

최대값이 업데이트되면 카운터를 어레이에 담고, 카운터를 초기화.

~~~scala
def solution(progresses: Vector[Int], speeds: Vector[Int]): Vector[Int] = {
  var count = 1
  var counts = Vector[Int]()
  progresses.zip(speeds)
  .map{case(progress, speed) => math.ceil((100-progress) / speed)}
  .reduce((cur, nex) => 
          if (cur > nex){
            count+=1
            cur
          } else {
            counts = counts:+count
            count=1
            nex
          })

  return counts:+count
}
~~~

실패... 63.6% (4개 실패)

뭐가 문제일까... math.ceil적용할때 타입 변환안했네 일단 이거부터 변환해보자. 안되네

파이썬 로직을 보자... 모르겠다 뭘 풀어놓은 거지 여기에..

### Idea2

테스트 케이스를 추가했다.

[5, 5, 5], [21, 25, 20] → [5, 4, 5] 이 케이스를 자꾸 틀리는 데 이유가 

~~~scala
if (cur > nex){
~~~

이 로직으로 인해 소요 일수가 같은 경우 같은 타임에 배포된다는 것을 고려되지 않았다.

~~~scala
if (cur >= nex){
~~~

로 변경.

끝.

~~~scala
def getDevDates(progress: Int, speed: Int): Int = {
  return if ((100-progress) % speed == 0) (100-progress) / speed
  else ((100-progress) / speed) + 1
}
def solution(progresses: Vector[Int], speeds: Vector[Int]): Vector[Int] = {
  var count = 1
  var counts = Vector[Int]()
  progresses.zip(speeds)
  .map{case(progress, speed) => getDevDates(progress, speed)}
  .reduce((cur, nex) => 
          if (cur >= nex){
            count+=1
            cur
          } else {
            counts = counts:+count
            count=1
            nex
          })

  return counts:+count
}
~~~

### Study from Implementation

- 리듀스 함수는 파이썬에서 처럼 쓰면 된다.
- 에로우 함수에 길게 로직을 쳐도 된다. 
  - 다만 마지막 줄에는 메소드 적용된 함수의 리턴값을 return없이 쓰면 된다.
