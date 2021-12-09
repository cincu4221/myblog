---
title: 2021 캐글 대회 코드 작성기 - 1
date: 2021-11-17 15:07:03
categories: 
- Data Visualization
tags: 
- Kaggle
- Python
- Plotly
---
파이썬을 배운지 며칠 되지 않아 kaggle이라는 예측모델 및 분석대회 플랫폼의 데이터 분석 대회에 참가하게 되었다.   
주제는 2021년 캐글러<sup>kaggler</sup>들에게 설문조사이며, 그 설문조사 데이터셋을 바탕으로 참가자가 분석을 하여 참가자만의 주제에 그래프와 수치로 답을 찾아내는 대회이다.

데이터셋에 있는 캐글러의 수는 19년 19717명, 21년 25974명, 직업은 데이터사이언스, 데이터 엔지니어부터 학생까지 다양하며, 나이, 학력, 국적, 라이브러리, 언어 등 매우 다양한 항목들이 있다.  

우리 조에서 처음으로 선정하려 했던 주제는 한국, 일본, 중국의 캐글러의 트렌드변화로 하려 했으나, 중국, 일본에 비해 데이터가 턱없이 부족해 비교가 무의미한 수준이었기에 캐글러의 수가 비슷한 두 나라인 중국과 일본로 선정했다.(의외로 중국의 캐글러 절대적인 수가 인구에 비해 상당히 적어 일본보다 조금 적은편이였다.)
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
이처럼 후에 사용할 라이브러리를 임포트, 그래프에 사용할 색을 리스트로 만들어주고 df19에 19년의 데이터셋을, df21에 21년의 데이터셋을 넣어준다.


## 사용자 지정 함수

---
```python
def group(data, country, question_num):
    return data[data['Q3'] == country][question_num].value_counts()

def go_Pie(country, label_value):
    return go.Pie(title = country,
                  labels = label_value.index,
                  values = label_value.values,
                  textinfo = 'label+percent',
                  rotation=315,
                  hole = .3,)
```

앞으로 코드에서 사용될 함수이다.  
[사용자 지정 함수란?](https://cincu4221.github.io/2021/11/10/Python-UserDefinedFunctions/)

## Q1. What`s your age?

---

```python
JP_age_19 = group(df19,'Japan','Q1').sort_index()

JP_age_21 = group(df21,'Japan','Q1').sort_index()

CN_age_19 = group(df19,'China','Q1')
CN_age_19.loc['55-59'] = 0
CN_age_19.loc['60-69'] = 0
CN_age_19 = CN_age_19.sort_index()

CN_age_21 = group(df21,'China','Q1')
CN_age_21.loc['60-69'] = 0
CN_age_21 = CN_age_21.sort_index()

fig_age = make_subplots(rows=1, cols=2, specs=[[{'type':'xy'}, {'type':'xy'}]])

fig_age.add_trace(go.Bar(name=coun_years[0], x=JP_age_19.index, y=JP_age_19.values, marker_color='#FDB0C0'),1,1)
fig_age.add_trace(go.Bar(name=coun_years[2], x=JP_age_21.index, y=JP_age_21.values, marker_color='#FD4659'),1,1)
fig_age.add_trace(go.Bar(name=coun_years[1], x=CN_age_19.index, y=CN_age_19.values, marker_color='#FFDB81'),1,2)
fig_age.add_trace(go.Bar(name=coun_years[3], x=CN_age_21.index, y=CN_age_21.values, marker_color='#FFAB0F'),1,2)

fig_age.update_layout(barmode='group', title_text='2019 & 2021, Japan and China age distribution', showlegend=True)

fig_age.update_xaxes(title_text='Japan Age distribution', row=1, col=1)
fig_age.update_yaxes(title_text='Counts', row=1, col=1)
fig_age.update_xaxes(title_text='China Age distribution', row=1, col=2)
fig_age.update_yaxes(title_text='Counts', row=1, col=2)

fig_age.show()
```

![일본, 중국 캐글러의 나이분포](/images/kaggle_graph/Q1gragh.png)  
 
첫번째 주제인 What`s your age?에 대한 일본과 중국의 캐글러 나이분포를 막대그래프로 나타낸 것이다.  
각 그래프는 연도별로 나눈 일,중 캐글러의 나이 분포이고 그래프의 항목은 18세부터 70세 이상까지 3,4년씩을 한 항목으로 묶었다.


## Q2. What`s your gender?

---

```python
JP_ndarray = df19[df19['Q3'] == 'Japan']['Q2'].values
CN_ndarray = df19[df19['Q3'] == 'China']['Q2'].values
JP_age_list = []
CN_age_list = []

for item in JP_ndarray:
    if item == 'Male':
        item_mod = item.replace('Male','Man')
        JP_age_list.append(item_mod)
    elif item == 'Female':
        item_mod2 = item.replace('Female','Woman')
        JP_age_list.append(item_mod2)
    else :
        JP_age_list.append(item)
    
for item in CN_ndarray:
    if item == 'Male':
        item_mod = item.replace('Male','Man')
        CN_age_list.append(item_mod)
    elif item == 'Female':
        item_mod2 = item.replace('Female','Woman')
    else :
        CN_age_list.append(item)

JP_age_series = pd.Series(JP_age_list)
CN_age_series = pd.Series(CN_age_list)

fig = make_subplots(rows=2, cols=2, specs=[[{'type':'domain'}, {'type':'domain'}],
                                           [{'type':'domain'}, {'type':'domain'}]])

fig.add_trace(go_Pie('2019_Japan', JP_age_series.value_counts()),1,1)
fig.add_trace(go_Pie('2019_China', CN_age_series.value_counts()),1,2)
fig.add_trace(go_Pie('2021_Japan', group(df21,'Japan','Q2')),2,1)
fig.add_trace(go_Pie('2021_China', group(df21,'China','Q2')),2,2)

fig.update_traces(marker=dict(colors=gen_colors[0:]))
fig.update_layout(title_text='Gender Distribution',
                  showlegend=True,
                  autosize=True,
                  height=700)
fig.show()
```

![일본, 중국 캐글러의 성별분포](/images/kaggle_graph/Q2gragh.png)  
 
두번쨰 질문에 답하기 위해 일본과 중국의 캐글러 성별분포를 도넛모양으로 나타낸 그래프이다.  
각각의 그래프는 국가,년도(2019, 2021)별로 각각 나누었고 그래프의 항목은 
`Man` 
`Woman` 
`Prefer not to say` 
`Nonbinary` 
`Prefer to self-describe`  
이렇게 다섯가지로 나누었다.


## References

[plotly bar chart tutorial](https://plotly.com/python/bar-charts/)  
[plotly bar chart properties (bar traces)](https://plotly.com/python/reference/bar/)  
[plotly pie chart tutorial](https://plotly.com/python/pie-charts/)  
[plotly pie chart properties (pie traces)](https://plotly.com/python/reference/pie/)

