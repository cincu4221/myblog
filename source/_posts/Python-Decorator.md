---
title: 파이썬 데코레이터 (Python Decorator)  
date: 2021-12-07 17:04:31  
categories: 
- Python  

tags:  
- Python
- Decorator
- Function
---

## 데코레이터란?
___
파이썬으로된 소스코드들을 보면, 가끔 다음과 같은 구문을 볼 수 있다.  
```python
@decorator
def func()
    print("How to use Python")
```
본적은 있는것 같으나 어디에 어떻게 사용되는지 처음보는사람은 모를 수 있다.  
데코레이터는 함수를 수정하지 않은 상태에서 추가기능을 구현할 때 사용한다.  
일단 다음의 예시를 보자

```python
def func1():
    print("func1")

def func2():
    print("func2")

func1()
func2()
```
위 두개의 함수에 각각 시작부분과 끝부분을 표기하고싶다면 아래와 같이 함수 시작, 끝부분에 print를 따로 넣어주어야 한다.
```python
def func1():
    print("func1 start")
    print("func1")
    print("func1 end")

def func2():
    print("func2 start")
    print("func2")
    print("func2 end")

func1()
func2()
```
함수가 한개, 두개라면 부담이 되지않겠지만 만약 10개, 100개, 1000개의 함수가 있고 그것을 수정해야한다면 여간 귀찮은 일이 아닐것이다.  

이런 경우에 데코레이터를 사용하면 편리하다.  
바로 다음 예시를 보자
```python
def dec(func):
    def wrapper(func):
        print(func.__name__, "start")
        func()
        print(func.__name__, "end")
    return wrapper

def func1():
    print("func1")

def func2():
    print("func2")

dec_func1 = dec(func1)
dec_func1()
dec_func2 = dec(func2)
dec_func2()

'''
또는
dec(func1)()
dec(func2)()
'''
```
```
<Output>
func1 start
func1
func1 end
func2 start
func2
func2 end
```
위처럼 입력하게 될 경우 먼저 만들어졌던 dec 함수에 의해 func1, func2의 함수 출력부분에 시작과 끝을 나타내는 print가 같이 출력되게 할 수 있다.

위 코드에서 start 와 end 앞에 있는 func1,func2의 경우에는 함수의 이름이 출력되는것이고, 그 사이에 있는 func1,func2은 함수의 print 열이 출력된 것이다.


## @가 있는 데코레이터 사용하기
___
그런데 처음에 예시로 보았던 @로 시작하는 데코레이터는 어디에도 보이지 않는다.  
@를 사용하는 데코레이터는 어떻게 만드는 것일까?

@를 사용하는 데코레이터는 다음과 같이 작성한다.
```python
@dec
def func1():
    print("func1")
```
간결하게 적어서 이해가 어려울 수 있으니 이전 챕터의 가장 뒷부분 코드를 가져와 수정해보면 다음과 같다.
```python
def dec(func):
    def wrapper():
        print(func.__name__, "start")
        func()
        print(func.__name__, "end")
    return wrapper

@dec
def func1():
    print("func1")

@dec
def func2():
    print("func2")

func1()
func2()
```
결과는 같지만 무엇보다 출력부분이 매우 간결해졌다.  

만약 한개의 함수에 데코레이터 여러개를 사용해야한다면 다음과 같이 할 수 있다.
```python
@dec1
@dec2
@dec3
def func1():
    print("func1")
```
코드가 위와 같을 때 여러개의 데코레이터가 지정되며 이때 데코레이터가 실행되는 순서는 위에서 아래 순으로 실행된다.

마지막으로 데코레이터를 그림으로 표현하면 다음과 같다.

![데코레이터의 실행 과정](/images/Python_Decorator/python_decorator.png)

## Reference
https://bluese05.tistory.com/30