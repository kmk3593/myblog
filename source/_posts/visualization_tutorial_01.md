---
title: "visualization_tutorial_01"
tags:
  - python
categories:
  - python
  - library
  - visualization
author: "minkuen"
date: '2022-03-26'
---


# 데이터 시각화

### 데이터 시각화의 기본 조건
- 목적에 맞는 선정
  - 선형 그래프, 막대 그래프, 산점도, 박스플롯 etc
- 환경에 맞는 도구 선택
  - 코드 기반(R, Python)
  - 프로그램 기반 (시각화 툴)
    - Powr BI, Tableau, Excel
- 문맥(도메인)에 맞는 색과 도형 사용
  - 회사 로고 색깔
  - 색상의 일반적인 통념
    - 빨간색(경고), 초록색(안전)

- 코드 기반의 장점
  - 재현성 (함수화)
    - 여러 그래프 동시 작성 가능
    - 기존 코드 Ctrl + C/V
    - 데이터 크기 제한 없음 (RAM 조건 충족 시)

- Matplotlib 사용시 주의점
  - 객체 지향 API 문법을 사용하라
    - 숙달 시 다른 곳에도 사용 가능하다.
  - pyplot API 문법 사용은 자제하라.
    - 숙달해도 다른 문법과 차이가 있어서 쓸 데가 없다.

### 참고
- 데이터 분석 강의안_220307.pdf 63페이지. ‘시각화'
- Matplotlib : [https://matplotlib.org/stable/api/ticker_api.html](https://matplotlib.org/stable/api/ticker_api.html)
- seaborn : [https://seaborn.pydata.org/](https://seaborn.pydata.org/)

- 국새 파이썬 시각화 TOP 블로그 [Pega Devlog (jehyunlee.github.io)](https://jehyunlee.github.io/)
  - 이 분 블로그는 정독할 필요가 있으니, 즐겨찾기 해두자.


### 라이브러리 불러오기


```python
import matplotlib
import seaborn as sns
print(matplotlib.__version__)
print(sns.__version__)
```

    3.2.2
    0.11.2
    

### 시각화 그려보기


```python
import matplotlib.pyplot as plt

dates = [
    '2021-01-01', '2021-01-02', '2021-01-03', '2021-01-04', '2021-01-05',
    '2021-01-06', '2021-01-07', '2021-01-08', '2021-01-09', '2021-01-10'
]
min_temperature = [20.7, 17.9, 18.8, 14.6, 15.8, 15.8, 15.8, 17.4, 21.8, 20.0]
max_temperature = [34.7, 28.9, 31.8, 25.6, 28.8, 21.8, 22.8, 28.4, 30.8, 32.0]

# 앞으로 본인이 아래와 같이 코드를 작성해야 한다. 디폴트이므로 쓰고 보자.
fig, ax = plt.subplots(nrows = 1, ncols = 1, figsize=(10,6))

ax.plot(dates, min_temperature, label = "Min Temp.")
ax.plot(dates, max_temperature, label = "Max Temp.")
ax.legend()
plt.show()
```


    
![png](/images/visualization_tutorial_01/output_8_0.png)
    


### 주섹 데이터 다운로드 받기


```python
!pip install yfinance --upgrade --no-cache-dir
```

    Collecting yfinance
      Downloading yfinance-0.1.70-py2.py3-none-any.whl (26 kB)
    Requirement already satisfied: pandas>=0.24.0 in /usr/local/lib/python3.7/dist-packages (from yfinance) (1.3.5)
    Requirement already satisfied: numpy>=1.15 in /usr/local/lib/python3.7/dist-packages (from yfinance) (1.21.5)
    Requirement already satisfied: multitasking>=0.0.7 in /usr/local/lib/python3.7/dist-packages (from yfinance) (0.0.10)
    Collecting lxml>=4.5.1
      Downloading lxml-4.8.0-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (6.4 MB)
    [K     |████████████████████████████████| 6.4 MB 9.7 MB/s 
    [?25hCollecting requests>=2.26
      Downloading requests-2.27.1-py2.py3-none-any.whl (63 kB)
    [K     |████████████████████████████████| 63 kB 41.2 MB/s 
    [?25hRequirement already satisfied: python-dateutil>=2.7.3 in /usr/local/lib/python3.7/dist-packages (from pandas>=0.24.0->yfinance) (2.8.2)
    Requirement already satisfied: pytz>=2017.3 in /usr/local/lib/python3.7/dist-packages (from pandas>=0.24.0->yfinance) (2018.9)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.7/dist-packages (from python-dateutil>=2.7.3->pandas>=0.24.0->yfinance) (1.15.0)
    Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.7/dist-packages (from requests>=2.26->yfinance) (2.10)
    Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.7/dist-packages (from requests>=2.26->yfinance) (2021.10.8)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /usr/local/lib/python3.7/dist-packages (from requests>=2.26->yfinance) (1.24.3)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /usr/local/lib/python3.7/dist-packages (from requests>=2.26->yfinance) (2.0.12)
    Installing collected packages: requests, lxml, yfinance
      Attempting uninstall: requests
        Found existing installation: requests 2.23.0
        Uninstalling requests-2.23.0:
          Successfully uninstalled requests-2.23.0
      Attempting uninstall: lxml
        Found existing installation: lxml 4.2.6
        Uninstalling lxml-4.2.6:
          Successfully uninstalled lxml-4.2.6
    [31mERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
    google-colab 1.0.0 requires requests~=2.23.0, but you have requests 2.27.1 which is incompatible.
    datascience 0.10.6 requires folium==0.2.1, but you have folium 0.8.3 which is incompatible.[0m
    Successfully installed lxml-4.8.0 requests-2.27.1 yfinance-0.1.70
    


```python
import yfinance as yf
data = yf.download("AAPL", start="2019-08-01", end="2020-08-01")
ts = data['Open']
print(ts.head())
print(type(ts))   # Series 타입니다.
```

    [*********************100%***********************]  1 of 1 completed
    Date
    2019-08-01    53.474998
    2019-08-02    51.382500
    2019-08-05    49.497501
    2019-08-06    49.077499
    2019-08-07    48.852501
    Name: Open, dtype: float64
    <class 'pandas.core.series.Series'>
    

### pyplot 형태


```python
import matplotlib.pyplot as plt
plt.plot(ts)
plt.title("")
plt.title("Stock Market of APL")
plt.xlabel("Date")
plt.ylabel("Open Pric")
plt.show()
```


    
![png](/images/visualization_tutorial_01/output_13_0.png)
    


### 객체지향으로 그리기
- fix 는 테두리
- 나머지는 ax가 표현


```python
import matplotlib.pyplot as plt

fix, ax = plt.subplots()
ax.plot(ts)
#ax.title("Stock Market of APL")
#ax.xlabel("Date")
#ax.ylabel("Open Pric")
plt.show()
```


    
![png](/images/visualization_tutorial_01/output_15_0.png)
    


### 막대 그래프


```python
import matplotlib.pyplot as plt
import numpy as np
import calendar

month_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
sold_list = [300, 400, 550, 900, 600, 960, 900, 910, 800, 700, 550, 450]

fix, ax = plt.subplots(figsize = (10, 6))
barplots = ax.bar(month_list, sold_list) # bar() 로 막대 그래프 생성

print("barplots : ", barplots)

for plot in barplots:
  print(plot)
  #print(plot.get_height())
  #print(plot.get_x())
  #print(plot.get_y())
  #print(plot.get_width())
  height = plot.get_height()
  ax.text(plot.get_x() + plot.get_width()/2., height, height, ha = 'center', va = 'bottom')  

plt.xticks(month_list, calendar.month_name[1:13], rotation = 90)
plt.show()
```

    barplots :  <BarContainer object of 12 artists>
    Rectangle(xy=(0.6, 0), width=0.8, height=300, angle=0)
    Rectangle(xy=(1.6, 0), width=0.8, height=400, angle=0)
    Rectangle(xy=(2.6, 0), width=0.8, height=550, angle=0)
    Rectangle(xy=(3.6, 0), width=0.8, height=900, angle=0)
    Rectangle(xy=(4.6, 0), width=0.8, height=600, angle=0)
    Rectangle(xy=(5.6, 0), width=0.8, height=960, angle=0)
    Rectangle(xy=(6.6, 0), width=0.8, height=900, angle=0)
    Rectangle(xy=(7.6, 0), width=0.8, height=910, angle=0)
    Rectangle(xy=(8.6, 0), width=0.8, height=800, angle=0)
    Rectangle(xy=(9.6, 0), width=0.8, height=700, angle=0)
    Rectangle(xy=(10.6, 0), width=0.8, height=550, angle=0)
    Rectangle(xy=(11.6, 0), width=0.8, height=450, angle=0)
    


    
![png](/images/visualization_tutorial_01/output_17_1.png)
    



```python
### 산점도
```


```python
import seaborn as sns

tips = sns.load_dataset("tips") # 영수증 데이터이다.
# print(tips.info())
x = tips['total_bill']
y = tips['tip']

# 산점도
flg, ax = plt.subplots(figsize=(10, 6))
ax.scatter(x,y)
ax.set_xlabel('Total Bill')
ax.set_ylabel('Tip')
plt.show
```




    <function matplotlib.pyplot.show>




    
![png](/images/visualization_tutorial_01/output_19_1.png)
    



```python
label, data = tips.groupby('sex')
# print(label)
# print(data)

tips['sex_color'] = tips['sex'].map({'Male': '#2521F6', 'Female': '#EB4036'})
#print(tips.head())

fix, ax = plt.subplots(figsize=(10,6))
for label, data in tips.groupby('sex'):
  ax.scatter(data['total_bill'], data['tip'], label=label, color=data['sex_color'],alpha=0.5)
  ax.set_xlabel('Total Bill')
  ax.set_ylabel('Tip')

ax.legend() # 범례
plt.show()
```


    
![png](/images/visualization_tutorial_01/output_20_0.png)
    


### Seaborn
- 다음 코드는 위와 같은 결과가 나온다. 하지만 더 간단하다.


```python
import matplotlib.pyplot as plt
import seaborn as sns

tips = sns.load_dataset("tips")
# print(tips.info())

fig, ax =plt.subplots(figsize=(10,6))
sns.scatterplot(x='total_bill', y = 'tip', hue='sex', data = tips)
plt.show()
```


    
![png](/images/visualization_tutorial_01/output_22_0.png)
    



```python
# 두 개의 그래프를 동시에 표현
fig, ax = plt.subplots(nrows=1, ncols=2, figsize=(15,5))

sns.regplot(x = "total_bill", y = "tip", data = tips, ax=ax[1], fit_reg = True)
ax[1].set_title("with linear regression line")

sns.regplot(x = "total_bill", y = "tip", data = tips, ax=ax[0], fit_reg = False)
ax[0].set_title("without linear regression line")

plt.show()
```


    
![png](/images/visualization_tutorial_01/output_23_0.png)
    


### 막대 그래프 그리기 seaborn 방식


```python
sns.countplot(x="day", data=tips)
plt.show()
```


    
![png](/images/visualization_tutorial_01/output_25_0.png)
    



```python
print(tips['day'].value_counts().index)
print(tips['day'].value_counts().values)
print(tips['day'].value_counts(ascending=True))
```

    CategoricalIndex(['Sat', 'Sun', 'Thur', 'Fri'], categories=['Thur', 'Fri', 'Sat', 'Sun'], ordered=False, dtype='category')
    [87 76 62 19]
    Fri     19
    Thur    62
    Sun     76
    Sat     87
    Name: day, dtype: int64
    


```python
flg, ax = plt.subplots()
ax = sns.countplot(x="day", data=tips, order = tips['day'].value_counts().index)

for plot in ax.patches: # matplotlib 와 같은 역할을 수행한다.
  print(plot)
  height = plot.get_height()
  ax.text(plot.get_x() + plot.get_width()/2., height, height, ha = 'center', va = 'bottom')  

ax.set_ylim(-5, 100)
plt.show()
```

    Rectangle(xy=(-0.4, 0), width=0.8, height=87, angle=0)
    Rectangle(xy=(0.6, 0), width=0.8, height=76, angle=0)
    Rectangle(xy=(1.6, 0), width=0.8, height=62, angle=0)
    Rectangle(xy=(2.6, 0), width=0.8, height=19, angle=0)
    


    
![png](/images/visualization_tutorial_01/output_27_1.png)
    


### 어려운 시각화 그래프


```python
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
from matplotlib.ticker import (MultipleLocator, AutoMinorLocator, FuncFormatter)

def major_formatter(x, pos):
  return "%.2f$" % x

formatter = FuncFormatter(major_formatter)

tips = sns.load_dataset("tips")
fig, ax = plt.subplots(nrows=1, ncols=2, figsize=(16, 6))


ax0 = sns.barplot(x="day", y="total_bill", data=tips,
            ci=None, color='lightgray', alpha=0.85, zorder=2,  # alpha는 투명도
            ax = ax[0])
# groupby
group_mean = tips.groupby(['day'])['total_bill'].agg('mean')
#print(group_mean)

h_day = group_mean.sort_values(ascending=False).index[0]  # sun 표시
#print(h_day)
h_mean = group_mean.sort_values(ascending=False).values[0]  
print(h_mean)

# text 추가
for plot in ax0.patches:
  height = np.round(plot.get_height(), 2)
  # print(height)

  # Default
  fontweight = "normal"
  color = "k"
  if h_mean == height:
    fontweight = "bold"
    color = "darkred"
    plot.set_facecolor(color)
    plot.set_edgecolor("black")

  ax0.text(plot.get_x() + plot.get_width()/2.,
           height + 1, height, 
           ha = 'center', size=12, fontweight = fontweight, color = color)

# 축 수정
ax0.set_ylim(-3, 30)
ax0.set_title("Bar Graph", size = 16)

# 테두리(spines) 삭제
ax0.spines['top'].set_visible(False)
ax0.spines['left'].set_position(("outward", 20))
ax0.spines['left'].set_visible(False)
ax0.spines['right'].set_visible(False)

ax0.yaxis.set_major_locator(MultipleLocator(10))
ax0.yaxis.set_major_formatter(formatter)
ax0.yaxis.set_minor_locator(MultipleLocator(5))

ax0.set_ylabel("Avg. Total Bill($)", fontsize=14)

ax0.grid(axis="y", which="major", color = "lightgray")
ax0.grid(axis="y", which="major", ls = ":")

for xtick in ax0.get_xticklabels():
  print(xtick)
  if xtick.get_text() == h_day:
    xtick.set_color("darkred")
    xtick.set_fontweight("demibold")

ax0.set_xticklabels(['Thursday', 'Friday', 'Saturday', 'Sunday'], size = 12)

plt.show()
```

    21.41
    Text(0, 0, 'Thur')
    Text(0, 0, 'Fri')
    Text(0, 0, 'Sat')
    Text(0, 0, 'Sun')
    


    
![png](/images/visualization_tutorial_01/output_29_1.png)
    

