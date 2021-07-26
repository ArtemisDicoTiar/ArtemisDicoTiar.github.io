---

title: Programmers Scala Study (level 1.33)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 33. 행렬의 덧셈

## 문제 설명

두 행렬의 element wise addition을 한 결과를 리턴.

## Inputs

| Variable Name | type                | meaning  |
| ------------- | ------------------- | -------- |
| arr1          | Vector[Vector[Int]] | matrix 1 |
| arr2          | Vector[Vector[Int]] | matrix 2 |

## output

~~~scala
return Vector[Vector[Int]] // element-wise added.
~~~

## Conditions

* arr1 arr2
  * row and column length < 500

## Test cases

| arr1          | arr2          | return        |
| ------------- | ------------- | ------------- |
| [[1,2],[2,3]] | [[3,4],[5,6]] | [[4,6],[7,9]] |
| [[1],[2]]     | [[3],[4]]     | [[4],[6]]     |

## Solution

두 행렬 zip후 map → 각 row별로 zip 후 map → element1+ element2

~~~scala
def solution(arr1: Vector[Vector[Int]], arr2: Vector[Vector[Int]]): Vector[Vector[Int]] = {
  arr1.zip(arr2).map(row => 
                     row._1.zip(row._2).map(cell => 
                                            cell._1+cell._2)
                    )
}
~~~

### Study from Implementation
