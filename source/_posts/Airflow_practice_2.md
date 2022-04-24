---
title: "Airflow 실습02"
tags:
  - setting
  - airflow
categories:
  - setting
  - airflow
author: "minkuen"
date: '2022-04-21'
---

## 데이터베이스를 위한 아파치 에어플로 데이터 파이프라인 구축

실무 예제로 배우는 데이터 공학 87 ~ 91p

관리자 권한으로 실행 : ubuntu

→ elasticsearch 가동하기


![Untitled](/images/Airflow_practice_2/Untitled.png)

→ Kibana 가동하기 

![Untitled](/images/Airflow_practice_2/Untitled%201.png)

- 경로 이동, 가상 환경 진입

→ `cd ..`→ `cd ..`→ `cd mnt/c/airflow-test`

→ `source venv/bin/activate`

- 교재의 elastic search 버전을 참고하여 설치

→ `pip3 install elasticsearch==7.17.2`

![Untitled](/images/Airflow_practice_2/Untitled%202.png)

- 교재 80p
- 일단 vi 대신에 code . 를 사용한다.

→ `code .`

( 안 될 경우, Ubuntu를 다시 시작한다)

→ 코드 실행 시, VSCord가 자동으로 시작된다

![Untitled](/images/Airflow_practice_2/Untitled%203.png)

- 폴더 생성

→ 폴더 생성 : chapter04

→ 파일 생성 : e_search.py

→ 코드 작성

```
from elasticsearch import Elasticsearch
from elasticsearch import helpers
from faker import Faker

fake=Faker()
es = Elasticsearch() #or pi {127.0.0.1}

doc={"name": fake.name(),"street": fake.street_address(), "city": fake.city(),"zip":fake.zipcode()}

res=es.index(index="users",doc_type="doc",body=doc)
print(res)

doc={"query":{"match":{"_id":"pDYlOHEBxMEH3Xr-2QPk"}}}
res=es.search(index="users",body=doc,size=10)
print(res)
```

- 가상환경 가동 후 실행

→ 저장

→ 터미널 

→ `source venv/bin/activate`

→ `cd chapter04/`

→`python3 e_search.py`

- 교재 81p

→ 파일 작성 : e_search02.py

→ 코드 작성

```
from elasticsearch import Elasticsearch
from elasticsearch import helpers
from faker import Faker

fake=Faker()
es = Elasticsearch() #or pi {127.0.0.1}

actions = [
  {
    "_index": "users",
    "_type": "doc",
    "_source": {
	"name": fake.name(),
	"street": fake.street_address(),
	"city": fake.city(),
	"zip":fake.zipcode()}
  }
  for x in range(998) # or for i,r in df.iterrows()
]

response = helpers.bulk(es, actions)
print(response)
```

→ 저장 후 실행

→ `python3 e_search02.py`

→ 다음과 같이 (998,[]) 출력되면 성공

![Untitled](/images/Airflow_practice_2/Untitled%204.png)

- Kibana 페이지 실행

→ 주소창에 입력 : localhost:5601/

→ 메뉴바

→ Stack Management

![Untitled](/images/Airflow_practice_2/Untitled%205.png)

→ Index Patterns

![Untitled](/images/Airflow_practice_2/Untitled%206.png)

→ Create index pattern

→ 이름 : users

![Untitled](/images/Airflow_practice_2/Untitled%207.png)

→ Create index pattern

![Untitled](/images/Airflow_practice_2/Untitled%208.png)

→ 햄버거 메뉴바 열기

→ Discover 

![Untitled](/images/Airflow_practice_2/Untitled%209.png)

→ 앞에서 추가한 index의 문서를 확인할 수 있다.

![Untitled](/images/Airflow_practice_2/Untitled%2010.png)

### 데이터 저장소

- RDBMS

— 종류 : Oracle, PostgreSQL, MySQL, 빅쿼리(구글),...

— 표준 SQL (하나를 잘 알면, 거의 비슷!)

- NoSQL

— 종류 : Elasticsearch, 몽고 DB (무료 버전)

어려운 것 조회 하는 방법이 RDMBS ≠ NoSQL 다름 (완전 다름!)

- Reference 
  - 실무 예제로 배우는 데이터 공학
  - [Elasticsearch (notion.so)](https://www.notion.so/Elasticsearch-36546819d5b44c778d6a9c08f18c8339)