---
title: "JAVA Setting with STS"
tags:
  - setting
categories:
  - Java
  - setting
author: "minkuen"
date: '2022-07-05'
---


### 사전준비

- VSCord 설치

### visual studio 추가 설치

- extension → 검색:markdown → 다음 확장 프로그램 3가지 설치

![Untitled](/images/JAVA_STS_setting/Untitled.png)

- 우측 위 돋보기 모양 클릭 → 마크다운 preview 참고하며 작성하자

![Untitled](/images/JAVA_STS_setting/Untitled%201.png)

### node.js

: 웹 브라우저가 아닌 환경에서 자바스크립트를 실행시킬 수 있는 런타임 환경

- 웹브라우저에서 동작하는 ‘프로그래밍 언어’는 only 자바스크립트뿐이다 O
    - 단, 다른 언어로 웹에서 동작하는 프로그래밍을 할 수 있다. —> 결국 자바스크립트로 변환
- 자바스크립트는 only 웹브라우저에서만 동작할 수 있다. O??
    - NODE JS가 이 문제의 답을 X로 만들었다.

### node.js 설치

- 구글링하여 설치
- 설치 확인 : 명령 프롬프트에서 `node -v`

![Untitled](/images/JAVA_STS_setting/Untitled%202.png)

### code runner 설치

- **node.js 설치된 상태**에서 설치해야 한다.
- visual studio → extension → 검색 : code ruuner
- 설치 후 visual studio 재부팅
- 우측 상단에 동영상 재생 마크와 유사하 것이 생성됨 = 코드 러닝 버튼

![Untitled](/images/JAVA_STS_setting/Untitled%203.png)

### run code사용

- 코드 작성 후 run code 버튼 클릭

![Untitled](/images/JAVA_STS_setting/Untitled%204.png)

- 결과

![Untitled](/images/JAVA_STS_setting/Untitled%205.png)

### STS 설치

구글링 : sts4

[https://spring.io/tools](https://spring.io/tools)

- 가장 아래에 window로 설치

![Untitled](/images/JAVA_STS_setting/Untitled%206.png)

### JDK - 1.11 다운로드

- 1.x버전이면 x버전이라 부른다
- 2번째로 많이 사용되는 버전
- 첫번째로 많이 사용되는 것은 2014년 1.8 버전
- 그나마 최근이면서 주로 사용되는 JDK  1.11 로 설치
- 구글링 : JDK 1.11 download
    - [https://www.oracle.com/kr/java/technologies/javase/jdk11-archive-downloads.html](https://www.oracle.com/kr/java/technologies/javase/jdk11-archive-downloads.html)

![Untitled](/images/JAVA_STS_setting/Untitled%207.png)

- 다음 경로를 참고해서 설치

![Untitled](/images/JAVA_STS_setting/Untitled%208.png)

### 버전 확인

- 다음 코드로 버전을 확인했을 때 11버전이 출력되어야 한다
- `java -version`
- `javac -version`
    - javac = java 컴파일러

![Untitled](/images/JAVA_STS_setting/Untitled%209.png)

### 다른 버전이 출력될 경우

검색창 : 변수 → 환경변수 → JAVA_HOME 을 편집으로 바꾼다

- 없다면 설정한다
- java 경로로 변경한다
    - C:\Program Files\Java\jdk-11.0.15
- 다시 버전 확인한다

### STS 설치

- 파일 이름 길이가 너무 길기 때문에 줄인다
    - 예시) spring-tool-suite-4.jar

![Untitled](/images/JAVA_STS_setting/Untitled%2010.png)

- spring-tool-suite-4.jar → contents.zip 앞축을 풀고 들어간다
- contents → sts-4.14.1.RELEASE 폴더를 안전한 경로에 복사 붙여넣기

- string-tool-suite4를 복사하여 백업본을 만들어둔다
- 우클릭 : string-tool-suite4 → 메모장으로 열기
- 메모장에서 메모리를 수정
- 램 용량을 표시
- 내 컴퓨터 → 속성
- 램 용량 확인 = 본인은 8G

![Untitled](/images/JAVA_STS_setting/Untitled%2011.png)

- 본인 RAM의 1/8, 1/4 이 되도록 표시
- 8G의 8/1 = 1G = 2^10 = 1024
- 8G의 4/1 = 2G = 2*2^10 = 2048

- 즉, -Xms1024m
     -Xmx2048m
- 이후 저장한다

![Untitled](/images/JAVA_STS_setting/Untitled%2012.png)

### Spring Tool Suite4 실행

- sts-4.14.1.RELEASE 폴더 → sprinttoolsuite4.exe 를 작업표시줄에 고정
- sprinttoolsuite4.exe 실행
    - workspace 설정을 요구할 것이다

![Untitled](/images/JAVA_STS_setting/Untitled%2013.png)

- sts-4.14.1.RELEASE 있는 경로에 폴더 생성 : workspace_seoulAI
- 해당 경로에 경로 설정

![Untitled](/images/JAVA_STS_setting/Untitled%2014.png)

### Spring Tool Suite에서 추가 설치

- Help → eclipse Marketplace → 검색 : Java and Web developer tool → 설치

![Untitled](/images/JAVA_STS_setting/Untitled%2015.png)

### UTF-8 설정

- window→preference → encoding 검색
- java class file,  text, text→java Properties File  이 3개에 대해서 utf-8 추가한다
- 추가 방법
    - 1. Content types: 에서 3개 중에서 설정할 것을 선택
    - 2.다음과 같이 하단에 utf-8 적고 Update
    1. 3개 모두 같은 방법으로 utf-8을 추가해준다

![Untitled](/images/JAVA_STS_setting/Untitled%2016.png)

- General - Workspace → 설정 : utf-8

![Untitled](/images/JAVA_STS_setting/Untitled%2017.png)

- 다음 그림의 좌측에 보이는 **모든 메뉴**에 들어가서  설정 변경
- 설정 변경 : utf-8

![Untitled](/images/JAVA_STS_setting/Untitled%2018.png)

### 추가 설정

- Window → preference → 검색 : installed → add

![Untitled](/images/JAVA_STS_setting/Untitled%2019.png)

- Standard VM 더블 클릭

![Untitled](/images/JAVA_STS_setting/Untitled%2020.png)

- directory 선택

![Untitled](/images/JAVA_STS_setting/Untitled%2021.png)

- jdk-11 선택

![Untitled](/images/JAVA_STS_setting/Untitled%2022.png)

- 11버전이므로 아래 2개중에서 아래 것을 체크
- 13버전 이상일 때만 다음 그림과 다르게 체크
- finish → 다음 페이지에서 위에 항목을 체크 → Apply and Close
- *이후에 코드 실행하여 Linkage… 에러가 생기면 이 설정을 변경해보자

![Untitled](/images/JAVA_STS_setting/Untitled%2023.png)

### 프로젝트 생성

- 기본 화면에서 좌측 workspace의 Create Java project를 클릭
- Create Java project → 다음 그림 참고하여 체크 → 생성한다

![Untitled](/images/JAVA_STS_setting/Untitled%2024.png)

- 다음과 같이 생성되었다

![Untitled](/images/JAVA_STS_setting/Untitled%2025.png)

### JDK

- JDK는 자바 개발도구(Java Development Kit)의 약자이다
- JDK는 JRE + 개발을 위해 필요한 도구(javac, java등)들을 포함한다

![Untitled](/images/JAVA_STS_setting/Untitled%2026.png)

### Hello World

- 우클릭 : src → New → class

![Untitled](/images/JAVA_STS_setting/Untitled%2027.png)

- Main 이라고 명명

![Untitled](/images/JAVA_STS_setting/Untitled%2028.png)

- 코드 작성
    - 팁 :  ctrl + space바

```html
package variable;

public class Main {
	public static void main(String[] args) {
		System.out.println("헬로 월드");
	}
	
}
```

- 저장한 후에 실행한 결과

![Untitled](/images/JAVA_STS_setting/Untitled%2029.png)