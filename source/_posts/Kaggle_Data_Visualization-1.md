---
title: 캐글 데이터 시각화 해석-1
date: 2021-11-08 14:50:50
tags:
- Kaggle
- Data Visualization
---

<details> 
<summary>임포트 및 데이터프레임 추가</summary>

```python
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
```


```python
from plotly.offline import plot, iplot, init_notebook_mode
init_notebook_mode(connected=True)
```


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from warnings import filterwarnings
filterwarnings('ignore')

colors = ['#B1EDED','#B1B2ED','#1DE7ED','#1DA5ED','#1D50ED','#16548E']

df = pd.read_csv('../input/kaggle-survey-2021/kaggle_survey_2021_responses.csv')
df.head()
```

</details> 

## 원 그래프 해석

---

```python
fig = go.Figure( data=[ # 그래프의 형태를 나타내는 함수
                            go.Pie( # 원그래프 
                                    labels = df['Q2'][1:].value_counts().index, # 값에 붙일 이름 - df['Q2'][1:].value_counts()의 인덱스
                                   values = df['Q2'][1:].value_counts().values, # 나타낼 값 - df['Q2'][1:].value_counts()의 값
                                    textinfo = 'label+percent')]) # 그래프 항목당 나타낼 텍스트 (여기서는 항목명, 비율)
fig.update_traces( 
                    marker=dict(colors=colors[2:])) # 그래프를 어떤 색으로 표현할 것인지
fig.update_layout( # 그래프의 레이아웃 설정
                    title_text='Gender Distribution', # 그래프의 제목
                    showlegend=False) # 범례표시여부
fig.show()
```

<details> 
<summary>그래프</summary>

![원 그래프](/images/Kaggle_Data_Visualization-1/Kaggle_Data_Visualization-1.png)  

<details> 
<summary>코드 해석</summary>

```python
fig = go.Figure(data=[
                        go.Pie(
                                labels = df['Q2'][1:].value_counts().index,
                                values = df['Q2'][1:].value_counts().values,
                                textinfo = 'label+percent'
                              )])
```
`fig = go.Figure(data=[`   
-> 그래프의 기본적인 틀을 설정하는 함수이고, `fig`에 데이터를 부여해준다.  

`go.Pie(`  
-> 그래프의 형태가 파이모양(원그래프)임을 의미한다.  

`labels = df['Q2'][1:].value_counts().index`  
-> 그래프로 표현될 값에 붙일 이름이다. 이 코드에서는 ***'df'의 'Q2'열에 있는 데이터의 '1번인덱스(질문열을 제외하기 위함) 행부터 마지막까지' 카운트하고 값에따라 분류했을 때의 인덱스열*** 인 것이다.  

`values = df['Q2'][1:].value_counts().values`  
-> 그래프로 표현될 값이다. 이 코드에서는 ***'df'의 'Q2'열에 있는 데이터의 '1번인덱스 행부터 마지막까지' 카운트하고 값에따라 분류했을 때의 값(각 값을 카운트한 값)*** 이다.  

`textinfo = 'label+percent'`  
-> 그래프에 표시된 항목에 나타낼 텍스트를 설정한다. 이 코드에서는 항목명(label)과 비율(percent)을 나타낸다.  
<br><br>
```python
fig.update_traces( 
                    marker=dict(colors=colors[2:])) # 그래프를 어떤 색으로 표현할 것인가를 설정
fig.update_layout( # 그래프의 부가정보 설정
                    title_text='Gender Distribution', # 그래프 제목
                    showlegend=False) # 범례표시여부
fig.show()
```
`fig.update_traces(`  
-> 추가바람  

`marker=dict(colors=colors[2:]))`  
-> 그래프의 색상을 설정한다. 이 코드에서는 위에서 설정된 `colors` 리스트에서 2번 인덱스부터 순서대로 사용한다.  

`fig.update_layout(`  
-> 그래프의 부가정보를 설정한다.  

`title_text='Gender Distribution'`  
-> 그래프의 제목을 설정한다.  

`showlegend=False)`  
-> 범례의 표기여부를 결정한다. 이 코드에서는 `False`이므로 범례가 표기되지 않는다.  

`fig.show()`  
-> 화면에 그래프를 표시하는 기능을한다. 몇몇에디터에서는 자동으로 표시되기때문에 호출할 필요가 없는 경우가 있다.  


</details>

</details>

## 막대그래프 해석

---

```python
man = df[df['Q2'] == 'Man']['Q1'].value_counts() # 성별이 남성[df['Q2'] == 'Man']인 행에서 나이['Q1']의 값을 카운트하여 시리즈로 만듦.
woman = df[df['Q2'] == 'Woman']['Q1'].value_counts() # 성별이 여성[df['Q2'] == 'Woman']인 행에서 나이['Q1']의 값을 카운트하여 시리즈로 만듦.
textonbar_man = [ # list comprehension = [(변수를 활용한 값) for (사용할 변수 이름) in (순회 할 수 있는 값)]
                    round((m/(m+w))*100, 1) for m, w in zip(man.values, woman.values)] # for문을 사용하여 round함수의 계산을 하고 textonbar_man에 저장
textonbar_woman = [ # list comprehension
                    round((w/(m+w))*100, 1) for m, w in zip(man.values, woman.values)]

# go = graph_objects
fig = go.Figure(data=[ 
                        go.Bar( # 막대그래프
                                name='Man', # 그래프로 나타낼 항목
                                x=man.index, # x축에 man의 인덱스
                                y=man.values, # y축에 man의 값
                                text=textonbar_man, # 막대의 값을 작성해줄 텍스트
                                marker_color=colors[2]), #막대 색
                        go.Bar(
                                name='Woman', 
                                x=woman.index, 
                                y=woman.values, 
                                text=textonbar_woman, 
                                marker_color=colors[3])
])
fig.update_traces(
                    texttemplate='%{text:.3s}%', # fig(print(fig)로 출력가능)내부의 text 인자를 차례대로 출력 (그래프의 위의 텍스트를 표현)
                    textposition='inside') # 그래프상에서 값의 위치
fig.update_layout(
                    barmode='stack', # 막대의 형태
                    title_text='Age distribution by gender', # 그래프 제목
                    xaxis_title='Age', # x축 제목
                    yaxis_title='Counts') # y축 제목
fig.show()
```
<details> 
<summary>그래프</summary>

![막대 그래프](/images/Kaggle_Data_Visualization-1/Kaggle_Data_Visualization-2.png)  

<details> 
<summary>코드 해석</summary>

```python
man = df[df['Q2'] == 'Man']['Q1'].value_counts()
woman = df[df['Q2'] == 'Woman']['Q1'].value_counts()
textonbar_man = [ round((m/(m+w))*100, 1) for m, w in zip(man.values, woman.values)]
textonbar_woman = [ round((w/(m+w))*100, 1) for m, w in zip(man.values, woman.values)]
```

`man = df[df['Q2'] == 'Man']['Q1'].value_counts()`  
-> 성별이 남성`[df['Q2'] == 'Man]`인 행에서 나이`['Q1']`의 값을 카운트하여 시리즈를 생성한다.

`woman = df[df['Q2'] == 'Woman']['Q1'].value_counts()`  
-> 성별이 여성`[df['Q2'] == 'Woman']`인 행에서 나이`['Q1']`의 값을 카운트하여 시리즈를 생성한다.  

`textonbar_man = [round((m/(m+w))*100, 1) for m, w in zip(man.values, woman.values)]`  
-> for문을 사용하여 round함수를 계산 하고 `textonbar_man`에 저장한다.

`textonbar_woman = [round((uw/(m+w))*100, 1) for m, w in zip(man.values, woman.values)]`  
-> for문을 사용하여 round함수를 계산 하고 `textonbar_woman`에 저장한다.

<br><br>

```python
fig = go.Figure(data=[
                        go.Bar(
                            name='Man', x=man.index, y=man.values,
                            text=textonbar_man, marker_color=colors[2]
                        ),
                        go.Bar(
                            name='Woman', x=woman.index, y=woman.values,
                            text=textonbar_woman, marker_color=colors[3]
                        )
])
```

`go.Bar(`  
-> 그래프의 모양이 막대모양임을 의미한다.

`name='Man', x=man.index, y=man.values,`  
-> 순서대로 막대의 이름, x축에는 man의 인덱스, y축에는 man의 값을 나타내라는 의미이다. 

`text=textonbar_man, marker_color=colors[2]),`  
-> 각각 막대의 값을 작성해줄 텍스트, 막대의 색을 의미한다.

<br><br>

```python
fig.update_traces(
                    texttemplate='%{text:.3s}%',
                    textposition='inside')
fig.update_layout(
                    barmode='stack',
                    title_text='Age distribution by gender',
                    xaxis_title='Age', yaxis_title='Counts')
fig.show()
)
```

`texttemplate='%{text:.3s}%',`  
-> fig(print(fig)로 출력가능)내부의 `text` 인자를 차례대로 출력 (그래프의 위의 텍스트를 표현)

`textposition='inside'`  
-> 그래프상에서의 값의 위치를 설정한다.

`barmode='stack'`  
-> 막대의 형태를 표현한다.

`title_text='Age distribution by gender'`  
-> 그래프의 제목을 설정한다.

`xaxis_title='Age', yaxis_title='Counts'`  
-> 그래프의 x축 제목, y축 제목


</details>

</details>

### 몇몇 요소 확인법

---


`print(type(데이터))`  
-> 데이터의 타입을 출력한다

`데이터.head()`,`데이터.tail()`  
-> 데이터를 인덱스 순으로 출력한다. **head**는 처음부터 끝까지, **tail**은 반대로 출력하며 괄호안에 숫자를 입력하면 숫자만큼 출력한다.  



## References

[go.Figure() properties](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#id0)  
[update_traces() properties](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.update_traces)  
[update_layout() properties](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.update_layout)  
[show() properties](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.show)   
[go.Bar() properties](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Bar.html)  