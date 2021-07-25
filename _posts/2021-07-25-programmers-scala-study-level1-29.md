---

title: Programmers Scala Study (level 1.29)

categories:
  - Programming Study
last_modified_at: 2021-07-25

tags: [programming, study, scala]

---

# 29. 콜라츠 추측

## 문제 설명

```
1-1. 입력된 수가 짝수라면 2로 나눕니다. 
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.
```

## Inputs

| Variable Name | type | meaning      |
| ------------- | ---- | ------------ |
| num           | Int  | input number |

## output

~~~scala
return Int // collatzed process count
~~~

## Conditions

* num
  * 1~8000000

## Test cases

| n      | result |
| ------ | ------ |
| 6      | 8      |
| 16     | 4      |
| 626331 | -1     |

## Solution

여태 안쓰려고 했던 반복문을 결국 써야하네 while 루프 쓰면 될듯.

~~~scala
def solution(num: Int): Int = {
  var count = 0
  var n = num.toLong
  while (n != 1 && count < 500) {
    if (n % 2 == 0) n = n/2 
    else n = n*3 + 1
    count += 1
  }
  if (count == 500) return -1
  return count
}
~~~

### Study from Implementation

