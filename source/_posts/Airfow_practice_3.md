---
title: "Airflow 실습03"
tags:
  - setting
  - airflow
categories:
  - setting
  - airflow
author: "minkuen"
date: '2022-04-22'
---

## Elastic search 질의

- 교재 83p

관리자 권한으로 실행 : Ubuntu

→ 경로 이동 : ...airflow/

→ `source venv/bin/activate`

→ `code .`

→ VSCord가 자동 실행된다 

→파일 생성 : e_query.py

→ 코드 작성

```
import pandas as pd
from pandas.io.json import json_normalize
from elasticsearch import Elasticsearch

# Elasticsearch 객체 생성
es = Elasticsearch()

# 일래스틱서치에 보낼 문서 본문(질의 요청) JSON 객체를 만든다.
# Matchall 검색 사용
doc = {"query" : {"match_all": {}}}
res = es.search(index="users", body = doc, size = 500)
# print(res['hits']['hits'])

# 루프로 문서를 훑으면서 각 문서의 _source 필드만 출력한다.
# for doc in res['hits']['hits']:
#    print(doc['_source'])

# 질의 결과를 pandas DataFrame에 넣는 것도 가능
df = json_normalize(res['hits']['hits'])
print(df.head())
print(df.info())

print(df['_source.city'].value_counts())
```

### postgreSQL → Elastic search 데이터 전송

- 교재 88p
- Elastic search 가동된 상태에서 진행

→ 선행 학습 링크 참고 : [postgreSQL 실습 (notion.so)](https://www.notion.so/postgreSQL-2a8e7bf9156b4514b28aafbd93421a79)

- pgAdmin 준비된 상태에서 진행

→ 다음과 같이 출력되는 상태여야 한다.

![Untitled](/images/Airflow_practice_3/Untitled.png)

- VSCord 에서 작업
- 교재 88p

dags 폴더 아래에 파일 생성

→ 파일 생성 : airflodb.py

→ 코드 작성

`import datetime as dt`

`from datetime import timedelta`

`from airflow import DAG`

`from airflow.operators.bash import BashOperator`

`from airflow.operators.python import PythonOperator`

`import pandas as pd`

`import psycopg2 as db`

`from elasticsearch import Elasticsearch`

`print("Hello")`

→ 경로 이동 : (venv) kmk3593@DESKTOP-LNQ780K:/mnt/c/airflow-test/dags$ 

→ 실행

→ Hello 가 출력되었으므로 성공.

![Untitled](/images/Airflow_practice_3/Untitled%201.png)

- 코드 추가 작성
- 다음 내용을 airflodb.py에 작성한다.

```
import datetime as dt
from datetime import timedelta
from airflow import DAG
from airflow.operators.bash import BashOperator
from airflow.operators.python import PythonOperator

import pandas as pd
import psycopg2 as db
from elasticsearch import Elasticsearch

# queryPostgresql 지정
def queryPostgresql():
    conn_string="dbname='dataengineering' host='localhost' user='postgres' password='postgres'"
    conn=db.connect(conn_string)
    print("DB connecting....", conn)

    # 데이터 추출
    df = pd.read_sql("select name, city from users", conn)
    df.to_csv("postgresqldata.csv")
    print("----Data Saved----")

# insertElasticSearch
def insertDataElasticsearch():

    # Elastic 인스턴스 생성
    es = Elasticsearch()

    # 데이터 불러오기
    df = pd.read_csv("postgresqldata.csv")
    for i, r in df.iterrows():
        doc = r.to_json()
        res = es.index(
            index="frompostgresql"
            , doc_type="doc", body=doc
        )
        print(res)

# DAG를 위한 인수들을 지정
default_args = {
    'owner' : 'human',
    'start_date' : dt.datetime(2022, 4, 18),
    'retries' : 1,
    'retry_delay': dt.timedelta(minutes = 5)
}

with DAG('MyDBdag',
         default_args = default_args,
         schedule_interval = timedelta(minutes=5), # '0 * * * * ',
     ) as dag:

    getData = PythonOperator(
        task_id = "QueryPostgreSQL"
        , python_callable=queryPostgresql
    )

    insertData = PythonOperator(
        task_id = "InsertDataElasticsearch"
        , python_callable = insertDataElasticsearch
    )

getData >> insertData
```

- Airflow 가동

→ 저장 후 실행

→ `python3 airflodb.py`

→ airflow 실행

→ `airflow db init`

→(재시도할 경우, 실행 : `airflow db reset` )

→ Terminal 2개 준비하고 다음 명령 실행

→`airflow webserver -p 8080`

→`airflow scheduler`

→ 다음 주소로 진입

[http://localhost:8080/](http://localhost:8080/) 

→ Dags

→ 활성화 : MyDBdag

→ 더블 클릭 : MyDBdag

![Untitled](/images/Airflow_practice_3/Untitled%202.png)

→ Tree 

→ Update

→ 다음과 같이 출력되면 성공

![Untitled](/images/Airflow_practice_3/Untitled%203.png)

- Reference : 실무 예제로 배우는 데이터 공학