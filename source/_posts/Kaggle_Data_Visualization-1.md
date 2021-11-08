---
title: 캐글 데이터 시각화 해석-1
date: 2021-11-08 14:50:50
tags:
- Kaggle
- Data Visualization
---

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

## 원그래프 해석

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
<summary>Output</summary>

![위 코드의 그래프](/images/Kaggle_Data_Visualization-1/Kaggle_Data_Visualization-1.png)


</details>

```python
man = df[df['Q2'] == 'Man']['Q1'].value_counts() # 성별이 남성[df['Q2'] == 'Man']인 행에서 나이['Q1']의 값을 카운트하여 시리즈로 만듦.
woman = df[df['Q2'] == 'Woman']['Q1'].value_counts() # 성별이 여성[df['Q2'] == 'Woman']인 행에서 나이['Q1']의 값을 카운트하여 시리즈로 만듦.
textonbar_man = [ # list comprehension = [(변수를 활용한 값) for (사용할 변수 이름) in (순회 할 수 있는 값)]
                    round((m/(m+w))*100, 1) for m, w in zip(man.values, woman.values)] # for문을 사용하여 round함수의 계산을 하고 textonbar_man에 저장
textonbar_woman = [ # list comprehension
                    round((w/(m+w))*100, 1) for m, w in zip(man.values, woman.values)]

fig = go.Figure(data=[ # 그래프의 형태를 정하는 함수
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
                    texttemplate='%{text:.3s}%', # 수치가 그래프에서 어느정도 멀어지는지
                    textposition='inside') # 값의 위치
fig.update_layout(
                    barmode='stack', # 막대의 형태
                    title_text='Age distribution by gender', # 제목
                    xaxis_title='Age', # x축 제목
                    yaxis_title='Counts') # y축 제목
fig.show()
```
