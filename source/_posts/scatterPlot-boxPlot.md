---
title: 산점도(scatter plot)와 박스플롯(box plot)
date: 2021-11-12 12:26:10
categories: 
- Data Visualization

tags: 
- Data Visualization
- Python
---

## 산점도(scatter plot)
### 산점도란?

---
![산점도](/images/Scatterplot_boxplot/Scatter_plot.png)  

산점도, 산포도<sup>scatter plot</sup>는 직교좌표계를 이용해 좌표상의 점들을 표시함으로써 두 개 변수 간의 관계를 나타내는 그래프 방법이다.  
도표 위에  두 변수 X와 Y값이 만나는 지점을 표시한 그림. 이 그림을 통해 두 변수 사이의 관계를 알 수 있다. 
<br><br><br>

### 언제 사용되는가??  

---

산점도는 다음의 경우에 사용된다.
1. 두 종류의 데이터의 관계를 파악할때. 즉, 양의 상관관계, 음의 상관관계, 관계없음 등의 관계를 파악한다.
2. 산점도의 작성으로 한 변수에 대한 결과의 영향조사를 한다.
<br><br><br>

### Plotly로 산점도 작성하기

---

* #### 데이터 임포트 및 데이터셋 생성
```python
import numpy as np
import pandas as pd
# plotly 라이브러리 불러오기
import plotly.offline as po
import plotly.graph_objs as go

# 임의의 숫자로 이루어진 2열,100행의 데이터프레임 생성
df1 = pd.DataFrame(np.random.randint(0, 100, (100, 2)), columns=['A', 'B'])
df2 = pd.DataFrame(np.random.randint(0, 100, (100, 2)), columns=['A', 'B'])
```

* #### 하나의 산점도 그리기

```python
trace1 = go.Scatter(x=df1['A'], y=df1['B'], mode='markers')
data = [trace1]
pyo.iplot(data)
```

<details> 
<summary>Output</summary>

![](/images/Scatterplot_boxplot/Scatter_plot-1.png)  

df1이 그대로 산점도로 출력된 모습이다.

</details>

* #### 두 개 이상의 산점도 그리기

```python
trace1 = go.Scatter(x=df1['A'], y=df1['B'], mode='markers')
trace2 = go.Scatter(x=df2['A'], y=df2['B'], mode='markers')
data = [trace1, trace2]
pyo.iplot(data)
```

<details> 
<summary>Output</summary>

![](/images/Scatterplot_boxplot/Scatter_plot-2.png)  

df1과 df2가 한 도표 내에 산점도로 출력된 모습이다.
이렇게 다른 데이터를 표시하고 싶을때에는 출력코드에 새로운 데이터값을 넣어주기만 하면 된다.

</details>

* #### 마커 모양 변경하기

```python
trace1 = go.Scatter(x=df1['A'], y=df1['B'], mode='markers', marker=dict(size=7, color='#D90B0B', symbol=20))
trace2 = go.Scatter(x=df2['A'], y=df2['B'], mode='markers', marker=dict(size=7, color='#F24444', symbol=23))
data = [trace1, trace2]
pyo.iplot(data)
```
<details> 
<summary>Output</summary>

![](/images/Scatterplot_boxplot/Scatter_plot-3.png)  

그림처럼 마커의 모양을 변경 할 수 있다.
`color`옵션은 헥스코드와 rgb값 모두 가능하며, 모양의 경우 매우 다양하므로 포스팅 최하단에 링크를 첨부한다. 

</details>
<br><br><br>

## 박스플롯 (box plot)

### 박스플롯이란??

---

![박스플롯](/images/Scatterplot_boxplot/box_plot.png)  

'박스플롯'<sup>box plot</sup>,또는 '상자 수염 그림'은 수치적 자료를 나타내는 그래프이다. 이 그래프는 가공하지 않은 자료 그대로를 이용하여 그린 것이 아니라, 자료로부터 얻어낸 통계량인 '5가지 요약 수치'<sup>five-number summary</sup> 를 가지고 그린다. 이 때 5갸지 요약 수치란 최솟값, 제 1사분위(Q<sub>1</sub>),제 2사분위(Q<sub>2</sub>), 제 3사분위(Q<sub>3</sub>), 최댓값을 일컫는 말이다. 히스토그램과는 다르게 집단이 여러개인 경우에도 한 공간에 수월하게 나타낼수 있다.
<br><br><br>

### 언제 사용되는가??

---
박스 플롯을 사용하는 이유는 데이터가 매우 많을때 모든 데이터를 한눈에 확인하기 어려우니 그림을 이용해 데이터 집합의 범위와 중앙값을 빠르게 확인 할 수 있는 목적으로 사용한다.  
또한, 통계적으로 이상치<sup>outlier</sup>가 있는지도 확인이 가능하다.
<br><br><br>

### 박스플롯의 구성

---

박스플롯을 처음 접한다면 박스플롯을 어떻게 해석해야 하는지 난해할수 있다.  
다음 그림에서 박스플롯의 각 구성이 무엇을 의미하는지 간단하게 알아보자.  
![박스플롯의 구성](/images/Scatterplot_boxplot/box_plot-1.png)  
각 요소들을 설명하면 다음과 같다.  

|요소|설명|
|:---:|:---:|
|이상치(outlier)|최소값보다 작은데이터 또는 최대값보다 큰 데이터가 이상치에 해당한다|
|최대값(upper whisker)|'중앙값 + 1.5 × IQR'보다 작은 데이터 중 가장 큰 값 |
|최소값(lower whisker)|'중앙값 - 1.5 × IQR'보다 큰 데이터 중 가장 작은 값 |
|IQR(Inter Quartile Range)|제3사분위수 - 제1사분위수<br>실수 값 분포에서 1사분위수(Q<sub>1</sub>)와 3사분위수(Q<sub>3</sub>)를 뜻하고 이 3사분위수와 1사분위수의 차이(Q<sub>3</sub> - Q<sub>1</sub>)를 IQR라고 한다.|
|중앙값|박스내부의 가로선, 용어 그대로 중앙값이다|
|whisker|상자의 상하로 뻗어있는 선|

<br><br><br>


### Plotly로 박스플롯 작성하기

---

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt


df3 = pd.DataFrame(np.random.randint(0, 100, (100, 2)), columns=['A', 'B']) #임의로 수 생성

plt.figure(figsize=(8,7)) # 크기 지정
boxplot = df3.boxplot(column=['B']) # df3의 'B'컬럼을 박스플롯으로 생성
plt.yticks(np.arange(0,101,step=5)) # 박스플롯이 그려질 범위 지정
plt.show()
```

<details> 
<summary>Output</summary>

![](/images/Scatterplot_boxplot/box_plot-2.png)  
위처럼 임의로 생성된 데이터프레임을 이용해 박스플롯을 만들 수 있다.

</details>

<br><br><br>





## References

[산점도 그리기](https://hogni.tistory.com/84)  
[산점도 마커 모양](https://plotly.com/python/marker-style/)  
[위키백과 - 산점도](https://ko.wikipedia.org/wiki/%EC%82%B0%EC%A0%90%EB%8F%84)  
[위키백과 - 상자 수염 그림](https://ko.wikipedia.org/wiki/%EC%83%81%EC%9E%90_%EC%88%98%EC%97%BC_%EA%B7%B8%EB%A6%BC)  
[박스플롯 및 요소 설명](https://codedragon.tistory.com/7012)
