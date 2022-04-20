---
title: "PSQL Install"
tags:
  - setting
  - postgreSQL
categories:
  - setting
  - postgreSQL
author: "minkuen"
date: '2022-04-18'
---

## ****PostgreSQL Installation on WSL2 and Windows****

[PostgreSQL Installation on WSL2 and Windows - Data Science | DSChloe](https://dschloe.github.io/sql/postgreslq_wsl2/)

(password : 2016*****)

( 서버 password : postgres )

### **개요**

- WSL2에서 PostgreSQL을 설치한다.
- pgAdmin은 Windows에 설치한다.

### **터미널 업그레이드**

- 먼저 WSL 터미널을 열고, Ubuntu 패키지를 모두 업데이트 및 업그레이드를 한다.

Windows Terminal → wsl bash 

또는

Ubuntu → ..cd → ..cd

→`sudo apt update`

→`sudo apt-get upgrade`

### **PostgreSQL Installation in WSL2**

- 이번에는 WSL2에서 PostgreSQL을 설치한다. 설치가 종료되면, 반드시 버전을 확인한다.

→`sudo apt install postgresql postgresql-contrib`

→`psql --version`

- 설치 이후에는 Database를 접근 가능하도록 활성화해야 한다.
    - 포트가 활성화 되어 있지 않다면 아래와 같은 메시지가 나타날 것이다.

→`sudo service postgresql status`

- 이번에는 활성화를 해보도록 한다. 온라인이라는 메시지가 나타난다면 활성화가 되었다는 것을 의미한다.

→`sudo service postgresql start`

→`sudo service postgresql status`

이번에는 활성화된 데이터베이스를 종료시킨다

→`sudo service postgresql stop`

→`sudo service postgresql status`

### **사용자 계정 Password 설정**

- 기본적으로 admin 사용자로 등록이 되어 있다. 보통 DB 초기 세팅 시에는 패스워드를 입력받아야 한다. ( password : 2016*****  )

→`sudo passwd postgres`

• 여기까지 했다면, WSL2에서 추가로 설정할 것은 더 없다.

### **pgAdmin Installation on Windows**

- 이번에는 pgAdmin을 설치한다. (최신버전 설치, pgAdmin 4 v6.8)웹사이트 : **[https://www.pgadmin.org/download/pgadmin-4-windows/](https://www.pgadmin.org/download/pgadmin-4-windows/)**
- 설치 할 때는 관리자로 실행하며, 아래 그림과 나타난다면, install for all users를 선택한다.

![Untitled](/images/PSQL_install/Untitled.png)

- 설치가 완료된 뒤에는 pgAdmin 이 검색되는지를 확인한다.
- WSL2 에서 PostgreSQL 서비스를 활성화 해야 한다.
- 처음 실행 시 나타나는 화면에 나오는 Password 설정
- WSL2에서 설정한 Password를 입력한다. (password : 2016*****)
    - 이번에는 서버를 설정하도록 한다  ( 서버 password : postgres )

![Untitled](/images/PSQL_install/Untitled%201.png)

server 우 클릭

→ register → server

→ 내용 작성

→ General Tab 의 Name에 입력 : test

![Untitled](/images/PSQL_install/Untitled%202.png)

- connection tab 에서 작성

→ host 에 입력 : 127.0.0.1 

→ Password는 WSL2에서 입력했던 Password를 입력한다.

- 만약에 아래와 같이 Password 에러가 나면 계정 Password를 변경 또는 재 지정해야 한다.
    - 참고자료 : **[https://stackoverflow.com/questions/12720967/how-to-change-postgresql-user-password/12721095#12721095](https://stackoverflow.com/questions/12720967/how-to-change-postgresql-user-password/12721095#12721095)**

![Untitled](/images/PSQL_install/Untitled%203.png)

서비스를 활성화한다.

`sudo service postgresql start`

다음과 같이 Password를 설정하도록 한다

`sudo -u postgres psql -c "ALTER USER postgres PASSWORD '<new-password>';"`

`sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';"`

- 위 설정이 끝난 후, 재 접속하면 정상적으로 접근이 되는 것을 확인할 수 있다.
- 비밀번호가 `postgres` 로 변경되었다.

### **DB 생성 및 확인**

- test 서버에 접속을 했다면, 이제 DB생성을 해본 후, pgAdmin과 WSL2에서 각각 확인을 한다.
- 먼저, Database에서 마우스 우클릭 후, 아래와 같이 순차적으로 클릭한다.

Databases 우클릭

→ create → database..

→ 새로운 데이터베이스명은 dataengineering으로 명명한다.

![Untitled](/images/PSQL_install/Untitled%204.png)

- 이번에는 아래 그림과 같이 dataengineering 데이터베이스의 노드 중 shemas를 확장하고 다시 public을 확장한다.

![Untitled](/images/PSQL_install/Untitled%205.png)

dataengineering 

→ shemas

→ public

→ tables 우클릭

→ Create → Table

→ General 탭 Name 입력 :  users

→ Column 탭에서는 아래와 같이 테이블 열을 추가한다

→ 우측의 + 버튼을 이용한다.

![Untitled](/images/PSQL_install/Untitled%206.png)

wsl2 가상환경 : postgresql 서버 & DB

윈도우 : GUI - pgAdmin

- 이번에는 psql에 접속 후 dataengineering DB와 생성된 테이블을 조회하는 쿼리를 실행한다.
    - dataengineering 테이블이 조회되는지 확인한다.
    
    ![Untitled](/images/PSQL_install/Untitled%207.png)
    
    → `sudo -u postgres psql`  (psql 접속 명령)
    
    → postgres=#  형태의 프롬프트가 출력된다.
    
    → 그림 맨 밑줄처럼  `\l` 을 입력하고 enter
    
    → dataengineering 이 출력되면 성공
    

이번에는 생성된 dataengineering DB에 연결 후, 테이블을 조회한다

→ `sudo -u postgres psql`  ( psql에 접속)

→ postgres=#  형태의 프롬프트가 출력된다.

→ `\c dataengineering` 

→ (dataengineering DB에 연결되어

    dataengineering=# 형태로 바뀐다. )

→  `\dt`

→ users 테이블이 출력 되면 성공

→ `\q` 하여 빠져나온다.

→ `sudo service postgresql stop` 하여 DB 종료

→ 반드시 종료하자

### Refefence

- [PostgreSQL Installation on WSL2 and Windows - Data Science | DSChloe](https://dschloe.github.io/sql/postgreslq_wsl2/)
- **Set up PostgreSQL on WSL2 and Access with pgAdmin on Windows,** **[https://chloesun.medium.com/set-up-postgresql-on-wsl2-and-connect-to-postgresql-with-pgadmin-on-windows-ca7f0b7f38ab](https://chloesun.medium.com/set-up-postgresql-on-wsl2-and-connect-to-postgresql-with-pgadmin-on-windows-ca7f0b7f38ab)**
- **PostgreSQL Show Tables,** **[https://www.postgresqltutorial.com/postgresql-administration/postgresql-show-tables/](https://www.postgresqltutorial.com/postgresql-administration/postgresql-show-tables/)**
- 실무 예제로 배우는 데이터 공학

SQLAlchemy : 반드시 사용하자.

나중에라도 파이썬에 연결하여 사용한다.

[https://www.sqlalchemy.org/](https://www.sqlalchemy.org/)

[postgreSQL 실습](https://www.notion.so/postgreSQL-2a8e7bf9156b4514b28aafbd93421a79)

[postgreSQL 실습_2](https://www.notion.so/postgreSQL-_2-e4bd3b39f87c457889449caee9f7bc2d)