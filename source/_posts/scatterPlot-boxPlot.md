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

산점도, 산포도<sup>scatter plot</sup>는 직교좌표계를 잉요해 좌표상의 점들을 표시함으로써 두 개 변수 간의 관계를 나타내는 그래프 방법이다.  
도표 위에  두 변수 X와 Y값이 만나는 지점을 표시한 그림. 이 그림을 통해 두 변수 사이의 관계를 알 수 있다.
<br><br><br>

### 언제 사용되는가??

---

산점도는 다음의 경우에 사용된다.
1. 두 종류의 데이터의 관계를 파악할때, 즉, 양의 상관관계, 음의 상관관계, 관계없음 등의 관계를 파악한다.
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

## 박스플롯 (box plot)

### 박스플롯이란??



## References

https://hogni.tistory.com/84  
[마커 모양 변경](https://plotly.com/python/marker-style/)



