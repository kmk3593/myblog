---
title: "Kakao Chatbot 스킬 사용"
tags:
  - chatbot
  - kakao_chatbot
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-05-28'
---


## 사전준비

- Heroku 배포 이후에 진행
- Hello world가 출력된 페이지를 띄어야 한다.

## **스킬 서버 구축 기본편**

- 스킬 서버에서 제공하는 2가지 API URI는 다음과 닽다.
- 단순 텍스트형 응답 스킬
    - POST /api/sayHello
- 단순 이미지형 응답 스킬
    - POST /api/showHello

### **(1) 스킬 서버 예제**

- 코드 작성 : [main.py](http://main.py)
    - 코드 `print(body['userRequest']['utterance'])`와 `responseBody` 영역은 추후 설명 할 예정이다.

```python
from flask import Flask, request
import json

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!!!!!!!!!!!!!!!!!!!!!!!'

# 카카오톡 텍스트형 응답
@app.route('/api/sayHello', methods=['POST'])
def sayHello():
    body = request.get_json() # 사용자가 입력한 데이터
    print(body)
    print(body['userRequest']['utterance'])

    responseBody = {
        "version": "2.0",
        "template": {
            "outputs": [
                {
                    "simpleText": {
                        "text": "반가워!!!!! hello I'm Ryan"
                    }
                }
            ]
        }
    }

    return responseBody

# 카카오톡 이미지형 응답
@app.route('/api/showHello', methods=['POST'])
def showHello():
    body = request.get_json()
    print(body)
    print(body['userRequest']['utterance'])

    responseBody = {
        "version": "2.0",
        "template": {
            "outputs": [
                {
                    "simpleImage": {
                        "imageUrl": "https://t1.daumcdn.net/friends/prod/category/M001_friends_ryan2.jpg",
                        "altText": "hello I'm Ryan"
                    }
                }
            ]
        }
    }

    return responseBody
```

- 코드 저장 후 배포 시 주의점
    - 경로에 주의해야 한다!
- 배포 진행한다.

```python
$ git add .
$ git commit -am "your_message" # 이 부분만 자유롭게 쓸 수 있다.
$ git push origin main ## Github Repository에 업데이트
$ git push heroku main ## Heroku 코드 배포
```

### **(2) 스킬 서버 등록**

**단순 텍스트형 응답**

- 아래와 같이 스킬 서버 정보를 입력하고 저장한다.
- 코드에서 정의한 이름을 URL 뒤에 덧붙인다  : /api/sayHello

![Untitled](/images/kakao_skill/Untitled.png)

**단순 이미지형 응답**

- 텍스트형 응답과 같은 과정을 거친다.
- /api/showHello

### **(3) 시나리오**

- 여기가 가장 중요하다. 이제 시나리오를 등록한다. 이 때 중요한 것은 파라미터 설정 탭에서 스킬 선택을 개별적으로 호출 할 수 있다.

‘**단순 텍스트형 응답’ 스킬 사용**

- 봇 응답에서 스킬 데이터를 선택 후, 저장 버튼을 클릭한다.

![Untitled](/images/kakao_skill/Untitled%201.png)

‘**단순 이미지형 응답’ 스킬 사용**

- 사용할 스킬 데이터를 선택 후, 저장한다.

### **(4) 배포**

- 배포 탭을 클릭한 후, 배포를 진행

![Untitled](/images/kakao_skill/Untitled%202.png)

### **(5) 테스트**

- 봇 테스트를 열고 아래와 같이 테스트를 한다.

- 배포 완료 후 사용 가능

- 단순 텍스트형 응답
    - 설정한 텍스트 출력
    - 정상 작동

- 단순 이미지형 응답
    - 설정한 이미지 출력
    - 정상 작동

![Untitled](/images/kakao_skill/Untitled%203.png)

### **(6) 로그 확인**

- Heroku 에서는 로그를 쉽게 확인 가능

```python
heroku logs
```

### (7) 출력

- outputs는 출력 그룹을 나타내며, 출력 그룹은 1~3개까지 출력 요소를 포함시킬 수 있다.
- 출력요소는 크게 7가지이다. (2022년 5월 기준)
    - simpleText : 간단 텍스트 (**[https://i.kakao.com/docs/skill-response-format##simpletext](https://i.kakao.com/docs/skill-response-format##simpletext)**)
    - simpleImage : 간단 이미지 (**[https://i.kakao.com/docs/skill-response-format##simpleimage](https://i.kakao.com/docs/skill-response-format##simpleimage)**)
    - basicCard : 기본 카드 (**[https://i.kakao.com/docs/skill-response-format##basiccard](https://i.kakao.com/docs/skill-response-format##basiccard)**)
    - commerceCard : 커머스 카드 (**[https://i.kakao.com/docs/skill-response-format##commercecard](https://i.kakao.com/docs/skill-response-format##commercecard)**)
    - listCard : 리스트 카드 (**[https://i.kakao.com/docs/skill-response-format##listcard](https://i.kakao.com/docs/skill-response-format##listcard)**)
    - ItemCard : 아이템 말풍성 카드 (**[https://i.kakao.com/docs/skill-response-format##itemcard](https://i.kakao.com/docs/skill-response-format##itemcard)**)
    - Carousel : 케로셀 카드 (**[https://i.kakao.com/docs/skill-response-format##carousel](https://i.kakao.com/docs/skill-response-format##carousel)**)
- 그 외에도 다양한 기능들은 도움말 및 예제코드를 확인하도록 한다.

## ****챗봇 빌더를 활용한 사칙연산 계산기 구현****

- 사칙 연산을 구현하는 챗봇을 만들어 본다.

### **(1) 엔티티 구성**

- 엔티티(Entity) : 봇이 이해할 수 있는 용어를 체계적으로 정리한 데이터 사전
- 엔티티 구조는 = 엔티티명, 대표 엔트리, 동의어
- 엔티티의 자세한 설명은 다음 링크에서 확인
    - URL : **[https://i.kakao.com/docs/key-concepts-entity](https://i.kakao.com/docs/key-concepts-entity)**
- 사칙연산을 예로 들면 아래와 같이 지정할 수 있다.
    - division, subtraction 등은 대표 엔트리를 말한다.
    - 동의어에 해당하는 값이 나오면 추후에 확인할 로그 값에는 대표 엔트리만 별도로 데이터를 수집할 수 있다.

![Untitled](/images/kakao_skill/Untitled%204.png)

### **(2) 시나리오 구성**

- 엔티티를 구성했다면, 이제 시나리오를 구성한다.
- 사용할 파라미터를 설정한다.

![Untitled](/images/kakao_skill/Untitled%205.png)

- 패턴 발화를 할 때 원하는 파라미터를 별도로 지정할 수 있다.
- 패턴 발화를 보면 빨간색 네모 박스를 확인할 수 있는 데, 이 부분에서 파라미터를 설정할 수 있다.
- 더하기, +에서의 파라미터는 엔티티 그룹을 설정하게 된다.

![Untitled](/images/kakao_skill/Untitled%206.png)

- 실제 파라미터 설정된 값은 다음과 같다.

![Untitled](/images/kakao_skill/Untitled%207.png)

### **(3) 파이썬 코드**

- 이제 다음 코드를 작성하여 기존 main.py에 추가한다.
- 코드 작성시, 한가지 유의 사항은 json.loads() 함수를 반드시 써줘야 한다. Python Dictionary를 String으로 변경하는 것은 str() 함수를 사용하면 쉽게 변경이 가능하지만, 문자열 dictionary를 Dictionary로 바로 변경은 되지 않는다. 따라서, json.loads()를 사용한다.
    - 참조 : **[https://blog.metafor.kr/224](https://blog.metafor.kr/224)**

```python
from flask import Flask, request
import json

# 메인 로직!! 
def cals(opt_operator, number01, number02):
    if opt_operator == "addition":
        return number01 + number02
    elif opt_operator == "subtraction": 
        return number01 - number02
    elif opt_operator == "multiplication":
        return number01 * number02
    elif opt_operator == "division":
        return number01 / number02

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!!!!!!!!!!!!!!!!!!!!!!!'

# 카카오톡 텍스트형 응답
@app.route('/api/sayHello', methods=['POST'])
def sayHello():
    body = request.get_json() # 사용자가 입력한 데이터
    print(body)
    print(body['userRequest']['utterance'])

    responseBody = {
        "version": "2.0",
        "template": {
            "outputs": [
                {
                    "simpleText": {
                        "text": "반가워!!!!! hello I'm Ryan"
                    }
                }
            ]
        }
    }

    return responseBody

# 카카오톡 이미지형 응답
@app.route('/api/showHello', methods=['POST'])
def showHello():
    body = request.get_json()
    print(body)
    print(body['userRequest']['utterance'])

    responseBody = {
        "version": "2.0",
        "template": {
            "outputs": [
                {
                    "simpleImage": {
                        "imageUrl": "https://t1.daumcdn.net/friends/prod/category/M001_friends_ryan2.jpg",
                        "altText": "hello I'm Ryan"
                    }
                }
            ]
        }
    }

    return responseBody

# 카카오톡 Calculator 계산기 응답
@app.route('/api/calCulator', methods=['POST'])
def calCulator():
    body = request.get_json()
    print(body)
    params_df = body['action']['params']
    print(type(params_df))
    opt_operator = params_df['operators']
    number01 = json.loads(params_df['sys_number01'])['amount']
    number02 = json.loads(params_df['sys_number02'])['amount']

    print(opt_operator, type(opt_operator), number01, type(number01))

    answer_text = str(cals(opt_operator, number01, number02))

    responseBody = {
        "version": "2.0",
        "template": {
            "outputs": [
                {
                    "simpleText": {
                        "text": answer_text
                    }
                }
            ]
        }
    }

    return responseBody
```

- 코드를 저장 후 git배포한다.
- 스킬 설정

![Untitled](/images/kakao_skill/Untitled%208.png)

- 스킬을 사용할 블록에서 스킬을 지정하고 챗봇 배포한다.

![Untitled](/images/kakao_skill/Untitled%209.png)

- 배포 후 카카오톡에서 직접 실험

- (+) 연산 정상작동

- (-)연산 정상작동
 
- (x) 연산 정상작동

- (%) 연산 정상작동

- 사칙연산 모두 정상작동하므로 성공

![Untitled](/images/kakao_skill/Untitled%2010.png)

- Reference
    - [https://dschloe.github.io/python/kakao_chatbot/chatbot_calculator/](https://dschloe.github.io/python/kakao_chatbot/chatbot_calculator/)