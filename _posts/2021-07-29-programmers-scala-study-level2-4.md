---

title: Programmers Scala Study (level 2.4)

categories:
  - Programming Study
last_modified_at: 2021-07-29

tags: [programming, study, scala]

---

# 4. 행렬 테두리 회전하기

## 문제 설명

rows*columns 크기의 행렬.

(x1, y1, x2, y2)의 형태로 두개의 지점을 정하면 해당 사각형 테두리에 있는 숫자들을 시계방향으로 하나씩 shift 한다.

![rotation_example](/assets/post/programmers_2_4_ex.png)

이러한 쿼리를 모두 처리한 뒤에 위치가 변경된 숫자들 중 가장 작은 숫자를 어레이에 담아 리턴.

## Inputs

| Variable Name | type                | meaning                                              |
| ------------- | ------------------- | ---------------------------------------------------- |
| rows          | Int                 | matrix rows                                          |
| columns       | Int                 | matrix columns                                       |
| queries       | Vector[Vector[Int]] | query that shows 4 numbers to make box for rotation. |

## output

~~~scala
return Vector[Int] // changed numbers sorted by ascending order
~~~

## Conditions

* rows & columns: 2~100
* initial matrix is looks like (eg)
  * [1 2 3 4 5]
    [6 7 8 9 10]
    ...
* quries
  * length: 1~10 000
  * first applied first.
  * query
    * 1 ≤ x1 ≤ x2 ≤ rows
    * 1 ≤ y1 ≤ y2 ≤ columns

## Test cases

| rows  | columns | queries                                     | result         |
| ----- | ------- | ------------------------------------------- | -------------- |
| `6`   | `6`     | `[[2,2,5,4],[3,3,6,6],[5,1,6,3]]`           | `[8, 10, 25]`  |
| `3`   | `3`     | `[[1,1,2,2],[1,2,2,3],[2,1,3,2],[2,2,3,3]]` | `[1, 1, 5, 3]` |
| `100` | `97`    | `[[1,1,100,97]]`                            | [1]            |

## Solution

### Idea1

일단 초기 어레이 형태를 생성. queries에 map걸고 변환.

~~~scala
def updateMatrix(box: Vector[Int], matrix: Vector[Vector[Int]]): Vector[Vector[Int]] = {
  val start = (box(0)-1, box(1)-1)
  val end = (box(2)-1, box(3)-1)

  return matrix.zipWithIndex
  .map{case(row, row_idx) => 
    row.zipWithIndex
    .map{case(v, col_idx) => 
      if (row_idx == start._1 && start._2 < col_idx && col_idx <= end._2) {
        // top row (other than left corner) -> refers one left, same row
        matrix(row_idx)(col_idx-1)
      } else if (row_idx == end._1 && start._2 <= col_idx && col_idx < end._2) {
        // bottom row (other than right corner) -> refers one right, same row
        matrix(row_idx)(col_idx+1)
      } else if (col_idx == end._2 && start._1 < row_idx && row_idx <= end._1) {
        // right col (other than top corner) -> refers one top, same col
        matrix(row_idx-1)(col_idx)
      } else if (col_idx == start._2 && start._1 <= row_idx && row_idx < end._1) {
        // left col (other than bottom corner) -> refers one below, same col
        matrix(row_idx+1)(col_idx)
      } else v
    }
  }
}
def getDiffMin(box: Vector[Int], matrix: Vector[Vector[Int]]): Int = {
  val start = (box(0)-1, box(1)-1)
  val end = (box(2)-1, box(3)-1)
  val trans = matrix.transpose

  var arr = Vector[Int]()

  arr = arr.appendedAll(matrix(start._1).slice(start._2, end._2))
  arr = arr.appendedAll(matrix(end._1).slice(start._2+1, end._2+1))
  arr = arr.appendedAll(trans(end._2).slice(start._1, end._1))
  arr = arr.appendedAll(trans(start._2).slice(start._1+1, end._1+1))

  return arr.filter(v => v != -1).min
}
def solution(rows: Int, columns: Int, queries: Vector[Vector[Int]]): Vector[Int] = {
  var initMatrix = Vector.tabulate(rows, columns){ (i,j) => rows*i + j+1 }
  var convMatrix = Vector.tabulate(rows, columns){ (i,j) => rows*i + j+1 }
  var ans = Vector[Int]()

  for(query <- queries){
    // initMatrix = convMatrix
    convMatrix = updateMatrix(query, convMatrix)

    ans = ans :+ getDiffMin(query, 
                            convMatrix.zip(initMatrix)
                            .map{case(convRow, initRow) => 
                              convRow.zip(initRow)
                              .map{case(c, i) => if (c != i) c else -1}
                            }
                           )
  }
  return ans
}
~~~

제출 테스트에서 2개 빼고 다 틀린다... 로직이 틀린듯. 다시 풀자.

### Idea2

회전에 의해 위치가 바뀌었다. → 이문장을 잘 이해해야할 거 같다. 

가 아니라 최초에 메트릭스 생성을 잘못했다 ㅋㅋㅋㅋㅋ 아니 진짜 나 뭐해.

tabulate로 생성할때 rows x i + j +1이 아니라 columns x i + j + 1이다.

~~~scala
def solution(rows: Int, columns: Int, queries: Vector[Vector[Int]]): Vector[Int] = {
  var matrix = Vector.tabulate(rows, columns){ (i,j) => columns*i+j +1 }

  var smallest = Vector[Int]()
  for (query <- queries) {
    // var query = queries(0)
    var rotationTarget = Vector[Int]()

    var tmp = matrix
    val x1 = query(0) - 1
    val y1 = query(1) - 1
    val x2 = query(2) - 1
    val y2 = query(3) - 1

    for (c <- y1+1 to y2) {
      // x1 top row (other than left corner) -> refers one left, same row
      rotationTarget = rotationTarget:+matrix(x1)(c-1)
      tmp = tmp.updated(x1, tmp(x1).updated(c, matrix(x1)(c-1)))
    }
    for (c <- y1 to y2-1) {
      // x2 bottom row (other than right corner) -> refers one right, same row
      rotationTarget = rotationTarget:+matrix(x2)(c+1)
      tmp = tmp.updated(x2, tmp(x2).updated(c, matrix(x2)(c+1)))
    }
    for (r <- x1+1 to x2) {
      // y2 right col (other than top corner) -> refers one top, same col
      rotationTarget = rotationTarget:+matrix(r-1)(y2)
      tmp = tmp.updated(r, tmp(r).updated(y2, matrix(r-1)(y2)))
    }
    for (r <- x1 to x2-1) {
      // y1 left col (other than bottom corner) -> refers one below, same col
      rotationTarget = rotationTarget:+matrix(r+1)(y1)
      tmp = tmp.updated(r, tmp(r).updated(y1, matrix(r+1)(y1)))
    }
    smallest = smallest:+rotationTarget.min
    matrix = tmp
  }

  return smallest
}
~~~

### Idea3

기존의 코드에서 최초 행렬 생성만 수정해보자 → 아주 잘작동한다. 허허. 왜 제일 중요한 기본적인걸 확인안했을 까 ㅠㅠ



### Study from Implementation

- 벡터의 값을 변경하려면 무조건 updated 메소드를 사용해야한다.
  - 이게 생각보다 불편하다
- 벡터에 append하는 방법은
  - 벡터 :+ 단일값
  - 벡터.appendedAll(벡터 with 복수값)
