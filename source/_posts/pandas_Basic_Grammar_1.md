---
title: pandas 기본 문법
date: 2021-11-02 16:14:46
categories: 
- pandas
tags: 
- Python
- pandas
---



## DataFrame 생성 방법


---



* ### list이용
```python

import pandas as pd

frame = pd.DataFrame([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
frame
```



<details> 
<summary>출력</summary>
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>

</details>


* ### Dictionary 이용
```python
import pandas as pd

data = {
    'age' : [20,39,41],
    'height' : [176, 182, 180],
    'weight' : [73, 78, 69]
}
indexName = ['사람1', '사람2', '사람3']

frame = pd.DataFrame(data, index = indexName)
frame
```


<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>사람1</th>
      <td>20</td>
      <td>176</td>
      <td>73</td>
    </tr>
    <tr>
      <th>사람2</th>
      <td>39</td>
      <td>182</td>
      <td>78</td>
    </tr>
    <tr>
      <th>사람3</th>
      <td>41</td>
      <td>180</td>
      <td>69</td>
    </tr>
  </tbody>
</table>
</div>

</details>


## Sample Dataset 가져오기


---



위처럼 직접 `DataFrame`을 만드는 것이 아닌 제공하는 `Dataset`을 직접 가져오는 방법도 있다.  
`Dataset`을 가져오는 방법은 다음과 같다.

1. [Dataset Github](https://github.com/mwaskom/seaborn-data)에 접속하고 가져오고싶은 데이터셋을 고른다.
2. 예를들어 `flights.csv` 를 가져오고 싶다면
```python
import seaborn as sns
flights = sns.load_dataset("flights") #여기까지가 가져오기
flights.head(5) # 다섯번째 행의 데이터까지만 출력
flights["year"] # 'year'열만 출력
```
위와 같이 제공되는 데이터셋을 가져올 수 있다.




## DataFrame 조회 방법

---



### 기본적인 조회 방법
`DataFrame`의 기본적인 조회 방법은 다음과 같다.

* #### .head()

---




```python
# 위에서 가져온 데이터셋 flights를 사용
flights.head() # 데이터프레임의 가장 첫부분부터 표시
```


<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>month</th>
      <th>passengers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1949</td>
      <td>Jan</td>
      <td>112</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>Feb</td>
      <td>118</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1949</td>
      <td>Mar</td>
      <td>132</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1949</td>
      <td>Apr</td>
      <td>129</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1949</td>
      <td>May</td>
      <td>121</td>
    </tr>
  </tbody>
</table>
</div>

</details>


이 때 `.head()`의 괄호 안에 숫자가 있다면 그 수의 개수만큼 데이터가 출력된다.



* #### .tail()

---




```python
flights.tail() #데이터프레임의 가장 뒷부분부터 표시
```


<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>month</th>
      <th>passengers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>139</th>
      <td>1960</td>
      <td>Aug</td>
      <td>606</td>
    </tr>
    <tr>
      <th>140</th>
      <td>1960</td>
      <td>Sep</td>
      <td>508</td>
    </tr>
    <tr>
      <th>141</th>
      <td>1960</td>
      <td>Oct</td>
      <td>461</td>
    </tr>
    <tr>
      <th>142</th>
      <td>1960</td>
      <td>Nov</td>
      <td>390</td>
    </tr>
    <tr>
      <th>143</th>
      <td>1960</td>
      <td>Dec</td>
      <td>432</td>
    </tr>
  </tbody>
</table>
</div>

</details>


`.tail()`역시 마찬가지로 괄호안에 숫자가 있다면 수의 개수만큼 데이터가 출력된다.



* #### .index 

---



데이터프레임의 인덱스를 표시하는 방법도 있다.




```python
flights.index
```




    RangeIndex(start=0, stop=144, step=1)



### 열(Column) 조회 방법


```python
#열(Column) 조회
print ("* 열 조회 - 1")
print (frame['age'])
print ("* 열 조회 - 2")
print(frame.age)

#특정 열의 특정 값을 조회하고 싶을때
print("* 특정 열 의 특정 값 조회")
print(frame['age'][1])
print(frame.height[2])
```
<details> 
<summary>출력</summary>

    * 열 조회 - 1
    사람1    20
    사람2    39
    사람3    41
    Name: age, dtype: int64
    * 열 조회 - 2
    사람1    20
    사람2    39
    사람3    41
    Name: age, dtype: int64
    * 특정 열 의 특정 값 조회
    39
    180

</details>

### 행(Row) 조회

행 조회는 열 조회와 조금 다르게 `loc`와 `iloc`를 사용해서 조회 할 수 있다.  
여기서 `loc`는 사람이 읽을 수 있는 라벨 값으로 특정 값들을 골라오는 방법이고,  
`iloc`는 행이나 칼럼의 순서를 나타내는 정수로 특정 값을 추출하는 방법이다.


```python
#행(Row) 조회 (loc)
print("* loc 특정 행 조회")
print(frame.loc['사람1'])

# print(frame.loc[0]) - 조건이 정수이므로 조회 불가
```

    * 특정 행 조회
    age        20
    height    176
    weight     73
    Name: 사람1, dtype: int64
    loc를 Seq로 조회할 경우
    


```python
#행(Row) 조회 (iloc)
print("* iloc 특정 행 조회")
print(frame.iloc[0])

# print(frame.iloc['사람1']) - 조건이 정수가 아니므로 조회 불가
```
<details> 
<summary>출력</summary>

    * iloc 특정 행 조회
    age        20
    height    176
    weight     73
    Name: 사람1, dtype: int64

</details>

## DataFrame 수정 방법


---



### 열(Column) 추가하기

gender 라는 컬럼을 추가합니다.


```python
frame_add_col = pd .DataFrame(frame,columns= ['age','height','weight','gender'])
frame_add_col
```


<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>사람1</th>
      <td>20</td>
      <td>176</td>
      <td>73</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>사람2</th>
      <td>39</td>
      <td>182</td>
      <td>78</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>사람3</th>
      <td>41</td>
      <td>180</td>
      <td>69</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


</details>

컬럼이 추가되었고 어떠한 값도 넣어주지 않았으므로 NaN 값이 출력되고있다.  
이제 데이터를 입력해준다.


```python
frame_add_col['gender'] = ['male', 'male', 'female']
frame_add_col
```


<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>사람1</th>
      <td>20</td>
      <td>176</td>
      <td>73</td>
      <td>male</td>
    </tr>
    <tr>
      <th>사람2</th>
      <td>39</td>
      <td>182</td>
      <td>78</td>
      <td>male</td>
    </tr>
    <tr>
      <th>사람3</th>
      <td>41</td>
      <td>180</td>
      <td>69</td>
      <td>female</td>
    </tr>
  </tbody>
</table>
</div>

</details>


### 행(Row) 추가하기


```python
frame_add_index = frame_add_col.copy()
frame_add_index.loc['사람4'] = [31, 158, 48, 'female']
frame_add_index
```



<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>사람1</th>
      <td>20</td>
      <td>176</td>
      <td>73</td>
      <td>male</td>
    </tr>
    <tr>
      <th>사람2</th>
      <td>39</td>
      <td>182</td>
      <td>78</td>
      <td>male</td>
    </tr>
    <tr>
      <th>사람3</th>
      <td>41</td>
      <td>180</td>
      <td>69</td>
      <td>female</td>
    </tr>
    <tr>
      <th>사람4</th>
      <td>31</td>
      <td>158</td>
      <td>48</td>
      <td>female</td>
    </tr>
  </tbody>
</table>
</div>

</details>


### 행, 열 삭제하기

drop 메소드를 사용하면 행 또는 열을 삭제할 수 있다.  
axis 값은 행이면'0', 열이면 '1'로 지정해주면 된다.


```python
print('remove age column')
frame_add_col.drop("height", axis=1)
```

    remove age column
    


<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>사람1</th>
      <td>20</td>
      <td>73</td>
      <td>male</td>
    </tr>
    <tr>
      <th>사람2</th>
      <td>39</td>
      <td>78</td>
      <td>male</td>
    </tr>
    <tr>
      <th>사람3</th>
      <td>41</td>
      <td>69</td>
      <td>female</td>
    </tr>
  </tbody>
</table>
</div>

</details>


그러나 이 경우 기존에 있던 `frame_add_col`에서 삭제되는게 아니라 삭제된 상태의 프레임을 리턴해준 것이다.  
그러므로 기존 프레임에 적용하기 위해서 `inplace = True` 옵션을 추가로 주어야 한다.


```python
frame_add_index.drop('사람2', axis=0, inplace = True)
frame_add_index
```


<details> 
<summary>출력</summary>

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>height</th>
      <th>weight</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>사람1</th>
      <td>20</td>
      <td>176</td>
      <td>73</td>
      <td>male</td>
    </tr>
    <tr>
      <th>사람3</th>
      <td>41</td>
      <td>180</td>
      <td>69</td>
      <td>female</td>
    </tr>
    <tr>
      <th>사람4</th>
      <td>31</td>
      <td>158</td>
      <td>48</td>
      <td>female</td>
    </tr>
  </tbody>
</table>
</div>

</details>


참조 : https://hong-sam.tistory.com/100
