---
title: "Crawling data for chatbot"
tags:
  - crawling
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-06-01'
---



# 크롤링 - 인기종목 top5
- 챗봇에 필요한 자료 수집 목적
- 크롤링 코드를 먼저 작성하고 이후에 스킬 형태로 변환하여 사용할 예정

### 준비

- 크롤링할 url 선택 : [https://finance.naver.com/](https://finance.naver.com/)
- 추출할 정보를 우클릭 → 검사
- 표시된 html을 copy → copy selector

### 크롤링 코드

- url과 copy selector를 이용하여 코드 작성

```python
import requests
from bs4 import BeautifulSoup

import pandas as pd
import numpy as np
url = 'https://finance.naver.com/'

response = requests.get(url)
response.raise_for_status()
html = response.text
soup = BeautifulSoup(html, 'html.parser')
tbody = soup.select_one('#container > div.aside > div > div.aside_area.aside_popular > table > tbody')
trs = tbody.select('tr')
datas = []
for tr in trs:
    name = tr.select_one('th > a').get_text()
    current_price = tr.select_one('td').get_text() 
    change_direction = tr['class'][0]
    change_price = tr.select_one('td > span').get_text()
    datas.append([name, current_price, change_direction, change_price])

# print(datas)
df = pd.DataFrame(datas, columns=['종목명', '현재가', '등락', '전일대비' ], index=range(1, 6))
df = str(df)
print(df)
```

- 결과

![Untitled](/images/crawling_stock_top5/Untitled.png)

### 크롤링 코드-2-

- 앞의 코드를 조금만 바꿔보자

```python
import requests
from bs4 import BeautifulSoup

import pandas as pd
import numpy as np
url = 'https://finance.naver.com/'

response = requests.get(url)
response.raise_for_status()
html = response.text
soup = BeautifulSoup(html, 'html.parser')
tbody = soup.select_one('#container > div.aside > div > div.aside_area.aside_popular > table > tbody')

trs = tbody.select('tr')
datas = []
for tr in trs:
    name = tr.select_one('a').get_text()
    current_price = tr.select_one('td').get_text()
    change_direction = []
    if tr['class'][0] == "up":
        change_direction.append("▲")
    else:
        change_direction.append("▼")
    change_price = tr.select_one('span').get_text()
    datas.append([name, current_price, change_direction, change_price])

# print(datas)
df = pd.DataFrame(datas, columns=['종목명', '현재가', '등락', '전일대비' ], index=range(1, 6))
df = str(df)
print(df)
```

- 결과

![Untitled](/images/crawling_stock_top5/Untitled%201.png)

- Reference
    - [https://wikidocs.net/85739](https://wikidocs.net/85739)
    - [https://github.com/AHNDUHONG/Kakaotalk_Chatbot_Finance/blob/main/bash/top5_search.py](https://github.com/AHNDUHONG/Kakaotalk_Chatbot_Finance/blob/main/bash/top5_search.py)
    - [https://m.blog.naver.com/ksg97031/222070026332](https://m.blog.naver.com/ksg97031/222070026332)