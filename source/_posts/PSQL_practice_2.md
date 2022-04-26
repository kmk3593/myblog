---
title: "PSQL practice 02"
tags:
  - postgreSQL
categories:
  - SQL
  - postgreSQL
author: "minkuen"
date: '2022-04-24'
---

- 실무 예제로 배우는 데이터 공학 72p

- 파일 생성, 가상 환경 진입

관리자 권한으로 실행 : Ubuntu

→ `cd ..`→ `cd ..`→ `cd mnt/c`

→ `mkdir sql`

→ `cd sql`

→ `virtualenv venv`

→ `source venv/bin/activate`

- 라이브러리 설치

→ `pip3 install psycopg2-binary pandas faker`

→ `pip3 install pandas`

→ `pip3 install numpy`

- 실무 예제로 배우는 데이터 공학 72p 실습 진행

→ `mkdir chapter04`

→ `cd chapter04/`

→ 파일 생성 : vi createrecord.py

→ 내용 작성

```
import numpy as np
import pandas as pd
import psycopg2

print(np.__version__)
print(pd.__version__)
print(psycopg2.__version__)
```

→ 저장 후 코드 실행 : 버전 확인

→ `python3 createrecord.py`

→ 버전이 출력되면 성공

- 서비스 활성화

→`sudo service postgresql status`

→`sudo service postgresql stop`

→`sudo service postgresql start`

→ [createrecord.py](http://createrecord.py)에 다음 내용을 추가한다.

```
import psycopg2 as db
conn_string="dbname='dataengineering' host='localhost' user='postgres' password='postgres'"
# 집 pc에서는 201610974
conn=db.connect(conn_string)
cur=conn.cursor()
print("Connected:", cur)
```

→ 저장 후 실행

→ `python3 createrecord.py`

→ Connected : cursor.... 가 출력되면 성공.

- pgAdmin에서 실습 진행

→ 관리자 권한으로 실행 : pgAdmin

→ 로그인 비밀번호 : 201610974

    test 서버 비밀번호 : postgres

→ dataengineering → Schema → public → Tables → users우클릭

 → querytool

![Untitled](/images/PSQL_practice_2/Untitled.png)

→ 내용 작성 : `SELECT * FROM public.users;` 

→ F5 키로 실행한다.  

→ 다음과 같은 결과가 나온다.

![Untitled](/images/PSQL_practice_2/Untitled%201.png)

- 실무 예제로 배우는 데이터 공학 77p
- 데이터 추출
- Ubuntu에서 진행

→ [createrecord.py](http://createrecord.py)에 다음 내용을 추가한다.

```
# 데이터 추출 예제
print("step 2: ----- select -----")
query = "select * from users"
cur.execute(query)
for record in cur:
    print(record)
```

→ 저장 후 실행

→ `python3 createrecord.py`

→ [createrecord.py](http://createrecord.py)에 다음 내용을 추가한다.

`#print("step is done!")
print(cur.fetchall())
print("--------------")
print(cur.fetchmany(3))
print("--------------")
print(cur.fetchone())
print("----")
print(cur.rowcount)`

→ 저장 후 실행

→ `python3 createrecord.py`

→ [createrecord.py](http://createrecord.py)에 다음 내용을 추가한다.

```
# 78페이지 8번.
conn = db.connect(conn_string)
cur = conn.cursor()
f = open('fromdb.csv', 'w')
cur.copy_to(f, 'users', sep=',')
f.close()
```

→ 저장 후 실행

→ `python3 createrecord.py`

→ `ls`

→ fromdb.csv 파일이 생성되면 성공

→ [createrecord.py](http://createrecord.py)에 다음 내용을 추가한다.

#78p 11번 

`f = open('fromdb.csv', 'r')
f.read()
print("reading data is done!")`

→ 저장 후 실행

→ `python3 createrecord.py`

- 새 폴더 생성

→ 폴더 생성 : `vi querydf.py`

→ 내용 작성

`import psycopg2 as db
import pandas as pd
conn_string="dbname='dataengineering' host='localhost' user='postgres' password='postgres'"
conn=db.connect(conn_string)`

`df = pd.read_sql("select * from users", conn)
print(df.head())`

→ 저장 후 실행

→ `python3 querydf.py`

- Reference : 실무 예제로 배우는 데이터 공학