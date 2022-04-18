---
title: "Apache Nifi Install"
tags:
  - setting
  - apache
  - airflow
categories:
  - setting
  - airflow
author: "minkuen"
date: '2022-04-16'
---

# Apache airflow

## Apache-Airflow in windows 설치

• Windows WSL2에서 airflow를 설치한다.

****Step 1. Install pip on WSL****

• c드라이브에 들어간다.

관리자 권한으로 실행 : Ubuntu

→ `cd..`

→ `cd..`

→`cd mnt/c`

• 폴더를 만든다

→ `mkdir airflow-test`

→ `ls`

→ `cd airflow-test/`

• pip를 설치한다.

→ `sudo apt-get update && sudo apt-get upgrade`

→ `sudo apt install python3-pip`

****Step 2. Install virtualenv package****

• virtualenv 라이브러리를 설치한다.

→ `sudo pip3 install virtualenv`

****Step 3. Create a virtual environment****

• 이제 가상환경을 생성한다.

→ `virtualenv venv`

• 가상환경에 접속을 한다.

→ airflowtest 경로에서 해야 한다.

→ `source venv/bin/activate`

→ 경로 확인 

→ `pwd`

• 이번에는 .bashrc 파일을 수정한다.

• 파일을 열고, 맨 밑줄에 다음과 같은 코드를 추가한다.

→ `vi ~/.bashrc`

→ 내용 추가 : `export AIRFLOW_HOME=/mnt/c/airflow-test`

→ ESC → :wq 하여 저장

• 수정된 코드를 업데이트 하기 위해서는 아래와 같이 반영한다.

→ `source ~/.bashrc`

• 실제로 코드가 반영되었는지 확인하기 위해서는 다음과 같이 확인해본다.

• 다시 가상환경에 접속하고 수행

→`source venv/bin/activate`

→ `echo $AIRFLOW_HOME`

→ /mnt/c/airflow-test 출력되면 성공.

****Step 4. Apache Airflow 설치****

• PostgreSQL, Slack, Celery 패키지를 동시에 설치하는 코드를 작성한다.

→ `sudo apt-get update && sudo apt-get upgrade`

→ `pip3 install 'apache-airflow[postgres, slack, celery]'`

• airflow 실행을 위해 DB 초기화를 해줘야 한다.

→ `airflow db init`

• 실제로 잘 구현이 되었는지 확인하기 위해 webserver를 실행한다

→ `airflow webserver -p 8081`

→ port 번호 8081을 뜻한다.

• 그리고, 해당 링크 **[http://localhost:8081/login/](http://localhost:8081/login/)** 에 접속하면 아래와 같은 화면이 나타난다.

![Untitled](/images/Apache_Airflow_install/Untitled.png)

• 그런데, 여기에서 문제는 username을 생성하지 않았다. 따라서, username을 추가하도록 한다

→ ctrl + c 로 빠져나온다.

→ `airflow users create --username airflow --password airflow --firstname evan --lastname airflow --role Admin --email your_email@some.com`

 • 다시 웹서버 실행

→ `airflow webserver -p 8081`

• 해당 링크 **[http://localhost:8081/login/](http://localhost:8081/login/)** 에 접속

• 다음 정보로 로그인한다

→ id : airflow

password : airflow

→ 다음 화면이 나오면 성공.

![Untitled](/images/Apache_Airflow_install/Untitled%201.png)

### 설정완료 후에 가상환경 키는 법

ubuntu 

→ cd .. → cd .. → cd mnt/c → cd airflow-test 

→ `source venv/bin/activate`

- Reference :
[Setting up Apache-Airflow in Windows using WSL2 - Data Science | DSChloe](https://dschloe.github.io/settings/apache_airflow_using_wsl2/)

[Airflow 재설치 및 데이터 파이프라인 구축](https://www.notion.so/Airflow-57e8167632db4f09a62f7aa1d64a8d22)