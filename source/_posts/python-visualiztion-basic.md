---
title: 파이썬 시각화 기본
date: 2021-11-03 12:23:18
tags:
- Python
- Data Visualization
---

#Matplotlib
먼저 `yfinance`라이브러리를 사용하기 위해 설치
```shell
!pip install yfinance --upgrade --no-cache-dir
```  
<br>
`yfinance`로 데이터 조회

```python
import yfinance as yf
data - yf.download('AAPL', '2020-08-01', '2020-08-08')
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

</details>

가져온 데이터에서 원하는 컬럼 출력하기
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

애플주식이 이렇게 쌌었나 검색해보니 이게 맞음.
</details>

```python
import yfinance as yf
import matplotlib.pyplot as plt

data = yf.download('AAPL', '2019-08-01', '2020-08-01')
ts = data['Open']
plt.figure(figsize=(10,6))
plt.plot(ts)
plt.legend(labels=['Price'], loc='best')
plt.title('Stock Market fluctuation of AAPL') 
plt.xlabel('Date') 
plt.ylabel('Stock Market Open Price') 
plt.show()
```

