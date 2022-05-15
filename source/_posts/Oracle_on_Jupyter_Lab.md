---
title: "Oracle on Jupyter Lab"
tags:
  - oracle
categories:
  - setting
  - oracle
author: "minkuen"
date: '2022-05-11'
---

### 사전준비

- Oracle 설치
- SQL Developer 설치
- Oracle DB 접속 설정

### Jupyter Lab에서 설치 및 설정 진행

- 순서대로 작성하고 실행한다.
- ipython 설치

`pip install ipython-sql`

- cx_Oracle 설치

`pip install cx_Oracle`

- 로드

`%load_ext sql`

- DB 연동
    - DB 접속 선택을 참고하여 코드를 작성한다.
    
    ```sql
    # Oracle
    %sql oracle://user_name:password@127.0.0.1:port_number/db
    ```
    
    - 코드 사용 예시 : `%sql oracle://ora_user:evan@127.0.0.1:1521/myoracle`
    - user_name, password, port_number, db는 본인의 DB 접속 선택을 참고한다.

![Untitled](/images/Oracle_on_Jupyter_Lab/Untitled.png)

- 여기까지 코드들을 실행하면 다음과 같이 출력된다.

![Untitled](/images/Oracle_on_Jupyter_Lab/Untitled%201.png)

### 실행

- 쿼리 작성 후 실행
    - 단, `%%sql` 을 붙여야 한다.
    - 쿼리 끝에 세미콜론(;)을 붙여서는 안 된다.

![Untitled](/images/Oracle_on_Jupyter_Lab/Untitled%202.png)

- 정상적으로 실행되었다.

- Reference
    - [https://rain-grouse-1fe.notion.site/Jupyter-Notebook-SQL-0973777326e2426da0797f75c09ad0bb](https://www.notion.so/Jupyter-Notebook-SQL-0973777326e2426da0797f75c09ad0bb)
    - [jupyter lab에서 ipython-sql로 DB 접속하기(SQL Server, MySQL, postgreSQL) :: 박범준 (tistory.com)](https://95pbj.tistory.com/47)