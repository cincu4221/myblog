---
title: NumPy 기본 다지기
date: 2021-11-06 12:06:27
tags:
- Python
- Numpy
---

## Numpy란 무엇인가?
![Numpy_Symbol](/images/Numpy_Symbol.png)  
`Numpy`는 상당부분 C언어로 작성된 파이썬 라이브러리이다. 기본적으로 `array`라는 자료를 생성하고 이를 바탕으로 색인, 처리, 연산 등을 하는 기능을 수행한다. 물론 C언어로 작성되었기 때문에 속도도 꽤나 빠른편이다.

## Numpy의 기본

### Numpy 불러오기

---
`Numpy`를 사용하기 위해서는 먼저 임포트시켜줘야 한다.
```python
import numpy as np
```
위처럼 입력하면 `Numpy`의 임포트가 된다. 뒤의 as np를 빼고 나머지만 입력해도 되지만, 앞으로 사용할 코드에서 조금 더 편히 사용하기 위하여(그리고 관례적으로) as np를 작성해 준다.

### Numpy배열 생성 및 둘러보기

---
Numpy는 기본적으로 `array`라는 자료구조를 사용하기때문에 배열을 생성하는 방법에 대해 먼저 알아두어야 한다.
```python
arr1 = [1,2,3]
my_array1 = np.array(arr1)
print(my_array1)
print(my_array1.shape)
```
Output:

    [1 2 3]
    (3,)

위의 출력 중 첫째줄은 `arr1`의 배열을 그대로 `my_arrary1`로 가져와 출력한 것이고, 둘째 줄은 가져온 배열의 길이를 `튜플`로 나타낸 것이다. 값 뒤에 콤마(,)가 붙어있는 이유는 값이 하나만 존재할 때, 튜플은 값 뒤에 콤마가 있어야 하기 때문이다.
 
<br><br>

---

다음은 2차원 배열일떄의 예제이다.
```python
my_array3 = np.array([[2,4,6],[8,10,12],[14,16,18],[20,22,24]])
print(my_array3)
print(my_array3.shape)
print(my_array3.dtype)
```
Output:

    [[ 2  4  6]
     [ 8 10 12]
     [14 16 18]
    [20 22 24]]
    (4, 3)
    int64
먼저 세개의 출력 중 첫번째로 `my_array3`의 값인 리스트들이 차례로 나열되며, 그 다음으로는 배열의 (행, 열)의 수, 마지막으로 배열내의 요소의 데이터타입을 출력한다.
<br><br><br>

---
마지막으로 3차원 배열일때의 예제이다.
```python
my_array5 = np.array([[[1, 2], [3, 4],[5, 6]], [[5, 6], [7, 8], [9, 10]]])
my_array5.shape
```
Output:

    (2, 3, 2)
세려는 양(또는 각각) 배열의 수가 대칭일때의 예제이다, 가장 바깥쪽의 배열부터 순서대로 배열의 수를 출력한다.  
그렇다면 대칭이 아니라면 어떻게 출력될까? 다음을 살펴보자

```python
my_array5 = np.array([[[1, 2], [3, 4], [5, 6, 7]], [[5, 6], [7, 8], [9, 10]]])
my_array5.shape
```
Output:

    (2, 3)
출력과 동시에 에러(위 출력창에서는 삭제함)가 뜨는데 추측하기론 양쪽 배열이 대칭이 아니기에 양 배열의 길이가 같은 두번째 항목까지는 출력되나 2와 3으로 갈리는 마지막 항목에서 출력이 안되는것 같다.  
확실하지않으니 참고만...



## Numpy의 기본 함수들

---
`Numpy`는 여러 함수들을 사용할수 있다, 하지만 함수의 종류가 너무 많기 때문에 이 챕터에서는 기본적인 함수들만 알아보도록 한다. 

* ### arange
---
`arange`는 배열을 만들어주는 함수이다.  
arange([시작],끝,[만큼 건너뜀])으로 작성 할 수 있으며 []안의 항목은 생략 할 수 있다.
```python
arrange_array = np.arange(3, 13, 2)
arrange_array
```
Output:  
  
    array([ 3,  5,  7,  9, 11])
3부터 시작해서 12(13-1)까지 출력하며 2씩 건너뛰는 배열을 생성하는 `arange`예제이다.


* ### zeros, ones
---
`zeros`와 `ones`는 0또는 1로 초기화된 `shape`* 차원의 `ndarray`** 배열 객체를 반환한다.  
두 함수 모두 객체 생성시 데이터 타입은 `float64`형식이다.
<br><br>
*shape : 행열의 차원  
**ndarray :  N차원의 배열객체. 기존파이썬과는 다르게 ndarray는 오직 같은 종류의 데이터만을 배열에 담을 수 있다.

```python
zeros_array = np.zeros((3,2))
print(zeros_array)
print("Data Type is:", zeros_array.dtype)
print("Data Shape is:", zeros_array.shape)
```
Output:  
  
    [[0. 0.]
     [0. 0.]
     [0. 0.]]
    Data Type is: float64
    Data Shape is: (3, 2)
순서대로 배열, 데이터 타입, 데이터의 차원을 출력한다.
<br><br>
```python
ones_array = np.ones((3,4), dtype='int32')
print(ones_array)
print("Data Type is:", ones_array.dtype)
print("Data Shape is:", ones_array.shape)
```
Output:  
  
    [[1 1 1 1]
     [1 1 1 1]
     [1 1 1 1]]
    Data Type is: int32
    Data Shape is: (3, 4)
같은 순서로 항목들을 출력했고 배열생성시 데이터 타입을 바꿀수 있음을 보여주는 예제이다.


* ### reshape

---
`reshape`는 구조를 재배열해주는 함수이다. `배열명.reshape(차원, 차원)`으로 사용할 수 있다.
```python
# 위에서 만들어진 3 x 4 배열의 ones_array를 reshape하여 2 x 6로 재배열
after_reshape = ones_array.reshape(2,6)
print(after_reshape)
print("Data Shape is:", after_reshape.shape)
```
Output:  
  
    [[1 1 1 1 1 1]
     [1 1 1 1 1 1]]
    Data Shape is: (2, 6)

`reshape`를 통해서 3x4 배열을 2x6으로 재배열 해준 가장 기본적인 예제이다.

재배열하려는 배열이 3x4 라면 3x4를 곱해서 나오는 값인 12의 인수들로 12의 결과가 나오는 배열((1,12), (2,6), (4,3))들로 바꿀 수 있으며, (2,2,3)등과 같은 3차원배열로도 재배열이 가능하다.

* ### reshape의 값에 -1을 넣는다면?

---
그렇다면 `reshape`의 괄호 차원값에 -1을 넣는다면 어떻게될까?
다음 결과를 보자.
```python
after_reshape2= ones_array.reshape(-1,6)
print(after_reshape2)
```
Output:  
  
    [[1 1 1 1 1 1]
     [1 1 1 1 1 1]]

-1을 작성한 곳에 12에서 나머지(두번째 값인 6)값을 보고 첫번째 값은 알아서 2로 지정이 된 것이다.  
<br><br>
다음은 값이 -1 하나일 때의 예제이다.
```python
after_reshape2= ones_array.reshape(-1)
print(after_reshape2)
```
Output:  
  
    [1 1 1 1 1 1 1 1 1 1 1 1]
결과와 같이 1차원 배열로 바뀐다. 하지만 (12)일뿐, 2차원 배열인 (1,12)과는 같지 않다.

## Numpy 인덱싱과 슬라이딩

---
`Numpy`의 배열에도 값을 추출 할 수 있게 인덱싱과 슬라이딩이 가능하다.
```python
my_array2 = np.arange(start=3,stop=30,step=3)
my_array2 = my_array2.reshape(3,3)

my_array2[1:3,:]
```
Output:  
  
    array([[12, 15, 18],
            [21, 24, 27]])
출력에서 첫번째 인자는 1에서 2(3-1)번째 까지의 배열을 출력하고, 두번째 인자인 :은 첫번째 인자에서 지목된 배열의 항목을 모두 출력하는 것이다.

## Numpy 정렬

---
여러 값이 모여있는 `array`인 만큼 정렬도 가능하다. 이 챕터에서는 오름,내림차순으로 정렬해주는 `sort()`, 값이 낮은 순서대로 인덱스를 배정해 배열을 출력해주는 `argsort()`가 있다.

* ### sort()

---
```python
height_arr = np.array([174, 165, 180, 182, 168])
sorted_height_arr = np.sort(height_arr)

print('Height Matrix: ', height_arr)
print('np.sort() Matrix: ', sorted_height_arr)
```
Output:  
  
    Height Matrix:  [174 165 180 182 168]
    np.sort() Matrix:  [165 168 174 180 182]
결과에서 보이다시피 `sort()`함수는 배열내의 값을 오름차순으로 정렬해준다.  
<br>

내림차순으로 정렬을 하고 싶다면 다음과 같이 하면 된다.

```python
desc_sorted_height_arr = np.sort(height_arr)[::-1]
print('np.sort()[::-1] : ', desc_sorted_height_arr)
```
Output:  
  
    np.sort()[::-1] :  [182 180 174 168 165]
위처럼 정렬을 할 때 `sort()`의 뒷부분에 `[::-1]`을 붙여주면 된다.

* ### argsort()

---
```python
fives = np.array([10, 5, 15, 20])
fives_order = fives.argsort()

print("The original data", fives)
print("The argsort(): ", fives_order)
print("The asending:", fives[fives_order])
```
Output:  
  
    The original data [10 5 15 20]
    The argsort():  [1 0 2 3]
    The asending: [ 5 10 15 20]
출력의 첫번째 줄은 가장 처음 입력했던 일반적인 배열이다.  
두번째 줄은 오름차순으로 인덱스를 매긴 배열이며,  
마지막은 두번째줄의 배열에 따라 첫번째줄의 결과인 배열을 정렬한 것이다.
