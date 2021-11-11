---
title: 파이썬 시각화 기본
date: 2021-11-03 12:23:18
categories: 
- Data Visualization
tags:
- Python
- Data Visualization
---

## 파이썬 시각화의 기본 형태들

---

* 선 그래프로 시각화하기
```python
import matplotlib.pyplot as plt

dates = [
    '2021-01-01', '2021-01-02', '2021-01-03', '2021-01-04', '2021-01-05',
    '2021-01-06', '2021-01-07', '2021-01-08', '2021-01-09', '2021-01-10'
]
min_temperature = [20.7, 17.9, 18.8, 14.6, 15.8, 15.8, 15.8, 17.4, 21.8, 20.0]
max_temperature = [34.7, 28.9, 31.8, 25.6, 28.8, 21.8, 22.8, 28.4, 30.8, 32.0]

fig, ax = plt.subplots()
ax.plot(dates, min_temperature, label = "Min Temp")
ax.plot(dates, max_temperature, label = "Max Temp")
ax.legend()
plt.show()
```

<details> 
<summary>Output</summary>
    
![선 그래프로 시각화](/images/python_visualiztion_basic_/output_1_0.png)
    
</details>

* 위의 그래프에서 크기의 변화를 준 그래프
```python
import matplotlib.pyplot as plt

dates = [
    '2021-01-01', '2021-01-02', '2021-01-03', '2021-01-04', '2021-01-05',
    '2021-01-06', '2021-01-07', '2021-01-08', '2021-01-09', '2021-01-10'
]
min_temperature = [20.7, 17.9, 18.8, 14.6, 15.8, 15.8, 15.8, 17.4, 21.8, 20.0]
max_temperature = [34.7, 28.9, 31.8, 25.6, 28.8, 21.8, 22.8, 28.4, 30.8, 32.0]

fig, axes = plt.subplots(nrows=1, ncols=1, figsize=(10,6))
axes.plot(dates, min_temperature, label = 'Min Temperature')
axes.plot(dates, max_temperature, label = 'Max Temperature')
axes.legend()
plt.show()
```

<details> 
<summary>Output</summary>
    
![크기의 변화를 준 그래프](/images/python_visualiztion_basic_/output_2_0.png)
    
</details>

* `fig`와 `axes` 출력
```python
print(fig)
print(axes)
```

<details> 
<summary>Output</summary>

    Figure(720x432)
    AxesSubplot(0.125,0.125;0.775x0.755)
</details>

    

## Matplotlib

---

### 선 그래프



먼저 `yfinance`라이브러리를 사용하기 위해 설치를 한다.
```shell
!pip install yfinance --upgrade --no-cache-dir
```
<details> 
<summary>실행시</summary>

    Collecting yfinance
      Downloading yfinance-0.1.64.tar.gz (26 kB)
    Requirement already satisfied: pandas>=0.24 in /usr/local/lib/python3.7/dist-packages (from yfinance) (1.1.5)
    Requirement already satisfied: numpy>=1.15 in /usr/local/lib/python3.7/dist-packages (from yfinance) (1.19.5)
    Requirement already satisfied: requests>=2.20 in /usr/local/lib/python3.7/dist-packages (from yfinance) (2.23.0)
    Requirement already satisfied: multitasking>=0.0.7 in /usr/local/lib/python3.7/dist-packages (from yfinance) (0.0.9)
    Collecting lxml>=4.5.1
      Downloading lxml-4.6.4-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (6.3 MB)
    [K     |████████████████████████████████| 6.3 MB 5.3 MB/s 
    [?25hRequirement already satisfied: python-dateutil>=2.7.3 in /usr/local/lib/python3.7/dist-packages (from pandas>=0.24->yfinance) (2.8.2)
    Requirement already satisfied: pytz>=2017.2 in /usr/local/lib/python3.7/dist-packages (from pandas>=0.24->yfinance) (2018.9)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.7/dist-packages (from python-dateutil>=2.7.3->pandas>=0.24->yfinance) (1.15.0)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /usr/local/lib/python3.7/dist-packages (from requests>=2.20->yfinance) (1.24.3)
    Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.7/dist-packages (from requests>=2.20->yfinance) (2021.5.30)
    Requirement already satisfied: idna<3,>=2.5 in /usr/local/lib/python3.7/dist-packages (from requests>=2.20->yfinance) (2.10)
    Requirement already satisfied: chardet<4,>=3.0.2 in /usr/local/lib/python3.7/dist-packages (from requests>=2.20->yfinance) (3.0.4)
    Building wheels for collected packages: yfinance
      Building wheel for yfinance (setup.py) ... [?25l[?25hdone
      Created wheel for yfinance: filename=yfinance-0.1.64-py2.py3-none-any.whl size=24109 sha256=da9039df457bcaed01c34fcce5bc8ee52dcf33151b9275684543166937fa1286
      Stored in directory: /tmp/pip-ephem-wheel-cache-qozcsm2m/wheels/86/fe/9b/a4d3d78796b699e37065e5b6c27b75cff448ddb8b24943c288
    Successfully built yfinance
    Installing collected packages: lxml, yfinance
      Attempting uninstall: lxml
        Found existing installation: lxml 4.2.6
        Uninstalling lxml-4.2.6:
          Successfully uninstalled lxml-4.2.6
    Successfully installed lxml-4.6.4 yfinance-0.1.64

다음과 같이 출력되며 `yfinace`를 설치한다.


</details>

`yfinance`를 임포트해주고 그로부터 데이터를 받아와 출력을 할수 있다.
```python
import yfinance as yf
data = yf.download('AAPL', '2019-08-01', '2020-08-01')
data.info()
```
<details> 
<summary>Output</summary>

    [*********************100%***********************]  1 of 1 completed
    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 253 entries, 2019-08-01 to 2020-07-31
    Data columns (total 6 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   Open       253 non-null    float64
     1   High       253 non-null    float64
     2   Low        253 non-null    float64
     3   Close      253 non-null    float64
     4   Adj Close  253 non-null    float64
     5   Volume     253 non-null    int64  
    dtypes: float64(5), int64(1)
    memory usage: 13.8 KB
다음과 같이 애플의 1년동안의 주가를 볼 수 있다.
</details>

데이터의 컬럼을 지목해서 열람하는것 역시 가능하다.
```python
ts = data['Open']
print(ts.head())
```
<details> 
<summary>Output</summary>

    Date
    2019-08-01    53.474998
    2019-08-02    51.382500
    2019-08-05    49.497501
    2019-08-06    49.077499
    2019-08-07    48.852501
    Name: Open, dtype: float64
`data`에 담겨있는 애플의 주가정보 중 'Open'에 해당하는 전일 종가를 가장 앞쪽(`.head()`)부터 출력한 것이다.
애플주식이 이렇게 쌌었나 검색해보니 이게 맞다....

</details>

<br><br>

#### 방법 1. Pyplot API

---

```python
# import fix_yahoo_finance as yf
import yfinance as yf
import matplotlib.pyplot as plt

data = yf.download('AAPL', '2019-11-01', '2021-11-01')
ts = data['Open']
plt.figure(figsize=(10,6))
plt.plot(ts)
plt.legend(labels=['Price'], loc='best')
plt.title('Stock Market fluctuation of AAPL') 
plt.xlabel('Date') 
plt.ylabel('Stock Market Open Price') 
plt.show()
```
<details> 
<summary>Output</summary>

    [*********************100%***********************]  1 of 1 completed

![애플의 최근 2년간 전일종가 그래프](/images/python_visualiztion_basic_/output_10_1.png)  
이처럼 결과가 출력되지만 이 문법은 시각화를 처음배우는 초심자에게는 적합하지 않다고 한다.  
후술할 문법과 위 문법 모두 출력은 되나 이 문법은 객체지향이 아니기도 하고 상대적으로 복잡하기때문에 초심자의 경우에 헷갈릴수 있어 사용하지 않는다.
구글링 했을때 `객체.`이 아닌 `plt.`으로 시작하는 애들이 있다면 그 코드는 스킵하는게 좋다.
</details>

<br><br>

#### 방법 2. 객체지향 API

---

```python
from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
from matplotlib.figure import Figure
import matplotlib.pyplot as plt

fig = Figure()

import numpy as np
np.random.seed(6)
x = np.random.randn(20000)

ax = fig.add_subplot(111)
ax.hist(x, 100)
ax.set_title('Artist Layer Histogram')
# fig.savefig('Matplotlib_histogram.png')
plt.show()
```
이 방법에 대해서는 따로 언급이 없었기 때문에 바로 방법 3으로 넘어간다.

<br><br>

#### 방법 3. Pyplot API + 객체지향 API

---
```python
import yfinance as yf
import matplotlib.pyplot as plt

data = yf.download('AAPL', '2019-08-01', '2020-08-01')
ts = data['Open']

fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(ts)
ax.set_title('Stock Market fluctuation of AAPL')
ax.legend(labels=['Price'], loc='best')
ax.set_xlabel('Date')
ax.set_ylabel('Stock Market Open Price')
plt.show()
```

<details> 
<summary>Output</summary>

    [*********************100%***********************]  1 of 1 completed
![](/images/python_visualiztion_basic_/output_14_1.png)  
드디어 꼭 외우라고 하셨던 pyplot + 객체지향 API 방법이다.  
특히 7번째 행 부터 마지막까지가 중요한데 그에대한 설명은 아래에 표로 적겠다.  
중요하다 몇번을 강조하셨으니 위 코드는 변형을 해가며 여러번 작성해보자.

<details> 
<summary>설명 표</summary>

|코드|설명|
|:---:|:---:|
|fig, ax = plt.subplots()|데이터 전체적 외형을 설정하는 부분|
|ax.plot(ts)|데이터를 표현해주는 행|
|ax.set_title()|데이터 시각화의 제목|
|ax.legend()|범례|
|ax.set_xlabel()|x축 데이터의 제목|
|ax.set_ylabel()|y축 데이터의 제목|
|plt.show()|안해도 상관없으나 '완료후 게시' 라는 뜻으로 작성|
앞으로 나올 표의 내용도 표의 위에 있는 코드들과 적절히 섞어서 이해하길 바란다.

</details>

</details>
    


### 막대 그래프

---

```python
import matplotlib.pyplot as plt
import numpy as np
import calendar

month_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
sold_list = [300, 400, 550, 900, 600, 960, 900, 910, 800, 700, 550, 450]

fig, ax = plt.subplots(figsize=(10,6))
plt.xticks(month_list, calendar.month_name[1:13], rotation=90)
plot = ax.bar(month_list, sold_list)
for rect in plot:
  print("graph:", rect) 
  height = rect.get_height()
  ax.text(rect.get_x() + rect.get_width()/2., 1.002*height,'%d' % 
  int(height), ha='center', va='bottom')

plt.show()
```

<details> 
<summary>Output</summary>

    graph: Rectangle(xy=(0.6, 0), width=0.8, height=300, angle=0)
    graph: Rectangle(xy=(1.6, 0), width=0.8, height=400, angle=0)
    graph: Rectangle(xy=(2.6, 0), width=0.8, height=550, angle=0)
    graph: Rectangle(xy=(3.6, 0), width=0.8, height=900, angle=0)
    graph: Rectangle(xy=(4.6, 0), width=0.8, height=600, angle=0)
    graph: Rectangle(xy=(5.6, 0), width=0.8, height=960, angle=0)
    graph: Rectangle(xy=(6.6, 0), width=0.8, height=900, angle=0)
    graph: Rectangle(xy=(7.6, 0), width=0.8, height=910, angle=0)
    graph: Rectangle(xy=(8.6, 0), width=0.8, height=800, angle=0)
    graph: Rectangle(xy=(9.6, 0), width=0.8, height=700, angle=0)
    graph: Rectangle(xy=(10.6, 0), width=0.8, height=550, angle=0)
    graph: Rectangle(xy=(11.6, 0), width=0.8, height=450, angle=0)

![막대 그래프로 시각화](/images/python_visualiztion_basic_/output_17_1.png)

<details> 
<summary>메소드 설명</summary>

`.xticks()`는 x축의 눈금을 나타내는 메소드인데 기본적으로는 `list`자료형 한개을 사용한다.  
하지만 메소드에 인자가 'list' 두 개로 받아졌을 경우,  
첫번째 list는 x축 눈금의 갯수가 된다.  
두번째 list는 x축 눈금의 이름이 된다.  
이 코드에서는 `rotation` 옵션도 들어가 있는데 이것은 그냥 이름을 몇도정도 기울일지 나타낸다.
<br><br>
`plot = ax.bar()`는 그래프를 막대로 만든다.  
첫번째 리스트 인자의 수 만큼 막대가 생성되고,  
두번째 리스트 인자의 값 만큼 막대가 길어진다.  
이렇다보니 첫번째 리스트와 두번째 리스트의 인자의 수가 일치해야 에러가 나지 않는다.
<br><br>
for문 내부의 `ax.text()`는 `Seaborn`-`막대그래프`-`표현할 값이 한 개인 막대 그래프` 챕터에 서술했으니 참고하길 바란다.

</details>




</details>



### 산점도 그래프

---

- 두개의 연속형 변수 (키, 몸무게 등)
- 상관관계 != 인과관계
<br><br>  

* 나타내는 값이 한가지인 산점도 그래프

```python
import matplotlib.pyplot as plt
import seaborn as sns

# 내장 데이터
tips = sns.load_dataset("tips")
x = tips['total_bill']
y = tips['tip']

fig, ax = plt.subplots(figsize=(10, 6))
ax.scatter(x, y) # 각각의 값을 선으로 표현해주는 scatter()
ax.set_xlabel('Total Bill')
ax.set_ylabel('Tip')
ax.set_title('Tip ~ Total Bill')

fig.show()
```
<details> 
<summary>Output</summary>

![전체 값 대비 팁](/images/python_visualiztion_basic_/output_19_0.png)
</details>

<br>

* 나타내는 값이 두 가지인 산점도 그래프

```python
label, data = tips.groupby('sex')
tips['sex_color'] = tips['sex'].map({"Female" : "#0000FF", "Male" : "#00FF00"})

fig, ax = plt.subplots(figsize=(10, 6))
for label, data in tips.groupby('sex'):
  ax.scatter(data['total_bill'], data['tip'], label=label, 
             color=data['sex_color'], alpha=0.5)
  ax.set_xlabel('Total Bill')
  ax.set_ylabel('Tip')
  ax.set_title('Tip ~ Total Bill by Gender')

ax.legend()
fig.show()
```
<details> 
<summary>Output</summary>
    
![전체 값 대비 팁의 성별분포](/images/python_visualiztion_basic_/output_21_0.png)

</details>

### 히스토그램

---

- 수치형 변수 1개


```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

# 내장 데이터 
titanic = sns.load_dataset('titanic')
age = titanic['age']

nbins = 21
fig, ax = plt.subplots(figsize=(10, 6))
ax.hist(age, bins = nbins) # 여기서 bins = nbins는 히스토그램을 더 세밀하게 나누어 준다.
ax.set_xlabel("Age")
ax.set_ylabel("Frequency")
ax.set_title("Distribution of Aae in Titanic")
ax.axvline(x = age.mean(), linewidth = 2, color = 'r')
fig.show()
```

<details> 
<summary>Output</summary>
    
![타이타닉호 탑승객의 나이 분포](/images/python_visualiztion_basic_/output_23_0.png)  

|코드|설명|
|:---:|:---:|
|`.hist()`|데이터를 히스토그램으로 표현해주는 메소드|
|`.axvline()`|데이터의 평균을 선으로 나타내주는 메소드|
</details>

### 박스플롯

---

- x축 변수: 범주형 변수, 그룹과 관련있는 변수, 문자열
- y축 변수: 수치형 변수 


```python
import matplotlib.pyplot as plt
import seaborn as sns

iris = sns.load_dataset('iris')

data = [iris[iris['species']=="setosa"]['petal_width'], 
        iris[iris['species']=="versicolor"]['petal_width'],
        iris[iris['species']=="virginica"]['petal_width']]

fig, ax = plt.subplots(figsize=(10, 6))
ax.boxplot(data, labels=['setosa', 'versicolor', 'virginica'])

fig.show()
```

<details> 
<summary>Output</summary>
    
![png](/images/python_visualiztion_basic_/output_25_0.png)  
수정바람) 정확히 어떻게 이 그래프가 출력되는지 모르기에 좀 더 공부후 수정할 것
</details>

### 히트맵

---

```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

# 내장 데이터
flights = sns.load_dataset("flights")
flights = flights.pivot("month", "year", "passengers")

fig, ax = plt.subplots(figsize=(12, 6))
im = ax.imshow(flights, cmap = 'YlGnBu')
ax.set_xticklabels(flights.columns, rotation = 20)
ax.set_yticklabels(flights.index, rotation = 10)
fig.colorbar(im)

fig.show()
```
<details> 
<summary>Output</summary>

         year month  passengers
    0    1949   Jan         112
    1    1949   Feb         118
    2    1949   Mar         132
    3    1949   Apr         129
    4    1949   May         121
    ..    ...   ...         ...
    139  1960   Aug         606
    140  1960   Sep         508
    141  1960   Oct         461
    142  1960   Nov         390
    143  1960   Dec         432
    
    [144 rows x 3 columns]
    
![연,월별 승객의 수](/images/python_visualiztion_basic_/output_27_1.png)  

|제목|제목|
|:---:|:---:|
|||
|fig.colorbar()|값의 빈도 수에 대한 컬러바생성|

</details>



## Seaborn

---

### 산점도와 회귀선이 있는 산점도

--- 


* 산점도


```python
%matplotlib inline 

import matplotlib.pyplot as plt
import seaborn as sns

tips = sns.load_dataset("tips")
sns.scatterplot(x = "total_bill", y = "tip", data = tips)
plt.show()
```

<details> 
<summary>Output</summary>

![산점도](/images/python_visualiztion_basic_/output_30_0.png)  
</details>

<br>

* 회귀선이 있는 산점도

```python
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(15, 5))
sns.regplot(x = "total_bill", 
            y = "tip", 
            data = tips, 
            ax = ax[0], 
            fit_reg = True)

sns.regplot(x = "total_bill", 
            y = "tip", 
            data = tips, 
            ax = ax[1], 
            fit_reg = False)

plt.show()
```

<details> 
<summary>Output</summary>
    
![회귀선이 있는 산점도](/images/python_visualiztion_basic_/output_31_0.png)  
위의 코드처럼 `fit_reg = True`로 해줄 경우 회귀선이 나타나는것을 알 수 있다.
그리고 `ax = ax[num]`의 경우에는 그래프의 인덱스로 보인다.

</details>

### 히스토그램/커널 밀도 그래프

---

```python
import matplotlib.pyplot as plt
import seaborn as sns

tips = sns.load_dataset("tips")

plt.figure(figsize=(10, 6))
sns.displot(x = "tip", data = tips)
sns.displot(x="tip", kind="kde", data=tips) # 종류 = 커널밀도 그래프(kde)
sns.displot(x="tip", kde=True, data=tips) # 히스토그램에 kde를 넣을건가 = True
plt.show()
```
<details> 
<summary>Output</summary>

    <Figure size 720x432 with 0 Axes>
![히스토그램](/images/python_visualiztion_basic_/output_33_0.png)
![커널 밀도 그래프](/images/python_visualiztion_basic_/output_34_0.png)    
![커널 밀드 그래프가 그려진 히스토그램](/images/python_visualiztion_basic_/output_35_0.png)

</details>


### 박스플롯


```python
#import matplotlib.pyplot as plt  # 주석처리된 부분은 원래 실행 해줘야 하는 내용이지만 위 히스토그램 챕터에서 미리 입력했기 때문에 생략한다. 
#import seaborn as sns

#tips = sns.load_dataset("tips")

sns.boxplot(x = "day", y = "total_bill", data = tips)
sns.swarmplot(x = "day", y = "total_bill", data = tips, alpha = .25)
plt.show()
```

<details> 
<summary>Output</summary>
    
![박스플롯](/images/python_visualiztion_basic_/output_37_0.png)
    
</details>


### 막대 그래프


```python
#import matplotlib.pyplot as plt  # 이 주석 역시 원래 실행 해줘야 하는 내용이지만 위 히스토그램 챕터에서 미리 입력했기 때문에 생략한다. 이하 기본주석이라 하고 생략한다.
#import seaborn as sns

#tips = sns.load_dataset("tips")

sns.countplot(x = "day", data = tips)
plt.show()
```

<details> 
<summary>Output</summary>
    
![png](/images/python_visualiztion_basic_/output_39_0.png)
    
</details>

<br>

<details> 
<summary>'tips'Data의 'day'값, 인덱스별 정렬, 'tips'의 내림차순 재배치</summary>




```python
print(tips['day'].value_counts())
print("index: ", tips['day'].value_counts().index)
print("values: ", tips['day'].value_counts().values)
```

    Sat     87
    Sun     76
    Thur    62
    Fri     19
    Name: day, dtype: int64
    index:  CategoricalIndex(['Sat', 'Sun', 'Thur', 'Fri'], categories=['Thur', 'Fri', 'Sat', 'Sun'], ordered=False, dtype='category')
    values:  [87 76 62 19]
    
</details>

<br>

<details> 
<summary>'tips'Data의 'day'값에 대한 오름차순(ascending) 정렬</summary>

```python
print(tips['day'].value_counts(ascending=True))
```

    Fri     19
    Thur    62
    Sun     76
    Sat     87
    Name: day, dtype: int64
    
</details>

<br>

* 표현할 값이 한 개인 막대 그래프

```python
# 기본주석 생략
ax = sns.countplot(x = "day", data = tips, order = tips['day'].value_counts().index) # x축을 'day'로 지정, data는 'tips'로 채워넣음, 'day'의 값이 높은 순서대로 막대그래프 정렬 
for p in ax.patches: # ax.patches = p
  height = p.get_height() # 아래행을 실행하기위해 막대그래프의 높이 가져옴
  ax.text(p.get_x() + p.get_width()/2., height+3, height, ha = 'center', size=9) # 막대그래프 위 수치 작성
ax.set_ylim(-5, 100) # y축 최소, 최대범위
plt.show()
```

<details> 
<summary>Output</summary>
    
![나타낼 값이 한 개인 막대그래프](/images/python_visualiztion_basic_/output_43_0.png)  
나중에 다시 본다면 조금 설명이 필요할 것 같다.  
특히 `ax.text`행의 인자가 조금 많은데 설명이 필요한 듯하다.  
직접 colab에서 이것저것 만져본 결과 추측하기로는 다음 표과 같은듯 하다.


|코드|설명|
|:---:|:---:|
|p.get_x() + p.get_width()/2.|수치가 들어갈 x축 위지|
|height+3|y축 위치(현재 +3)|
|height|수치의 값을 조절할 것인지(현재 +0)|
|ha = 'center'|수치를 (x,y)축의 가운데로 정렬|
|size=9|폰트의 크기이다|

여기서 혹시나 `ha = 'center'`부분이 잘 이해가 안될수 있다.~~내가그랬다~~  
`ha =`는 (x,y)축의 기준이 될 곳을 정하는 인자인듯 하다.  
`center`말고도 `left`,`right`등을 사용할수 있는데 막대의 기준에서 왼쪽,오른쪽이 아닌 텍스트의 기준에서 왼쪽,오른쪽이라 방향을 선택하면 오히려 반대로 배치되는것을 알 수 있다.

</details>

* 표현할 값이 두 개인 막대 그래프

```python
# 기본주석 생략
ax = sns.countplot(x = "day", data = tips, hue = "sex", dodge = True,
              order = tips['day'].value_counts().index)
for p in ax.patches:
  height = p.get_height()
  ax.text(p.get_x() + p.get_width()/2., height+3, height, ha = 'center', size=9)
ax.set_ylim(-5, 100)

plt.show()
```

<details> 
<summary>Output</summary>
    
![나타낼 값이 두 개인 막대그래프](/images/python_visualiztion_basic_/output_44_0.png)  

이 코드에서 첫째줄의 인자를 표로 나타내면  

|코드|설명|
|:---:|:---:|
|x = "day"| x축이 나타낼 자료 |
|data = tips| 표현할 데이터셋 |
|hue = "sex"| 그래프로 표현할 항목 |
|dodge = True| 항목끼리 나눠서 표현할 것인지 |
|order = tips['day'].value_counts().index| 'day'의 값이 높은 순서대로 그래프 정렬 |

sns.countplot() x축이 나타낼 자료, 나타낼 데이터셋, 그래프로 나타낼 항목, 항목끼리 나눠서 표현할것인지, 'day'의 값이 높은 순서대로 막대그래프 정렬 
</details>

### 상관관계 그래프

---

<details> 
<summary>데이터 불러오기 및 행, 열 갯수 표시하기</summary>

```python
import pandas as pd 
import numpy as np 
import seaborn as sns
import matplotlib.pyplot as plt

mpg = sns.load_dataset("mpg")
print(mpg.shape) # 398 행, 9개 열

num_mpg = mpg.select_dtypes(include = np.number) # num_mpg에 'mpg' 데이터셋의 데이터타입 총갯수를 입력한다(숫자형 데이터타입만 포함)
print(num_mpg.shape) # 398 행, 7개 열 (두개가 사라진 이유는 number타입이 아닌 Object타입이기 때문)
```


    (398, 9)
    (398, 7)

</details>

<br>

<details> 
<summary>데이터셋의 컬럼 표시</summary>

```python
num_mpg.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 398 entries, 0 to 397
    Data columns (total 7 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   mpg           398 non-null    float64
     1   cylinders     398 non-null    int64  
     2   displacement  398 non-null    float64
     3   horsepower    392 non-null    float64
     4   weight        398 non-null    int64  
     5   acceleration  398 non-null    float64
     6   model_year    398 non-null    int64  
    dtypes: float64(4), int64(3)
    memory usage: 21.9 KB
    
</details>

<br>

<details> 
<summary>데이터셋 컬럼간의 상관관계 표시</summary>

```python
num_mpg.corr()
```

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
      <th>mpg</th>
      <th>cylinders</th>
      <th>displacement</th>
      <th>horsepower</th>
      <th>weight</th>
      <th>acceleration</th>
      <th>model_year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mpg</th>
      <td>1.000000</td>
      <td>-0.775396</td>
      <td>-0.804203</td>
      <td>-0.778427</td>
      <td>-0.831741</td>
      <td>0.420289</td>
      <td>0.579267</td>
    </tr>
    <tr>
      <th>cylinders</th>
      <td>-0.775396</td>
      <td>1.000000</td>
      <td>0.950721</td>
      <td>0.842983</td>
      <td>0.896017</td>
      <td>-0.505419</td>
      <td>-0.348746</td>
    </tr>
    <tr>
      <th>displacement</th>
      <td>-0.804203</td>
      <td>0.950721</td>
      <td>1.000000</td>
      <td>0.897257</td>
      <td>0.932824</td>
      <td>-0.543684</td>
      <td>-0.370164</td>
    </tr>
    <tr>
      <th>horsepower</th>
      <td>-0.778427</td>
      <td>0.842983</td>
      <td>0.897257</td>
      <td>1.000000</td>
      <td>0.864538</td>
      <td>-0.689196</td>
      <td>-0.416361</td>
    </tr>
    <tr>
      <th>weight</th>
      <td>-0.831741</td>
      <td>0.896017</td>
      <td>0.932824</td>
      <td>0.864538</td>
      <td>1.000000</td>
      <td>-0.417457</td>
      <td>-0.306564</td>
    </tr>
    <tr>
      <th>acceleration</th>
      <td>0.420289</td>
      <td>-0.505419</td>
      <td>-0.543684</td>
      <td>-0.689196</td>
      <td>-0.417457</td>
      <td>1.000000</td>
      <td>0.288137</td>
    </tr>
    <tr>
      <th>model_year</th>
      <td>0.579267</td>
      <td>-0.348746</td>
      <td>-0.370164</td>
      <td>-0.416361</td>
      <td>-0.306564</td>
      <td>0.288137</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>

</details>

<br>

* 상관관계 히트맵

```python
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(16, 5))

#  기본 그래프 [Basic Correlation Heatmap]
sns.heatmap(num_mpg.corr(), ax=ax[0])
ax[0].set_title('Basic Correlation Heatmap', pad = 12) 

# 상관관계 수치 그래프 [Correlation Heatmap with Number]
sns.heatmap(num_mpg.corr(), vmin=-1, vmax=1, annot=True, ax=ax[1])
ax[1].set_title('Correlation Heatmap with Number', pad = 12)

plt.show()
```

<details> 
<summary>Output</summary>
    
![png](/images/python_visualiztion_basic_/output_49_0.png)  

위의 코드에서 `pad`는 히트맵과 타이틀의 간격설정이며,  
`set_title`의 인자를 설명하면 (히트맵을 만들 '데이터셋.corr()', 히트맵의 최소값, 최대값, 수치표현(bool값), 마지막인자는 확실하지는 않지만 앞의 히트맵 설정을 어떤 히트맵에 적용시킬지 묻는것 같다.)

</details>

<br>

<details> 
<summary>상관관계 배열 만들기</summary>

```python
# import numpy as np
# 윗단 코드에서 만들어진 num_mpg 사용
print(int(True))
np.triu(np.ones_like(num_mpg.corr()))
```

    1
    array([[1., 1., 1., 1., 1., 1., 1.],
           [0., 1., 1., 1., 1., 1., 1.],
           [0., 0., 1., 1., 1., 1., 1.],
           [0., 0., 0., 1., 1., 1., 1.],
           [0., 0., 0., 0., 1., 1., 1.],
           [0., 0., 0., 0., 0., 1., 1.],
           [0., 0., 0., 0., 0., 0., 1.]])

`np.triu(배열, k=0)`는 위 결과처럼 우하향 대각선이 있고 위 아래로 삼각형이 있다 생각했을때 아래쪽의 삼각형이 모두 0이 되는 함수이다.  
`k`의 숫자가 낮아질수록 삼각형은 한칸씩 작아진다.
위 결과에서 행과 열이 7칸이 된 이유는 `np.ones_like(num_mpg.corr())`의 행이 7개 이기때문인듯 하다.
~~확실히 모르겠음 질문 필수~~
<br><br>

```python
mask = np.triu(np.ones_like(num_mpg.corr(), dtype=np.bool))
print(mask)
```

    [[ True  True  True  True  True  True  True]
     [False  True  True  True  True  True  True]
     [False False  True  True  True  True  True]
     [False False False  True  True  True  True]
     [False False False False  True  True  True]
     [False False False False False  True  True]
     [False False False False False False  True]]

k 값을 바꿔 True와 False로 값을 준 경우.
</details>



```python
# 기본주석 생략
fig, ax = plt.subplots(figsize=(16, 5))

#  기본 그래프 [Basic Correlation Heatmap]
ax = sns.heatmap(num_mpg.corr(), mask=mask, 
                 vmin=-1, vmax = 1, 
                 annot=True, 
                 cmap="BrBG", cbar = True)
ax.set_title('Triangle Correlation Heatmap', pad = 16, size = 16)
fig.show()
```

<details> 
<summary>Output</summary>

    
![png](/images/python_visualiztion_basic_/output_52_0.png)

위의 글들을 모두 읽었음에도 단 하나 모르는 요소가 있다면 바로 `cmap`일 것이다.
`cmap`은 colormap을 줄인것으로 `cmap`의 종류는 상당히 많다.  
[이곳](https://codetorial.net/matplotlib/set_colormap.html)에 가면 상당히 잘 정리되어 있으니 `cmap`옵션을 사용할 때마다 요긴하게 쓸 수 있을것이다.

</details>



## Intermediate

### 페가블로그 코드

---

- https://jehyunlee.github.io/2020/08/27/Python-DS-28-mpl_spines_grids/


* 이 챕터의 내용은 코드가 너무 긺으로 시각화 결과물을 접지않고 코드를 접는형식으로 서술하겠음.

* 필수 코드이므로 생략을 생략
```python
import matplotlib.pyplot as plt
from matplotlib.ticker import (MultipleLocator, AutoMinorLocator, FuncFormatter)
import seaborn as sns
import numpy as np
```

<details> 
<summary>Code</summary>

```python
def plot_example(ax, zorder=0):
    ax.bar(tips_day["day"], tips_day["tip"], color="lightgray", zorder=zorder)
    ax.set_title("tip (mean)", fontsize=16, pad=12)

    # Values
    h_pad = 0.1
    for i in range(4):
        fontweight = "normal"
        color = "k"
        if i == 3:
            fontweight = "bold"
            color = "darkred"

        ax.text(i, tips_day["tip"].loc[i] + h_pad, f"{tips_day['tip'].loc[i]:0.2f}", 
                horizontalalignment='center', fontsize=12, fontweight=fontweight, color=color)

    # Sunday
    ax.patches[3].set_facecolor("darkred")
    ax.patches[3].set_edgecolor("black")

    # set_range
    ax.set_ylim(0, 4)
    return ax

def major_formatter(x, pos):
    return "{%.2f}" % x
formatter = FuncFormatter(major_formatter)

```


```python
tips = sns.load_dataset("tips")
tips_day = tips.groupby("day").mean().reset_index()
print(tips_day)
```

        day  total_bill       tip      size
    0  Thur   17.682742  2.771452  2.451613
    1   Fri   17.151579  2.734737  2.105263
    2   Sat   20.441379  2.993103  2.517241
    3   Sun   21.410000  3.255132  2.842105
    
</details>

---


<details> 
<summary>Code</summary>

```python
fig, ax = plt.subplots(figsize=(10, 6))
ax = plot_example(ax, zorder=2)
```
</details>

    
![png](/images/python_visualiztion_basic_/output_58_0.png)
    

<details> 
<summary>Code</summary>

```python
fig, ax = plt.subplots(figsize=(10, 6))
ax = plot_example(ax, zorder=2)

ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
ax.spines["left"].set_visible(False)
```

</details>
    
![png](/images/python_visualiztion_basic_/output_59_0.png)
    

<details> 
<summary>Code</summary>

```python
fig, ax = plt.subplots()
ax = plot_example(ax, zorder=2)

ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
ax.spines["left"].set_visible(False)

ax.yaxis.set_major_locator(MultipleLocator(1))
ax.yaxis.set_major_formatter(formatter)
ax.yaxis.set_minor_locator(MultipleLocator(0.5))
```

</details>
    
![png](/images/python_visualiztion_basic_/output_60_0.png)
    

<details> 
<summary>Code</summary>

```python
fig, ax = plt.subplots()
ax = plot_example(ax, zorder=2)

ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
ax.spines["left"].set_visible(False)

ax.yaxis.set_major_locator(MultipleLocator(1))
ax.yaxis.set_major_formatter(formatter)
ax.yaxis.set_minor_locator(MultipleLocator(0.5))
    
ax.grid(axis="y", which="major", color="lightgray")
ax.grid(axis="y", which="minor", ls=":")
```

</details>
    
![png](/images/python_visualiztion_basic_/output_61_0.png)
    


### 책 코드

---

<details> 
<summary>Code</summary>

```python
import matplotlib.pyplot as plt
from matplotlib.ticker import (MultipleLocator, AutoMinorLocator, FuncFormatter)
import seaborn as sns
import numpy as np

tips = sns.load_dataset("tips")
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(16, 5))

def major_formatter(x, pos):
    return "%.2f$" % x
formatter = FuncFormatter(major_formatter)

# Ideal Bar Graph
ax0 = sns.barplot(x = "day", y = 'total_bill', data = tips, 
                  ci=None, color='lightgray', alpha=0.85, zorder=2, 
                  ax=ax[0])
```

</details>

    
![png](/images/python_visualiztion_basic_/output_63_0.png)
    

<details> 
<summary>Code</summary>

```python
group_mean = tips.groupby(['day'])['total_bill'].agg('mean')
h_day = group_mean.sort_values(ascending=False).index[0]
h_mean = np.round(group_mean.sort_values(ascending=False)[0], 2)
print("The Best Day:", h_day)
print("The Highest Avg. Total Biil:", h_mean)
```

</details>

    The Best Day: Sun
    The Highest Avg. Total Biil: 21.41
    
<details> 
<summary>Code</summary>

```python
tips = sns.load_dataset("tips")
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(16, 5))

# Ideal Bar Graph
ax0 = sns.barplot(x = "day", y = 'total_bill', data = tips, 
                  ci=None, color='lightgray', alpha=0.85, zorder=2, 
                  ax=ax[0])

group_mean = tips.groupby(['day'])['total_bill'].agg('mean')
h_day = group_mean.sort_values(ascending=False).index[0]
h_mean = np.round(group_mean.sort_values(ascending=False)[0], 2)
for p in ax0.patches:
  fontweight = "normal"
  color = "k"
  height = np.round(p.get_height(), 2)
  if h_mean == height:
    fontweight="bold"
    color="darkred"
    p.set_facecolor(color)
    p.set_edgecolor("black")
  ax0.text(p.get_x() + p.get_width()/2., height+1, height, ha = 'center', size=12, fontweight=fontweight, color=color)

fig.show()
```

</details>

    
![png](/images/python_visualiztion_basic_/output_65_0.png)
    

<details> 
<summary>Code</summary>

```python
import matplotlib.pyplot as plt
from matplotlib.ticker import (MultipleLocator, AutoMinorLocator, FuncFormatter)
import seaborn as sns
import numpy as np

tips = sns.load_dataset("tips")
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(16, 5))

def major_formatter(x, pos):
    return "%.2f$" % x
formatter = FuncFormatter(major_formatter)

# Ideal Bar Graph
ax0 = sns.barplot(x = "day", y = 'total_bill', data = tips, 
                  ci=None, color='lightgray', alpha=0.85, zorder=2, 
                  ax=ax[0])

group_mean = tips.groupby(['day'])['total_bill'].agg('mean')
h_day = group_mean.sort_values(ascending=False).index[0]
h_mean = np.round(group_mean.sort_values(ascending=False)[0], 2)
for p in ax0.patches:
  fontweight = "normal"
  color = "k"
  height = np.round(p.get_height(), 2)
  if h_mean == height:
    fontweight="bold"
    color="darkred"
    p.set_facecolor(color)
    p.set_edgecolor("black")
  ax0.text(p.get_x() + p.get_width()/2., height+1, height, ha = 'center', size=12, fontweight=fontweight, color=color)

ax0.set_ylim(-3, 30)
ax0.set_title("Ideal Bar Graph", size = 16)

ax0.spines['top'].set_visible(False)
ax0.spines['left'].set_position(("outward", 20))
ax0.spines['left'].set_visible(False)
ax0.spines['right'].set_visible(False)

ax0.yaxis.set_major_locator(MultipleLocator(10))
ax0.yaxis.set_major_formatter(formatter)
ax0.yaxis.set_minor_locator(MultipleLocator(5))

ax0.set_ylabel("Avg. Total Bill($)", fontsize=14)

ax0.grid(axis="y", which="major", color="lightgray")
ax0.grid(axis="y", which="minor", ls=":")

fig.show()
```

</details>
    
![png](/images/python_visualiztion_basic_/output_66_0.png)
    

<details> 
<summary>Code</summary>

```python
import matplotlib.pyplot as plt
from matplotlib.ticker import (MultipleLocator, AutoMinorLocator, FuncFormatter)
import seaborn as sns
import numpy as np

tips = sns.load_dataset("tips")
fig, ax = plt.subplots(nrows = 1, ncols = 2, figsize=(16, 5))

def major_formatter(x, pos):
    return "%.2f$" % x
formatter = FuncFormatter(major_formatter)

# Ideal Bar Graph
ax0 = sns.barplot(x = "day", y = 'total_bill', data = tips, 
                  ci=None, color='lightgray', alpha=0.85, zorder=2, 
                  ax=ax[0])

group_mean = tips.groupby(['day'])['total_bill'].agg('mean')
h_day = group_mean.sort_values(ascending=False).index[0]
h_mean = np.round(group_mean.sort_values(ascending=False)[0], 2)
for p in ax0.patches:
  fontweight = "normal"
  color = "k"
  height = np.round(p.get_height(), 2)
  if h_mean == height:
    fontweight="bold"
    color="darkred"
    p.set_facecolor(color)
    p.set_edgecolor("black")
  ax0.text(p.get_x() + p.get_width()/2., height+1, height, ha = 'center', size=12, fontweight=fontweight, color=color)

ax0.set_ylim(-3, 30)
ax0.set_title("Ideal Bar Graph", size = 16)

ax0.spines['top'].set_visible(False)
ax0.spines['left'].set_position(("outward", 20))
ax0.spines['left'].set_visible(False)
ax0.spines['right'].set_visible(False)

ax0.yaxis.set_major_locator(MultipleLocator(10))
ax0.yaxis.set_major_formatter(formatter)
ax0.yaxis.set_minor_locator(MultipleLocator(5))

ax0.set_ylabel("Avg. Total Bill($)", fontsize=14)

ax0.grid(axis="y", which="major", color="lightgray")
ax0.grid(axis="y", which="minor", ls=":")

ax0.set_xlabel("Weekday", fontsize=14)
for xtick in ax0.get_xticklabels():
  print(xtick)
  if xtick.get_text() == h_day:
    xtick.set_color("darkred")
    xtick.set_fontweight("demibold")
ax0.set_xticklabels(['Thursday', 'Friday', 'Saturday', 'Sunday'], size=12)

ax1 = sns.barplot(x = "day", y = 'total_bill', data = tips, 
                  ci=None, alpha=0.85, 
                  ax=ax[1])
for p in ax1.patches:
  height = np.round(p.get_height(), 2)
  ax1.text(p.get_x() + p.get_width()/2., height+1, height, ha = 'center', size=12)
ax1.set_ylim(-3, 30)
ax1.set_title("Just Bar Graph")

plt.show()
```

</details>

    Text(0, 0, 'Thur')
    Text(0, 0, 'Fri')
    Text(0, 0, 'Sat')
    Text(0, 0, 'Sun')
    


    
![png](/images/python_visualiztion_basic_/output_67_1.png)
    

