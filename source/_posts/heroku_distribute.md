---
title: "Heroku 배포"
tags:
  - heroku
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-05-27'
---

## **개요**

- 카카오톡 챗봇 만들기를 Python + FLASK를 통해 간단한 튜토리얼을 만들어본다.

## **사전준비**

- OBT 참여승인을 받아야 한다.

## **기본설정**

- 카카오톡 챗봇 버튼 클릭 후, 봇 이름 생성
    - [봇 만들기] - [카카오톡 챗봇]

- 카카오톡 채널 연결을 진행한다.

![Untitled](/images/heroku_distribute/Untitled.png)

- 바탕화면 폴더 생성 : chatbotnos
- 깃허브 Repo 생성 : chatbotnos

![Untitled](/images/heroku_distribute/Untitled%201.png)

- heroku app 생성 : chatbotnos

![Untitled](/images/heroku_distribute/Untitled%202.png)

### 나만의 주소 생성됨 : [https://chatbotnos.herokuapp.com/](https://chatbotnos.herokuapp.com/)

### 로컬 폴더 생성

- VSCord에서 c 드라이브 경로에 폴더 생성 : chatbotnos
    - 폴더 우클릭 : git bash here
    - `git clone [ 깃허브 repo 주소 ]`

### 가상환경 생성

- 가상환경 생성
    - `pip3 install virtualenv`
    - `virtualenv venv` # 노트북으로 진행. 환경설정에 부족한 부분이 있는지 실패

- virtualenv 명령 실패 시, 다음 명령으로 대응
    - 가상환경 생성 : `python -m venv venv`
    - 가상환경 진입 : `source venv/Scripts/activate`

![Untitled](/images/heroku_distribute/Untitled%203.png)

### Heroku App 구축

- 간단하게 app 파일을 만들어 Heroku App URL을 확보해보자.
- 파일 생성 : chatbotnos/app/main.py
    - `mkdir app`
    - `cd app`
    - `vi main.py`

- 다음 코드 작성
- 들여쓰기 주의 !!!!

```python
from flask import Flask
 
app = Flask(__name__)
  
@app.route('/')
def hello_world():
        return 'Hello, World!'
```

- 파일 생성 : chatbotnos/wsgi.py
    - app은 폴더를 말하고, main은 main.py를 말한다.
    - 해당 파일에 코드 작성 : `vi wsgi.py`

```python
from app.main import app

if __name__ == "__main__":
        app.run(threaded=True, port=5000)
```

- Procfile 파일 작성 (오타 x. profile x)
    - 카카오톡 챗봇에서는 포트번호를 입력을 해줘야 한다.
        - localhost:5000 처럼 명시적으로 입력해주는 것으로 생각하면 된다.

- 파일 생성 : chatbotnos/Procfile
    - `vi Procfile`
    - 코드 작성

```python
web: gunicorn --bind 0.0.0.0:$PORT wsgi:app
```

- 파일 생성 : chatbotnos/runtime.txt
    - `vi runtime.txt`

```python
python-3.8.5
```

### heroku CLI 설치

- 구글링 : heroku cli
    - install the Heroky CLI

![Untitled](/images/heroku_distribute/Untitled%204.png)

- 설치 진행

![Untitled](/images/heroku_distribute/Untitled%205.png)

- 디폴트 설정으로 설치

![Untitled](/images/heroku_distribute/Untitled%206.png)

### Heroku login

- Heroku CLI 설치 후 로그인을 진행해야 한다.
- cmd에서  실행

```python
heroku login
```

- press any key : 아무 키나 입력한다

![Untitled](/images/heroku_distribute/Untitled%207.png)

- 로그인 창이 출력된다.

![Untitled](/images/heroku_distribute/Untitled%208.png)

- 로그인 진행

### .gitignore 파일 작성

[https://www.toptal.com/developers/gitignore](https://www.toptal.com/developers/gitignore) 

- 해당 링크에서 키워드 입력하고 ‘생성’
- 키워드 : virtualenv, vs

![Untitled](/images/heroku_distribute/Untitled%209.png)

- 복사 : ctrl + A
- .gitignore 파일에 붙여넣어 완성

![Untitled](/images/heroku_distribute/Untitled%2010.png)

 

### Requirements.txt 파일

- 다음 코드를 실행하여 생성한다.
- 하는 김에 gunicorn 설치
    - `pip install -r requirements.txt`
    - `pip install gunicorn`
    - `pip freeze > requirements.txt`

### Heroku 배포

- Heroku Project 생성
    - 다른 사용자들과 이름 다르게 진행! = 유일값
    - 언더바 사용불가 : name_name (x)
    - 로컬 폴더명 == Github Repo == Heroku Project 이름

- 위 코드에서 **이미 있는 이름이라 뜨면** 다음 코드 실행
- 기존 Existing App과 연동하려면 배포 전 아래 코드를 선 실행 후, 배포를 진행한다.
    - `heroku git:remote -a chatbotnos`

```python
git init
```

- heroku 배포 메뉴얼의 코드

```python
$ heroku git:clone -a chatbotnos 
$ cd chatbotnos
```

- Heroku 배포
    - Heroku에 배포하기 위해서는 크게 아래 코드만 기억한다.

```python
$ git add .
$ git commit -am "your_message" # 이 부분만 자유롭게 쓸 수 있다.
$ git push origin main ## Github Repository에 업데이트
$ git push heroku main ## Heroku 코드 배포
```

- 배포 완료

![Untitled](/images/heroku_distribute/Untitled%2011.png)

### 로그 확인

- 오류가 발생할 경우에 사용
- 오류 로그를 확인하고 코드를 수정하는 용도
    - `heroku logs --tail`

- Reference
    - [https://dschloe.github.io/python/kakao_chatbot/chatbot_calculator/](https://dschloe.github.io/python/kakao_chatbot/chatbot_calculator/)