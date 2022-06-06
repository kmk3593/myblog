---
title: "Kakao 스킬서버"
tags:
  - chatbot
  - kakao_chatbot
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-05-26'
---

### 챗봇에 다음과 같은 연산을 도입하게 위한 기능이다

5*10은 무엇인가요?

- 사칙연산
- number01 operator number02
- def cal(number1, number2)
    
           number 1 * number 2
    

### 스킬의 역할

1. 바로 동작에서 출력으로 이동함으로써 달성 불가능한 것을 **스킬을 거쳐서 가능케 함**
2. [발화입력 → 동작 → 스킬 → 출력] 

![Untitled](/images/skill_server_theory/Untitled.png)

- **웰컴 블록(Welcome Block)**

웰컴 블록은 사용자가 봇을 처음 사용할 때 받게되는 웰컴메시지를 설정하는 블록.

웰컴블록'이 '사용중'일 경우 사용자가 봇을 처음 사용할 때 웰컴블록에 설정된 응답이 전송되고, '미사용'일 경우 응답을 설정하는 부분이 비활성화 되고 OFF로 표기.

- **폴백 블록(Fallback Block)**

폴백 블록은 사용자의 발화 의도가 어떠한 블록과도 매칭이 되지 않을 때 (=봇이 사용자의 발화 의도를 이해하지 못할 때)의 응답을 설정하는 블록.

- **탈출 블록(Exit Block)**

탈출 블록은 봇의 되묻기 상황에서 사용자가 대화를 초기화하거나 탈출하고 싶을때 쓰는 사용자 명령어를 정의하는 블록.

### 스킬 처리 과정

- 봇 시스템 = 주문 블록
- 사용자 발화 : ‘피자 주문 할께요’
- 주문 블록 — **[스킬 호출]** —> 스킬 서버
- 주문 블록 <— **[스킬 응답]** — 스킬 서버
- 챗봇 답변 :  ‘피자 주문 완료’

![Untitled](/images/skill_server_theory/Untitled%201.png)

### 서버와 DB 구조

- 서버가 2개 필요
- 폭백 블록 → ←챗봇 API 서버 ↔ 챗봇 엔진 서버 ↔ 학습 DB

![Untitled](/images/skill_server_theory/Untitled%202.png)

### 스킬 사용

- 카카오 챗봇 → 스킬 → 생성
- 단, **서버 주소가 필요**하다.

![Untitled](/images/skill_server_theory/Untitled%203.png)

- 주소 끝에 다음과 같은 형식으로 입력
    - 단순 테스트 응답 스킬 주소 끝에 입력 : .com/api/sayHello
    - 단순 계산기 텍스트 응답 스킬 주소 끝에 입력 : .com/api/calCulator

- body = request.get_json() # 사용자가 입력한 데이터
- responseBody 는 일종의 템플릿. 이 틀에서 응답 형식으로 작성한다.
- simpletext

# 스킬 사용 코드 예시 : **SimpleImage**

간단한 이미지형 출력 요소입니다. 이미지 링크 주소를 포함하면 이를 스크랩하여 사용자에게 전달합니다. 이미지 링크 주소가 유효하지 않을 수 있기 때문에, 대체 텍스트를 꼭 포함해야 합니다.

### **상세 필드**

- 카카오챗봇 메뉴얼 참고 : [https://chatbot.kakao.com/docs/skill-response-format#basiccard](https://chatbot.kakao.com/docs/skill-response-format#basiccard)

```python
{
    "version": "2.0",
    "template": {
        "outputs": [
            {
                "simpleImage": {
                    "imageUrl": "http://k.kakaocdn.net/dn/83BvP/bl20duRC1Q1/lj3JUcmrzC53YIjNDkqbWK/i_6piz1p.jpg",
                    "altText": "보물상자입니다"
                }
            }
        ]
    }
}
```

### 엔티티 설정

- 엔티티 → 나의 엔티티 관리 → (엔티티 생성)

![Untitled](/images/skill_server_theory/Untitled%204.png)

- 이 엔티티와 동일한 이름으로 변수를 생성하고 코드 작성
- def clas(opt_operator, number01, number02) :  # 메인로직!!!

- sys.number 사용 가능한지 체크

![Untitled](/images/skill_server_theory/Untitled%205.png)

- 파라미터 설정

![Untitled](/images/skill_server_theory/Untitled%206.png)

- 사용자 발화 : 다음과 같이 발화에서 엔티티를 설정

![Untitled](/images/skill_server_theory/Untitled%207.png)

- 로그값 확인이 가능한 것을 사용 : aws, heroku, 구름IDE 중에서 선택

### heroku project 생성 시 주의

- 이름 다르게 생성! =  유일값
- heroku-kakap-chatbot은 사용 불가
- 언더바 _ 사용불가
- 다음 3가지를 같은 이름으로 생성
    - 로컬 폴더명 == Github Repo == Heroku Project 이름