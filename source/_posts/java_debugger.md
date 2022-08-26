---
title: "JAVA Debugger"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-07-10'
---


### 디버거 (debugger)

- de + bug = 버그를 없애다
- 개발에 매우 중요한 모드

### Java에서 사용하는 법

- 원하는 라인에 더블클릭 = 파란색 브레이크 포이트 걸기
- 우클릭 : debug as로 실행

![Untitled](/images/java_debugger/Untitled.png)

- 디버그 모드 탈출
- 우측 상단에 벌레 아이콘 옆에 있는 Java 아이콘 클릭
- 해당 아이콘을 클릭하면 개발자 모드로 돌아올 수 있다.

![Untitled](/images/java_debugger/Untitled%201.png)

### Java Script에서 사용하는 법

- 지정할 브레이크 포인트에 `debugger;` 작성
- 개발자모드를 열어놓은 상태에서 해당 영역에 도달한다

- 브라우저 → 우클릭: 감사
- Console 창에서 실행)  함수를 복사해서 붙여넣는다
- 함수를 호출한다

![Untitled](/images/java_debugger/Untitled%202.png)

- 디버거 모드 진입
- F9
    - 해당 키를 통해서 순차적으로 코드를 살펴보면 된다

![Untitled](/images/java_debugger/Untitled%203.png)

### 디버거의 용도

- 혼자하는 작업만 고려한다면 필수는 아니다
- 하지만, 수십명이 함께 작업한 코드를 분석할 경우에는 상황이 매우 복잡해지므로
- 다수가 함게하는 작업에서 특히 유용한 것이 디버거이다
- 디버거의 활용으로 (초급 개발자) / (중급 개발자)로 나뉜다는 듯