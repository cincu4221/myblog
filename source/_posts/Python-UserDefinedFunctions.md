---
title: 파이썬(Python) 사용자 지정 함수
date: 2021-11-10 15:12:27
categories: 
- Python

tags: 
- Python
- Function
---

## 사용자 지정 함수란?

---
파이썬에서(다른프로그래밍 언어, 스크립트 언어에서도) 함수란, 소프르웨어에서 특정 동작을 수행하는 일정 코드부분을 의미한다.

하나의 큰 프로그램을 여러부분으로 나누어주기 때문에 같은 함수를 여러 상황에서 여러차례 호출할 수 있고, 일부분을 수정하기 쉽다는 장점을 지닌다.  

파이썬에서는 미리 정의 되어있는 built in 함수(내장함수)가 있고. 또, 사용자가 필요에 의해 정의를 한 사용자 지정 함수가 존재한다.

## 파이썬에서의 함수 모형

---

### 파이썬 함수의 기본 모형
```python
def 함수명() :
    실행문
    실행문
    ...
```
이와 같은 구조인데 함수를 정의하는 `def`뒤에 함수명이 오고 소괄호`()`를 붙인 다음 콜론`:`을 붙여주고, 다음줄에 원하는 실행문을 들여쓰기하여 사용하면 된다.

```python
def func() :
    print('python function')
```
위는 기본 모형을 응용하여 함수를 정의한 것이다. 이는 입력값도, 반환값도 없는 함수이며 값이 있는 함수에 대해서는 후술하겠다.

그러나 위 코드는 함수를 정의한 것이지 사용을 한 것이 아니다. 그렇기 때문에 함수를 사용하기 위해서는 함수의 사용법을 알아야 한다.

```python
def func() :
    print('python function')

#함수 호출
func()
```
<details> 
<summary>Output</summary>

```python
python function
```

</details>

`func()`함수는 입력값이 없기때문에 호출시에 입력값을 넣어주지 않고 괄호만 입력해 준다.
<br><br><br>

### 입력값만 있는 함수

---

```python
def func2(a) :
    print('입력한 문자는 ' + a + ' 입니다.')

func2("비행기")
func2("자동차")
func2("파이썬")
```

<details> 
<summary>Output</summary>

```python
입력한 문자는 비행기 입니다.
입력한 문자는 자동차 입니다.
입력한 문자는 파이썬 입니다.
```
</details>

`func2()`함수의 입력값이 a 에 입력되어 출력 된 것을 볼 수 있다.
<br><br><br>

### 리턴값만 있는 함수

---

```python
def func3() :
    return "12345"

print(func3())
```
<details> 
<summary>Output</summary>

```python
12345
```

</details>

`func3()`의 값이 리턴되어 `print()`를 통해 출력된 것을 알 수 있다.
<br><br><br>

### 입력,리턴값이 모두 있는 함수

---

```python
def func4(a, b) :
    return a + b

print(func4(10,20))
```
<details> 
<summary>Output</summary>

```python
30
```

</details>

a,b의 입력값을 더하는 함수에 10,20의 값을 주었더니 예상대로 30이 출력 되었다. 
<br><br><br>

### 기본 인자 값

---

입력이 있는 함수를 여러 곳에 사용할 때 반복되는 값에 대해서는 기본적인 값을 지정할 수 있다.  
기본값은 `입력 = 값`의 형태로 작성된다.

```python
def func_b(a,b,c=5) :
    return a*b+c

print(func_b(2,3,10))
print(func_b(2,3))
```
<details> 
<summary>Output</summary>

```python
16
11
```

</details>

출력에서처럼 기본값이 주어진 c 인자에 별다른 값을 넣지 않으면 기본값 5로 계산되어 10이들어간 결과보다 5가 낮아지게 된다.

이렇게 기본 인자를 줄 때는 주의 할 점이 한 가지 있는데 바로 인자의 순서에 맞게 넣어주어야 한다는 것과, 기본값과 입력값이 없으면 에러가 난다는 것이다.  
다음 예시를 보자.

```python
def func_b2(a,b=5,c) :
    return a*b+c

print(func_b2(2,3))
```
위와 같이 값을 주게 된다면 어떨까?  
b에 기본값이 있으니 a와 c에 각각 2와 3이 입력된다고 생각한 사람도 있을 것이다.  
그러나 이 생각은 적어도 사용자 지정 함수에서는 옳지 않다.  

이 코드가 불가능한 데에는 두 가지 이유가 있다.  

첫 번째로는 a에는 2가 들어가는 것이 맞겠지만, b에 기본값이 있더라도 두 번째 입력값 자리에 3을 넣게 되는 순간 그 숫자는 b에 입력되기 때문에 결국엔 기본값이 없는 c는 어떠한 값도 입력받지 못하게 되기 때문이고,

두 번째 이유로는 c의 인자에 기본값이 없음에도 앞에 있는 b의 인자에 기본값이 있으므로 아예 성립할 수 없는 코드이다.
그러므로 기본값을 부여받은 인자는 항상 뒤에 배치해야 한다.
<br><br><br>

### 키워드 인자

---

키워드 인자는 함수를 정의할때 인자에 키워드를 부여하고 함수를 호출할 때 `키워드=값`의 형태로 넣어줄 수 있는 인자이다.  
그냥 인자에 값을 넣어주는것과 뭐가 다르냐?라는 의문이 들 수도 있다.  
다음 예시를 보자.
```python
def score(kim=100, lee=100, park=100, choi=100) :
    print('score = kim :', kim, 'lee :',lee, 'park :',park, 'choi :',choi)

score(park= 50)
```

<details> 
<summary>Output</summary>

```
score = kim : 100 lee : 100 park : 50 choi : 100
```
</details>

이렇게 중간의 인자만 `키워드=값`의 형태로 입력해 값을 변경해 줄 수 있다.  
예제처럼 여러 기본값이 있고 그중 몇 가지의 기본값만 바꿔 주어야 할 때 용이하게 쓸 수 있다.

### Arbitrary Argument Lists (임의 인자 리스트)

---

Arbitrary Argument Lists는, 여러인자를 함수에 잔달하는 방법들중 하나이다.

함수내부에서 이 인자들은 튜플로 감싸져있으며 이는`*args`<sup>arguments</sup> 생성자를 사용하여 정의 된다.
```python
def avg_score(*numbers) :
    s = 0
    count = 0
    for i in numbers:
        s += i
        count += 1
    return s / count

print('국어와 수학점수의 평균은{}점 입니다'.format(avg_score(95, 87)))
print('입력된 숫자들의 평균은{} 입니다.'.format(avg_score(42,63,45,32,48)))
```
<details> 
<summary>Output</summary>

```
국어와 수학점수의 평균은91.0점 입니다
입력된 숫자들의 평균은46.0 입니다.
```
</details>

위 코드에서는 `*args`를 `*numbers`로 대체했다.  
이처럼 함수를 호출 할 때에 숫자를 몇가지를 넣어도 사용이 가능하다.
<br><br><br>

### Lambda 함수

---

우리가 앞에서 배웠던 대로 사용자 지정 함수를 정의하고 사용하여 평균을 구하라고 한다면 아마 다음과 같을것이다.
```python
def avg(x,y):
    return(x + y) / 2
print(avg(5,13))

>> 9.0
```

그러나 파이썬은 Lambda함수를 통해서 이 코드를  더욱 짧게 줄일수 있다.
```python
print((lambda x,y: (x + y)/2)(5,13))

>> 9.0
```
그러나 배우는 입장인 내 눈으로 단점을 찾아보자면 함수인데 정의를 하는 부분이 따로 없다 보니, 출력할 일이 여러 번 생긴다면 번거로워 질 것 같다.  
그러니 앞으로 호출 횟수에 따라 적다면 람다 함수를, 많다면 기본적인 사용자 지정 함수를 사용하는 방식이 좋을 듯하다.
<br><br><br>

## References
* [https://djangojeng-e.github.io](https://djangojeng-e.github.io/2020/11/08/Python-%EA%B8%B0%EC%B4%88-17%ED%8E%B8-%EC%82%AC%EC%9A%A9%EC%9E%90-%EC%A0%95%EC%9D%98-%ED%95%A8%EC%88%98/)
