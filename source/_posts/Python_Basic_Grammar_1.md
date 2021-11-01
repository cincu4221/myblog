
파이썬(Python) 기본 문법 - 1
---

이 포스트는 필자의 정확한 파이썬 문법을 익히고 필요할때 찾아보기 위해 서술한 것이다. 

## Hello World

---
어떤 프로그래밍언어든 배우기 시작하면 출력하고 보는 `Hello world`, 파이썬에서는 다음과 같이 출력한다.
```python
print("Hello, world!")
```
Output:  
  
    Hello, world!
당연하게도 Hello, world 이외의 다른 문장이 들어가면 그대로 출력되며  
`print()` 에서 괄호 내부에 출력을 해주고싶은 변수나 문장을 입력하면 된다, 문장의 경우는 따옴표로 묶어줘야 출력이 된다.   

## 주석처리 

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

프로그래밍 언어마다 주석처리해주는 방법이 다르다, 파이썬 역시 그러하며 다음과 같이 주석처리한다.
```python
# 한줄을 주석처리하는 방법입니다.
"""
여러줄을
한번에 주석처리하는
방법입니다.
"""
print("Hello, world!")
```
Output:  
  
    Hello, world!
위처럼 작성하고 실행시키면 나머지 줄은 모두 주석처리되고 가장 아랫줄인 Hello, world만 출력이 되는걸 볼 수 있다.  

</div>
</details>


## 변수의 종류


---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

**변수**(Variable)는 (문자나 숫자 같은) 값을 담는 컨테이너로 값을 유지할 필요가 있을 때 사용한다. 여기에 담겨진 값은 다른 값으로 바꿀 수 있다. 변수는 마치 (사람이 쓰는 언어인) 자연어에서 대명사와 비슷한 역할을 한다. 

출처 : [생활코딩 - 변수](https://www.opentutorials.org/course/743/4673)   

다른 프로그래밍언어와 같이 파이썬 역시 다양한 변수의 종류(타입)가 있는데 이번 단락에서는 그것에 대해 알아보겠다.

### int타입 (정수형)
```python
num_int = 1
print(type(num_int))
```
변수에 값을 정수로 주고 그 변수의 타입을 알아본 예제, 출력을 하게되면 `<class 'int'>`가 줄력된다.

### float타입 (실수형)
```python
num_float = 0.2
print(type(num_float))
```
변수에 값을 실수로 주고 그 변수의 타입을 출력한 예제, 출력을 하게되면 `<class 'float'>`가 출력된다.

### bool타입 (논리형)
```python
bool_true = True
print(type(bool_true))
```
변수에 값을 논리타입(True or False)으로 주고 그 변수의 타입을 출력한 예제, 출력하면 `<class 'bool>`이 출력된다.

### None타입
```python
none_x = None
print(type(none_x))
```
`Null`을 나타내는 자료형이다, `None`라는 한가지 값만 가질 수 있다. (왜 필요한지는 아직 모르겠다)

</div>
</details>


## 사칙연산


---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

파이썬에서의 사칙연산은 일반적인 사칙연산과 같다.  
그리고 나눈후 정수의값만 구하는 `//`, 나머지를 구하는 `%`, 거듭제곱을 뜻하는 `**` 등의 연산자가 있다.
```python
a = 3
b = 2
print('a + b = ', a+b)
print('a - b = ', a-b)
print('a * b = ', a*b)
print('a / b = ', a/b)
print('a // b = ', a//b)
print('a % b = ', a%b)
print('a ** b = ', a**b)
```
Output:  
  
    a + b =  5
    a - b =  1
    a * b =  6
    a / b =  1.5
    a // b =  1
    a % b =  1
    a ** b =  9
위처럼 각각 계산이 된걸 알 수 있다.

### 정리하면 아래와 같다
|연산자|내용|
|:------:|:---:|
|+|두 변수의 합을 계산|
|-|두 변수의 차를 계산|
|*|두 변수의 곱을 계산|
|/|두 변수로 나눈 결과를 float 형으로 반환|
|//|두 변수로 나눈 결과에서 정수 부분만 취함|
|%|두 변수로 나눈 결과에서 나머지 값만 가져옴|
|**|i**j일 경우, i의 j만큼 제곱하여 계산 (예: 2 ** 4 = 24 = 16)|

</div>
</details>



## 논리형 연산자


---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

논리형 연산자에는 `and` 와 `or`이 있다.  
`and`연산자는 두 조건이 모두 참일때 `True`가 되며 `or`의 경우 두 조건중 하나라도 참일때 `True`가 된다.

### and연산자

```python
print(True and True)
print(True and False)
print(False and True)
print(False and False)
```
Output:  
  
    True
    False
    False
    False
위 결과처럼 두 조건 모두 참일때만 `True`를 반환한다.  
표로 나타내면 다음과 같다.  

|변수1|변수2|AND 연산결과|
|:------:|:---:|:---:|
|True|True|True|
|True|False|False|
|False|True|False|
|False|False|False|


### or 연산자
```python
print(True or True)
print(True or False)
print(False or True)
print(False or False)
```
Output:  
  
    True
    True
    True
    False
위 결과처럼 두 조건 중 하나만 참이라도 `True`를 반환한다.
표로 나타내면 다음과 같다.  

|변수1|변수2|AND 연산결과|
|:------:|:---:|:---:|
|True|True|True|
|True|False|True|
|False|True|True|
|False|False|False|

</div>
</details>


## 비교 연산자


---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">  

비교 연산자에는 `>`,`<`,`>=`,`<=`이 있다.
일단, 예제를 보자.
```python
print(4 > 3)
print(4 < 3)
print(4 >= 3)
print(4 <= 3)
```
Output:  
  
    True
    False
    True
    False
예제처럼 결과는 논리타입으로 출력된다.

</div>
</details>

## 문자열 연산

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">  

정수나 실수 논리타입뿐만 아니라 문자열도 연산이 가능하다.  
다만 문자열을 뒤에 덧붙이는`+`연산자, 문자열을 횟수만큼 반복해주는`*`연산자만 사용이 가능하다.  
```python
str1 = "Python "
str2 = "Editor "
print('str1 + str2 = ', str1 + str2)
```
Output:  
  
    Python Editor
`+`연산자의 경우 위처럼 문자열 두 개가 나란히 이어붙혀져 출력이 되며,
```python
greet = str1 + str2
print('greet * 3 = ', greet * 3)
```
Output:  
  
    Python Editor Python Editor Python Editor 
`*`연산자의 경우 변수에 담긴 문자열이 정해준 횟수만큼 반복되어 나열된다.
</div>
</details>

## 문자열 인덱싱

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

문자열이 있는경우 숫자을 통해 문자열에서 특정 문자만을 출력할 수 있는데 이를 `Indexing` 이라고 한다.  
`Hello world`이라는 문자열이 있다고 하자 그럼 문자열의 각 인덱스는 다음과 같다.  

|문자열|H|e|l|l|o| |w|o|r|l|d|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|인덱스|0|1|2|3|4|5|6|7|8|9|10|

이처럼 각 글자마다 인덱스가 배정되며 공백에도 인덱스가 배정된다.  
인덱스를 사용하면 다음과 같은 것도 가능하다.
```python
text_ex = "Hello world"
print(text_ex[2])
print(text_ex[6:10])
print(text_ex[2:11:2])
```
Output:  
  
    l
    worl
    lowrd
위 예제는 문자열을 담은 변수에 인덱싱을 한 것이다  
첫번째 줄은 인덱스'2'의 문자를 가져오는 것인데 인덱스는 0부터 시작하므로 (2번째가아닌)3번째인'l'을 출력한것이다.  
두번째 줄은 인덱스'6'부터 '9'까지(두번째인덱스-1)의 숫자를 가져오는 것이므로 'worl'이 출력되었다.  
세번째 줄은 인덱스'2'부터 '10'까지를 가져오되, 한칸씩 건너뛰고(세번째 숫자가 3이므로) 가져오는것이다.

</div>
</details>


## 리스트(list)

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

`리스트`는 여러개의 문자열, 변수, 숫자 등을 담을수 있는 자료구조이다.
리스트의 장점은 다음과 같다.
- 인덱스 번호로 빠른 접근이 가능하다.
- 데이터의 위치에 대해 직접적인 접근(Access)가 가능하다.
```python
fruit = [['apple', 'banana', 'cherry'], 123]
```
위가 리스트의 형태이다.  
리스트의 값은 기본적으로 인덱스가 배정된다 이때는
```python
print(fruit[0])
```
Output:  
  
    ['apple', 'banana', 'cherry']
위와 같은 형태로 나타낼 수 있으며 해당 인덱스의 요소가 리스트라면 리스트 전체를 출력한다.  

만약 위처럼 리스트가 중첩된 형태라면
```python
print(fruit[0][1])
```
Output:  
  
    banana
위처럼 출력이 가능하며 이때 리스트의 요소중 해당 인덱스의 요소가 출력된다.  
물론 이 때도 출력된 문자열에서 다음과 같이 문자열의 요소를 출력하는것도 가능하다.
```python
print(fruit[0][1][3])
```
Output:  
  
    a
위와같이 결과가 출력된다.

</div>
</details>


## 리스트값 수정, 추가, 삭제하기

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

리스트가 여러 요소들의 집합이다보니 리스트의 값에 변동이 필요할 때가 있다.  
리스트는 값의 수정, 추가, 삭제가 가능하므로 기능과 문법에 대해 알아둘 필요가 있다.

### 리스트 값 수정하기
```python
a = [0,1,2]
a[1] = "b"
print(a)
```
Output:  
  
    [0, 'b', 2]
별다른 문법없이 리스트의 인덱스에 값을 넣어주니 수정이 되는것을 알 수 있다.

### 리스트 값 추가하기
* ### append
```python
a = [100, 200, 300]
a.append(400)
print(a)

b = [500,600]
a.append(b)
print(a)
```
Output:  
  
    [100, 200, 300, 400]
    [100, 200, 300, 400, [500, 600]]
`리스트명.append(값)`을 통해서 리스트에 값을 추가할 수 있으며 한개의 값만 추가할 수 있다.  
리스트의 경우엔 한가지 값이며 추가할 경우 중첩된 리스트의 형태로 추가가 된다.  

* ### extend
`extend`는 `append`와 거의 같지만 다른점이 하나 있습니다.  
`append`는 인자(리스트, 튜플 등)를 주어도 인자 그대로를 리스트에 추가하지만,  
`extend`는 인자를 줄 경우 인자의 값 하나하나를 리스트에 추가한다.
```python
a = [2, 9, 3]
b = [1, 2, 3]
a.extend(b)
print(a)
```
Output:  
  
    [2, 9, 3, 1, 2, 3]
결과와 같이 `append`와 비교했을때 `extend`된 인자의 값 하나하나가 추가된걸 볼 수 있다.

* ### insert
`insert`는 입력해준 위치의 인덱스에 값을 추가해준다.
```python
a = [1,2,3]
print(a)
a.insert(1,'abc')
print(a)
```
Output:  
  
    [1,2,3]
    [1,'abc',2,3]


### 리스트 값 삭제하기
* ### remove
```python
a =[1,2,1,2]
#리스트의 첫번째 1이 삭제
a.remove(1)
print(a)
#리스트의 두번째 였던 1이 삭제
a.remove(3)
print(a)
```
Output:  
  
    [2, 1, 2]
    [2, 2]
`리스트명.remove()`는 괄호내의 값을 삭제한다.  
만약 값이 리스트내에서 중복될경우 가장 앞에 있는 값을 삭제한다.

* ### del
```python
a = [0,1,2,3,4,5,6,7,8,9]

# 1 삭제
del a[1]
print(a)

b = [0,1,2,3,4,5,6,7,8,9]
# 범위로 삭제
del b[1:3] #list는 항상 시작하는 index부터, 종료하는 n의 n-1까지의 범위를 잡아준다.
print(b)
```
Output:  
  
    [0, 2, 3, 4, 5, 6, 7, 8, 9]
    [0, 3, 4, 5, 6, 7, 8, 9]
`del 리스트명[인덱스]`는 리스트의 인덱스에 위치한 값을 삭제해준다.  
인덱스값에 범위를 주고싶다면 0:4 처럼 넣을수 있으며 이때는 0에서 3번째 값까지 삭제가 된다.

* ### pop
```python
a = [0,1,2,3,4]
r = a.pop(1)

print(a)
print(r)
```
Output:  
  
    [0, 2, 3, 4]
    1
`리스트명.pop()`은 괄호내의 값을 해당 리스트에서 끄집어낸다.

</div>
</details>

## 튜플(tuple)

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

`튜플`은 리스트와 비슷하게 여러개의 문자열, 변수, 숫자 등을 담을수 있는 **자료구조**이다.  
튜플과 리스트의 가장 차이점으로는 튜플은 값에대한 수정이 불가하다는 점이다.  
그렇다면 튜플은 무슨 장점이 있느냐 라고 반문할 수 있는데 리스트와 비교한 튜플의 장점은 다음과 같다.  
- 메모리 사용량이 적다.
- 생성 시간이 빠르다.
- 인덱스를 사용하여 튜플의 데이터에 접근하는 시간이 비교적 짧다.

튜플의 문법, 기본형태는 다음과 같다.

```python
tuple1 = (0) # 끝에 콤마(,)를 붙이지 않았을 때
tuple2 = (0,) # 끝에 콤마(,)를 붙여줬을 때
tuple3 = 0,1,2

print(tuple1)
print(tuple2)
print(tuple3)

print(type(tuple1)) # 콤마(,)를 붙여주지 않으면 튜플이 아닙니다.
print(type(tuple2)) # 콤마(,)를 붙여주어야 튜플 자료형 입니다.
print(type(tuple3)) # 여러개의 값 일경우 괄호를 없애주어도 튜플 자료형 입니다.
```
Output:  
  
    0
    (0,)
    (0, 1, 2)
    <class 'int'>
    <class 'tuple'>
    <class 'tuple'>
튜플을 생성할때 튜플이 되기위해서는 콤마(,)가 필수적이다.  
콤마를 작성하지 않으면 타입을 출력했을때 튜플이 아닌 입력한 변수형태로 출력이 된다.

튜플역시 리스트와 같이 인덱싱및 슬라이싱이 가능하다.

### 튜플의 연산
튜플도 연산이 가능한데, 더하거나 곱하는 `+`, `*` 연산자만 사용이 가능하다.
```python
t1 = (0,1,2,3,4)
t2 = ('a','b','c')
t3 = t1+t2
print(t3)
```
Output:  
  
    (0, 1, 2, 3, 4, 'a', 'b', 'c')
</div>
</details>

## 딕셔너리

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

딕셔너리는 키와 그에따른 값으로 구성되어있는 파이썬의 **자료구조**이다.  
```python
dic = {'teacher':'alice', 'class': 5, 'studentid': '15', 'list':[1,2,3]}

print(dic['teacher'])
print(dic['class'])
print(dic['list'])
```
Output:

    alice
    5
    [1, 2, 3]

`키`를 출력하면 그와 대응하는 `값`이 출력되는 자료구조이며 자료에 순서가 없는`논시퀀스 자료형`이다.

```python
a = {'name': 'bob', 'job': 'farmer', 'age': 35}
a.keys()
a.values()
```
Output:  
  
    dict_keys(['name', 'job', 'age'])
    dict_values(['bob', 'farmer', 35])
이렇게 키만 출력할수도, 값만 출력할수도 있다.

</div>
</details>

## 집합 연산자

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

파이썬에도 집합연산이 있고, 자료구조들의 합,교,차집합에 대한 연산을 할수 있다.  
기호는 `|`,`&`,`-`이며, 각각의 예시는 다음과 같다.
```python
a = {1,2,3,4}
b = {3,4,5,6}
print(a|b) 
print(a&b)
print(a-b)
```
Output:  
  
    {1, 2, 3, 4, 5, 6}
    {3, 4}
    {1, 2}

</div>
</details>

## if 조건문

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

**조건문**이란 작성자가 명시한 조건식의 결과인 `boolean`값이 참인지 거짓인지에 따라 달라지는 계산이나 상황을 수행하는 문장이다.
```python
a = -5

if a>5:
    print('a는 5이상입니다')

elif a > 0:
    print("a는 0초과, 5이하입니다")

else:
    print("a는 음수입니다")
```
Output:  
  
    a는 음수입니다.

조건식에는 기본적으로 조건식이 들어가지만 `True`나 `False`등의 직접적인 `bool`형 변수가 삽입될수도 있으며, `and`,`or` 등과 결합하여 여러가지의 조건식을 사용할수도 있다.

</div>
</details>

## 반복문 (for,while)

---
<details> 
<summary>접기 / 펼치기</summary>
<div markdown="1">

같은동작을 여러번 반복해야 할 때 같은코드를 여러번 적어넣는건 비효율적이다.
그럴때 반복문을 사용하면 훨씬 적은양의 코드로도 같은효과를 낼 수 있다.

* ### for문
* for문의 기본 구조
```python
for 변수 in 리스트(또는 튜플, 문자열) :
    수행할 문장1
    수행할 문장2
```
리스트나 튜플, 문자열의 첫 번째 요소부터 마지막 요소까지 차례로 변수에 대입되어 "수행할 문장1", "수행할 문장2" 등이 수행된다.
```python
a = ['1','2','3']
for i in a :
    print(i)
```
Output:  
  
    1
    2
    3

리스트 `a`의 첫번째 값인 1이 `i`에 대입되고 `print(i)`가 출력된다.  
다음엔 두번째 값인 2가 대입되고 출력된다.  
이것을 마지막 값까지 반복한다.

* ### while문
* while문의 기본 구조
```python
while <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    <수행할 문장3>
    ...
```
`while`문은 `for`보다는 간단하다. `while`, `조건문`, `실행문` 이 세개면 완성되기 때문이다.  
이러한 특성때문에 `while`문은 조건문을 거짓으로 만들어주는 문장이 없다면 무한실행된다. ~~프로그램 뻗는다~~  
간단한 예제를 보면 다음과 같다.
```python
i = 0
while i <= 5 :
    print("{}번째 반복입니다.".format(i))
    i += 1
```
Output:  
  
    0번째 반복입니다.
    1번째 반복입니다.
    2번째 반복입니다.
    3번째 반복입니다.
    4번째 반복입니다.
    5번째 반복입니다.
변수 `i`로 인해 자동으로 조건식이 `False`가 되면서 `while`문이 종료되는 모습이다.  
이렇듯 `while`문은 조건문을 거짓으로 만들어주는 무엇인가가 없다면 종료되지않는다.

</div>
</details>
