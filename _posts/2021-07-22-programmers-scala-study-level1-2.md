---

layout: post

title: Programmers Scala Study (level 1.2)

date: 2021-07-22 14:27:00 +0100

description: Programmers coding study with programming language Scala. The difficulty selected is level 1.

tags: [programming, study, scala]

---

# 2. 숫자 문자열과 영단어

## 문제 설명

영어와 숫자의 조합으로 적힌 단어를 숫자로 변환

## inputs

| Variable Name | type   | Meaning                               |
| ------------- | ------ | ------------------------------------- |
| s             | String | 영어로 쓰인 숫자와 숫자의 조합 문자열 |

## output

~~~scala
return Int // s -> converted to all number
~~~

## Condition

* s
  * lenght: 1~50
  * never starts with "Zero" or "0"
  * The string only given that can be converted to 1~2,000,000,000 integer.

## Test cases

| s                  | result |
| ------------------ | ------ |
| "one4seveneight"   | 1478   |
| "23four5six7"      | 234567 |
| "2three45sixseven" | 234567 |
| "123"              | 123    |



## Solution

map string → int ⇒ join

스트링에서 영어로 적힌 내용을 숫자로 매핑

결과로 나온 매핑을 join

* 문제점: 단어 구분을 어떻게 하면 되려나

### Study from implementation

* converting "Integer" → Int 하려면
  * "Integer".toInt하면 된다.
* 문자열에서 단어 찾아서 바꾸려면
  * string.replace(찾는 거, 바꿀거) 혹은 string.replaceAll(찾는 거, 바꿀거)하면 된다.



### final solution code

~~~scala
def solution(s: String): Int = {
        return s.replaceAll("one", "1")
                .replaceAll("two", "2")
                .replaceAll("three", "3")
                .replaceAll("four", "4")
                .replaceAll("five", "5")
                .replaceAll("six", "6")
                .replaceAll("seven", "7")
                .replaceAll("eight", "8")
                .replaceAll("nine", "9")
                .replaceAll("zero", "0")
                .toInt
    }
~~~

### 신박한 solution from 다른사람들의 solution

테이블을 리스트로 만든 다음에 해당 인덱스가 각 문자열의 값이 되게 함.

리스트를 iterate하며 s문자열에서 해당 단어를 단어가 있는 인덱스로 변환.

리스트를 iterate하는 거기때문에 각 리스트 안에 변환된 문자열이 생성되는 거 같다. 

그래서 각 문자열을 변환하고 foldLeft해서 변환된 문자열을 새롭게 변환. 

~~~scala
def solution(s: String): Int = {
        val table  = List("zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine")
        val answer = table.zipWithIndex.foldLeft(s)((s, index) => s.replace(index._1, index._2.toString)).toInt
        return answer
    }
~~~

(zipWithIndex는 파이썬에서 쓰던 zip을 인덱스와 함께 한거 같고.. foldLeft는 위에서 설명한게 맞는 건가?)

#### foldLeft(variable)

definition:

~~~scala
def foldLeft[B](z: B)(op: (B, A) ⇒ B): B
~~~

Iterable을 iterate하는데 z에 들어온 변수에 op를 적용시켜 나온 결과를 z에 들어온 변수에 다시 넣는다?

(op는 z에 들어온 변수 타입과 동일한 결과를 리턴..?)



위 식을 이해하기 위해서 어떤식으로 작성되는 지 찾아보니 이 한줄이 제일 적당한거 같다.

~~~scala
def calculator(x:Int, y:Int)(f:(Int, Int) => Int) = f(x,y)
~~~

calculator라는 함수는 x와 y라는 정수형 변수 두개를 받는다. (def calculator(x: Int, y: Int))

해당 함수는 적용시킬 함수 f를 받아 X, Y변수를 이용해 결과를 도출하는 데 (= f(x, y))

적용시킬 함수는 두개의 Int를 받아 하나의 Int를 리턴해야한다. (f: (Int, Int) ⇒ Int)



자 이제 뭐가 뭔지 대충 이해했으니 foldLeft는 결국

B, A타입 두개의 변수 두개를 받은 뒤 B타입의 결과를 리턴한다는 거고.

그 타입은 input파라미터로 받는 z와 동일한 타입이고

foldLeft의 동작은 파이썬의 reduce와 동일한거 같다.
