---
title: "Kakao Chatbot Skill with GoormIDE "
tags:
  - chatbot
  - kakao_chatbot
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-05-29'
---



# 스킬 사용 : 구름 IDE
- 구름 IDE를 이용한 스킬 사용 시도
- 그러나 구름IDE는 서버 실행 후 해당 창을 종료하면 스킬 사용이 불가능 = 편의성이 떨어짐
- 된다는 것만 확인하고 실제 챗봇 스킬에는 사용하지 않았다
- 단, Heroku에 비해 난이도는 낮은 편이라 수월하다는 장점이 있었다


### 사전준비

- 카카오 채널 생성
- 카카오 챗봇 오픈 빌더 OBT 승인
- 구름 IDE 가입 : [https://ide.goorm.io/](https://ide.goorm.io/)

### 컨테이너 생성

- 구름 IDE 가입 후에 컨테이너를 생성한다.

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled.png)

- 생성 시 설정 : 이름, 설명, 공개범위 등
- 추가 모듈/패키지 : 항목 모두 체크

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%201.png)

- 생성 완료

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%202.png)

- 컨테이너 실행

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%203.png)

### 파일 생성, 코드 작성

- 파일 생성 : application.py
- 랜덤으로 숫자를 생성하는 코드를 작성해본다

```python
from flask import Flask, jsonify
import sys 
import random
application = Flask(__name__)

@application.route("/")
def start():
    return "Hello goorm!!!"

@application.route("/random", methods=["POST"])
def random_function():
    response = {
        "version": "2.0",
        "template": {
            "outputs": [
                {
                    "simpleText": {
                        "text": str(random.randint(1,10))
                    }
                }
            ]
        }
    }
    return jsonify(response)

if __name__ == "__main__":
    application.run(host='0.0.0.0', port=int(sys.argv[1]), debug=True)
```

- 실행 : `python [application.py](http://application.py/) 80`
- 서버가 작동한다.
- 구름을 사용하는 동안에는 **이 창을 종료해서는 안 된다.**

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%204.png)

- 컨테이너 관리 창에서 ‘설정으로 가기’

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%205.png)

- 설정에서 주소 확인 가능
    - url : [https://gr--jnwgn.run.goorm.io](https://gr--jnwgn.run.goorm.io/)
    
    ![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%206.png)
    

- 주소창에 url 입력하고 정상작동하는지 테스트

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%207.png)

### 스킬 사용

- 카카오톡 오픈 빌더 스킬 설정
- URL 입력 + 엔드포인트
    - [https://gr--jnwgn.run.goorm.io](https://gr--jnwgn.run.goorm.io/)/random

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%208.png)

- 블록에서 사용할 스킬을 설정한다.

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%209.png)

### 결과

- 설정한 발화패턴 입력시 랜덤으로 숫자가 생성된다

![Untitled](/images/GoormIDE_with_kakaoSkill/Untitled%2010.png)

- Reference

[https://www.youtube.com/watch?v=EWK9G9XAk00&t=97s](https://www.youtube.com/watch?v=EWK9G9XAk00&t=97s)