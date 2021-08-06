---
title: Programmers Scala Study (level 2.6)

categories:
  - Programming Study
last_modified_at: 2021-08-05

tags: [programming, study, scala]

---

# 6. 거리두기 확인하기 (2021 카카오 채용연계형 인턴십 문제)

## 문제 설명

대기실은 5개, 각 대기실은 5 by 5의 크기이다.

거리두기를 위해 각 응시자 끼리의 맨해튼 거리가 2 초과를 유지해야한다.

응시자 사이가 파티션으로 막혀있는 경우 허용.

각 대기실이 거리두기를 지키고 있으면 1, 한명이라도 지키지 않고 있으면 0을 어레이에 담아 해당 어레이를 리턴.

## Inputs

| Variable Name | type                   | meaning                                    |
| ------------- | ---------------------- | ------------------------------------------ |
| places        | Vector[Vector[String]] | 2d array shows how people sit in the room. |

## output

~~~scala
return Vector[Int] // array that shows whether the room is safe from distancing or not.
~~~

## Conditions

* places
  * row
    * length: 5
    * each row shows structure of the room
  * col
    * length: 5
  * values
    * P: People
    * O: Empty table
    * X: Partition
* input room size: 5*5
* return
  * 1d array with 5 elements
  * order of return value follows the order of the room on places array
  * value
    * 1: well distanced
    * 0: not distancing each other

## Test cases

| places                                                       | result          |
| ------------------------------------------------------------ | --------------- |
| `[["POOOP", "OXXOX", "OPXPX", "OOXOX", "POXXP"], ["POOPX", "OXPXP", "PXXXO", "OXXXO", "OOOPP"], ["PXOPX", "OXOXP", "OXPOX", "OXXOP", "PXPOX"], ["OOOXX", "XOOOX", "OOOXX", "OXOOX", "OOOOO"], ["PXPXP", "XPXPX", "PXPXP", "XPXPX", "PXPXP"]]` | [1, 0, 1, 1, 1] |

## Solution

맨해튼 거리 2 초과가 되기 위해서는 같은 행, 열에 위치해있다면 최소한 다음과 같은 구조, 거리여야한다.

~~~
P ? ? P
~~~

대각선으로 위치한다면 최소 다음과 같아야한다.

~~~
P ? 
? ? 
? P 
~~~

### Idea1

파티션의 좌표, 사람의 좌표를 일단 뽑아보자. → 함수로 만들어서 뽑아냈다

사람들의 좌표를 combination(2)로 뽑아낸뒤에 각 좌표간의 맨해튼 거리르 측정, 2 이하인 경우만 벡터로 리턴.

해당 사람들 좌표에 남은 사람들의 좌표를 보고 두 좌표 사이에 파티션이 있는 지 확인. 있으면 벡터에서 없앰.

벡터가 다 비워지면 1. 아니면 0

~~~scala
object Solution {
  def getCoordinates(of: Char, places: Vector[Vector[String]]): Vector[Vector[(Int, Int)]] = {
    places.map(place => 
               place.zipWithIndex
               .map{case(row, row_idx) => 
                 row.zipWithIndex
                 .map{case(v, col_idx) => 
                   if (v == of) (row_idx, col_idx) else null}
                 .filter(v => v != null)
               }.flatten
              )
  }
  def getReqPartitions(v1:(Int, Int), v2:(Int, Int)): Vector[(Int, Int)] = {
    val Xs = if (v1._1 < v2._1) (v1._1, v2._1) else (v2._1, v1._1) 
    val Ys = if (v1._2 < v2._2) (v1._2, v2._2)  else (v2._2, v1._2)
    val total_idx = (Xs._1 to Xs._2).map(e1 => (Ys._1 to Ys._2).map(e2 => (e1, e2))).toVector.flatten
    total_idx.filter(v => v != v1 && v != v2)
  }
  def solution(places: Vector[Vector[String]]): Vector[Int] = {
    val partitions_room = getCoordinates('X', places)
    val people_room = getCoordinates('P', places)
    val people_not_distancing = people_room.map(people =>
                                                people.combinations(2).toVector
                                                .map(v => 
                                                     if ((v(0)._1-v(1)._1).abs + (v(0)._2-v(1)._2).abs <= 2) v else null
                                                    )
                                                .filter(v => v != null)
                                               )
    val reqPartitions = people_not_distancing.map(room => 
                                                  room.map(pp => getReqPartitions(pp(0), pp(1))).flatten
                                                 )

    return reqPartitions.zip(partitions_room)
    .map{case(req, exs) => req.filter(v => !exs.contains(v))}
    .map(v => if (v.length == 0) 1 else 0)
  }
}
~~~

반은 맞고 반은 틀린다 ㅠ

### Idea2 

이게 문제네 ㅋㅋㅋㅋ (https://programmers.co.kr/questions/19267)

required partition을 계산할때 2보다 작은 경우 (바로 옆에 붙은 경우) → 파티션이 없어도 된다고 계산하네... ㅠ

파티션 계산에서 없어도 된다고 계산되면 강제로 (-1, -1) 주입해야겠다 (애초에 2보다 큰 경우는 다 걸렀으니 바로 옆에 붙은 건 파티션 여부와 상관없이 무조건 안되는 거라서)

getReqPartitions 함수 업데이트 했더니 성공! XD

~~~scala
def getReqPartitions(v1:(Int, Int), v2:(Int, Int)): Vector[(Int, Int)] = {
  val Xs = if (v1._1 < v2._1) (v1._1, v2._1) else (v2._1, v1._1) 
  val Ys = if (v1._2 < v2._2) (v1._2, v2._2)  else (v2._2, v1._2)
  var total_idx = (Xs._1 to Xs._2).map(e1 => (Ys._1 to Ys._2).map(e2 => (e1, e2))).toVector.flatten.filter(v => v != v1 && v != v2)
  if (total_idx.length == 0) total_idx = total_idx :+ (-1, -1)
  return total_idx
}
~~~



### Study from Implementation

- 맨해튼 거리가 뭐지...?
  - 두 테이블 T1, T2가 행렬 (r1, c1), (r2, c2)에 각각 위치하고 있다면, T1, T2 사이의 맨해튼 거리는 |r1 - r2| + |c1 - c2| 입니다.
