title: "PostgreSQL_on_Heroku"
tags:
  - heroku
  - postgreSQL
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-06-02'
---


# 헤로쿠에서 PostgreSQL 사용하기

### heroku에서 postgresql 설치

- 내 홈페이지의 Resources로 들어가기

![Untitled](/images/PostgreSQL_on_Heroku/Untitled.png)

- Add-ons 에 postgres 검색

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%201.png)

- Heroku Postgres설치를 위해 Submit Order Form 클릭
![Untitled](/images/PostgreSQL_on_Heroku/Untitled%202.png)

- Heroku Postgres 클릭
    
    ![Untitled](/images/PostgreSQL_on_Heroku/Untitled%203.png)
    
- 하면 현재 사용중인 DB현황을 볼 수 있다.

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%204.png)

### pgAdmin에서 heroku 와 연동

- pgAdmin 실행
    - 중간에 문제가 생긴다면ubuntu에서 service start를 해볼것

→`sudo service postgresql status`

→`sudo service postgresql start`

### **사용자 계정 Password 설정**

- 기본적으로 admin 사용자로 등록이 되어 있다. 보통 DB 초기 세팅 시에는 패스워드를 입력받아야 한다. ( password : 2016*****  )

→`sudo passwd postgres`

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%205.png)

- Servers(우클릭) → Register → Server… → 클릭

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%206.png)

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%207.png)

- General 탭의 Name 작성해주기

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%208.png)

- Connection탭의 주소 작성해주기
    - Heroku 홈페이지의 Datastores → Settings → View CreDentials… 클릭
        
        ![Untitled](/images/PostgreSQL_on_Heroku/Untitled%209.png)
        
         ——> 양식에 맞춰 작성해주기
        
        ![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2010.png)
        
         ——> Save 클릭
        
- 서버가 추가된것을 확인

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2011.png)

- Heroku에서 대여해준 DataBase들 목록중에서 나의 DB를 찾아야함.

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2012.png)

### Python으로 db에 데이터 입력하기

- 테이블을 생성하고 데이터를 입력하는 python 코드 작성 후 실행

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2013.png)

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2014.png)

- pgAdmin에서 확인
    - Query Tool 실행
    
    ![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2015.png)
    
    - test 테이블을 확인하는 쿼리 작성 후 실행
        
        ![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2016.png)
        
         ——> 성공!
        

### python에서 db쿼리가 잘 작동하는지 확인

- psycopg2 설치

```jsx
pip3 install psycopg2-binary
```

- 파이썬에서 test 테이블을 조회하는 코드를 작성 후 실행
- python3 명령어로 실행

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2017.png)

![Untitled](/images/PostgreSQL_on_Heroku/Untitled%2018.png)

 ——> 성공!

### 최종 코드

```python
# # 테이블 생성 + 데이터 집어넣기

import psycopg2

passwd = ''
db = psycopg2.connect(host='ec2-54-204-56-171.compute-1.amazonaws.com', dbname='d2p5j2up8o05rg',user='dywzgxybcyjnzu',password= passwd,port=5432)
cur=db.cursor()

# cur.execute("DROP TABLE test")

cur.execute("CREATE TABLE test (url varchar, title varchar);")

cur.execute("INSERT INTO test (url, title) VALUES (%s, %s);"
            , ("google.com", "구글입니다") )

db.commit()

print("good")
```

```python
# # 테이블 조회하기

import psycopg2

passwd = ''
db = psycopg2.connect(host='ec2-54-204-56-171.compute-1.amazonaws.com', dbname='d2p5j2up8o05rg',user='dywzgxybcyjnzu',password= passwd,port=5432)
cur=db.cursor()

cur.execute("SELECT * FROM test;")
rows = cur.fetchall()

print(rows)
print(rows[0][0])
print(type(rows))
```