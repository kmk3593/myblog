---
title: "Kakao Chatbot open builder"
tags:
  - chatbot
  - kakao_chatbot
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-05-24'
---


# 챗봇 제작

## 챗봇 설정

- 프로필 설정 : 모든 사항에 관해 공개로 전환

![Untitled](/images/kakao_chatbot_1/Untitled.png)

- 운영 채널 연결 : ‘tutorial’ 챗봇 ↔ ‘휴먼주식도우미챗봇’ 채널
    - 배포만 하면 카카오톡에서 검색 가능하다.

![Untitled](/images/kakao_chatbot_1/Untitled%201.png)

- 배포
    - 첫 배포 : 이제 카카오톡에서 검색이 가능하며 사용이 가능해진다.
    - 그 이후의 배포 : 작성한 블록 시나리오 등이 실제 카카오톡에 반영된다.

![Untitled](/images/kakao_chatbot_1/Untitled%202.png)

- 관리자 초대
    - 조원들과 챗봇을 공동으로 관리하기 위해 설정

![Untitled](/images/kakao_chatbot_1/Untitled%203.png)

## 시나리오 작성

- 앞서 제작된 **시나리오 구상안을 토대**로 챗봇의 **시나리오, 블록 작성**

- 시나리오 생성
- 주요 기능을 기반으로 시나리오 생성

![Untitled](/images/kakao_chatbot_1/Untitled%204.png)

- 0 메뉴
    - 주요 기능을 모두 사용할 수 있는 메뉴를 호출할 시나리오를 의도하고 생성

- 1 주식이 처음이신가요?
    - 주식 초심자를 위해 ‘계정 생성 방법’과 ‘주식 거래하는 방법’ 등을 설명하기 위한 시나리오

- 2 주식 단어
    - 입문자를 위한 간단한 주식 용어를 설명하고 더 많은 용어를 공부하기 원하는 사용자를 위한 추가적으로 자료를 담을 예정
    
- 3 종목별 시세를 알려드릴까요
    - 종목 시세를 확인 가능하도록 크롤링한 데이터를 출력할 시나리오를 계획

- 4 현재 인기 많은 종목 알려드릴까요?
    - 처음 주식하는 사람들에게 주식을 추천하기 위한 기능을 넣을 시나리오

- 5 꼭 알아야 할 이슈
    - 초심자가 현재의 주식 관련 흐름을 파악하는데 도움을 줄 정보를 알려줘야 할 시나리오 생성

## 블록 작성

- 시나리오 아래에 **구상안을 구현할 블록들을 작성**
- 블록명을 **넘버링하여 상위 하위를 구분 가능**하게 함.
- **상위에서 하위로** 넘어갈 수 있게 제작
    - 예를 들어, 1-1 블록에서 1-1-1 블록이나 1-1-2 블록으로 이동 가능
- 거의 모든 블록에 **돌아가기 기능 탑재.** 반대로 **하위에서 상위로** 이동하도록 구현

- **0 메뉴얼 블록**
    - 0 메뉴얼 : 주요 기능 사용과 개선사항 전달이 가능한 메뉴를 출력하는 블록

![Untitled](/images/kakao_chatbot_1/Untitled%205.png)

- **1 주식이 처음이신가요** **블록**
    - 다음 두 가지 기능 중 하나를 선택하고 호출하는 블록
    - 1-1 계정 만드는 법 알아보기
        - 1-1-1 오프라인으로 계좌 개설하기
        - 1-1-2 온라인으로 계좌 개설하기
    - 1-2 기초 상식 알아보기
        - 1-2-1 주식은 이렇게 거래합니다
        - 1-2-2 주식 시장의 결제 방식
        - 1-2-3 증권사 수수료, 증권거래세

![Untitled](/images/kakao_chatbot_1/Untitled%206.png)

- **2 주식 단어 목록 블록**
    - 간단한 단어와 그 뜻이 담긴 여러 블록과 연결
    - 더 많은 용어를 알고 싶은 초심자를 위한 자료의 링크가 연결된 버튼을 제작

![Untitled](/images/kakao_chatbot_1/Untitled%207.png)

- **3 종목별 시세 확인 블록**
    - 종목 시세를 확인 가능하도록 크롤링한 데이터를 출력할 예정
    - 임시로 시가총액 확인 가능한 링크를 연결

![Untitled](/images/kakao_chatbot_1/Untitled%208.png)

- **4 최근 인기 종목 알려드립니다 블록**
    - 거래상위, 상승주, 하락주를 확인 가능한 링크를 연결
    - 매수상위, 매도상위를 기반으로 인기 많은 종목을 출력할 예정
    - 임시로 매수상위, 매도상위 확인 가능한 링크를 연결

![Untitled](/images/kakao_chatbot_1/Untitled%209.png)

- **5 꼭 알아야할 이슈,뉴스 블록**
    - 주식 관련 뉴스를 확인할 수 있게 설정
    - 매일 뉴스를 찾아서 확인하기 번거로운 사용자들을 위한 관련 기능 추천

![Untitled](/images/kakao_chatbot_1/Untitled%2010.png)

## 제네릭 메뉴 설정

- +시나리오 밑에 ‘시나리오 설정’ 에서 설정
- 주요 기능과 같은 이름으로 제네릭 메뉴 생성
- 각 제네릭 메뉴를 주요 기능을 사용할 수 있는 블록과 연결한다.

![Untitled](/images/kakao_chatbot_1/Untitled%2011.png)

## 배포 : 챗봇 시나리오 반영 여부 확인

- 배포 후 카카오톡에서 의도대로 기능이 작동하는 시험

![Untitled](/images/kakao_chatbot_1/Untitled%2012.png)

![Untitled](/images/kakao_chatbot_1/Untitled%2013.png)

 

![Untitled](/images/kakao_chatbot_1/Untitled%2014.png)

![Untitled](/images/kakao_chatbot_1/Untitled%2015.png)

## 피드백 받습니다.

- 카카오톡 검색 : 휴먼주식도우미챗봇

![Untitled](/images/kakao_chatbot_1/Untitled%2016.png)

- 개선사항 전달 or 상담직원 연결

![Untitled](/images/kakao_chatbot_1/Untitled%2017.png)

![Untitled](/images/kakao_chatbot_1/Untitled%2018.png)

- 개선사항을 적어주세요

![Untitled](/images/kakao_chatbot_1/Untitled%2019.png)

- 채널에서 확인하고 개선

![Untitled](/images/kakao_chatbot_1/Untitled%2020.png)