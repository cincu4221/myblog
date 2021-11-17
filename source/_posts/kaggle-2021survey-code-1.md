---
title: 2021 캐글 대회 코드 작성기 
date: 2021-11-17 15:07:03
tags: 
- Kaggle
- Python
- Plotly
---

## import(Kaggle notebook)

---
```python
import numpy as np 
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from warnings import filterwarnings
from plotly.subplots import make_subplots
filterwarnings('ignore')

colors = ['#B1EDED','#B1B2ED','#1DE7ED','#1DA5ED','#1D50ED','#16548E']
gen_colors = ['#4169E1','#B2182B','#81007F','#D1B2FF','#EFE4E2']
JP_colors = ['#D90B0B','#F24444','#EFE4E2','#FCCE88','#64807F']
CN_colors = ['#E0201B','#FFCE3F','#A63F03','#04BF33','#F2E6D8']
coun_years_colors = ['#D90B0B','#FFCE3F','#FF6161','#FFDB81']

df19 = pd.read_csv('../input/kaggle-survey-2019/multiple_choice_responses.csv')
df21 = pd.read_csv('../input/kaggle-survey-2021/kaggle_survey_2021_responses.csv')
```
이처럼 후에 사용할 라이브러리를 임포트, 그래프에 사용할 색을 리스트로 만들어주고 df19에 19년도 데이터셋을, df21에 21년도 데이터셋을 넣어준다.

## Q1. What`s your age?

---

## Q2. What`s your gender?

---

```python
fig = make_subplots(rows=2, cols=2, specs=[[{'type':'domain'}, {'type':'domain'}],[{'type':'domain'}, {'type':'domain'}]])

fig.add_trace(go_Pie('2019_Japan', JP_age_series.value_counts()),1,1)
              
fig.add_trace(go_Pie('2019_China', CN_age_series.value_counts()),1,2)

fig.add_trace(go_Pie('2021_Japan', group(df21,'Japan','Q2')),2,1)

fig.add_trace(go_Pie('2021_China', group(df21,'China','Q2')),2,2)

fig.update_traces(marker=dict(colors=gen_colors[0:]))
fig.update_layout(title_text='Gender Distribution',
                  paper_bgcolor='ivory',
                  showlegend=True,
                  autosize=True,
                  height=700)
fig.show()
```
