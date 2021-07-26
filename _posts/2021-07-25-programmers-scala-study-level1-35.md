---

title: Programmers Scala Study (level 1.35)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 35. 직사각형 별찍기

## 문제 설명

행렬 입력된 숫자만큼 별(*)을 출력한다.

## Inputs

| Variable Name | type          | meaning             |
| ------------- | ------------- | ------------------- |
| args          | Array[String] | arguments(col, row) |

## output

~~~scala
return Vector[Long] // array of numbers
~~~

## Conditions

* n, m ≤ 1000

## Test cases

5 3

~~~
*****
*****
*****
~~~

## Solution

이런 기초적인게 맨뒤에 있네 ㅋㅋㅋ 

그냥 for loop 돌려야겠다.

~~~scala
def main(args: Array[String]) {
  val n = readLine().split(" ")
  val (a, b) = (n(0).toInt, n(1).toInt)

  for ( _ <- 1 to b) {
    for( _ <- 1 to a){
      print("*")
    }
    print("\n")
  }

}
~~~

### Study from Implementation
