---
title: "JAVA exception"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-09-17'
---

# Java 실행파일 생성, 사용

### 자바 실행파일 생성 & 사용

- 프로젝트 우클릭 → export → 검색:runnable

![Untitled](/images/Java_runnable_file/Untitled.png)

- 다음 그림에서 Runnable Jar file 클릭

![Untitled](/images/Java_runnable_file/Untitled%201.png)

- 해당 경로로 가서 Shift + 우클릭 → 현재 위치에서 powerShell 열기

ls명령어로 파일 확인

- 다음과 같이 Main 을 지정해준다.
- Browse → 원하는 경로 설정 → 파일 저장

![Untitled](/images/Java_runnable_file/Untitled%202.png)

- Browse → 원하는 경로 설정 → 파일 저장
- 이름 지정하고 파일 저장

![Untitled](/images/Java_runnable_file/Untitled%203.png)

- 파일 탐색기에서 해당 경로로 이동
- 공백에서 Shift + 우클릭 → 여기에 PowerShell 창 열기

![Untitled](/images/Java_runnable_file/Untitled%204.png)

- `java -jar` + `‘찾을 파일 앞글자’` + Tab
- Enter → 자바 파일 실행
- 정삭적으로 실행되었다.

![Untitled](/images/Java_runnable_file/Untitled%205.png)