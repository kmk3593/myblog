---
title: "html 기초"
tags:
  - setting
  - HTML
categories:
  - frontEnd 
  - html & css
author: "minkuen"
date: '2022-06-05'
---



### 사전작업

- 바탕 화면에 폴더 생성 : project
- 폴더 우클릭 : git bash here
- VSCord 작동 : `code .`

![Untitled](/images/html_start/Untitled.png)

- 폴더, 파일 생성
- PROJECT 아래에 생성
    - 폴더 생성 : step01_intro
    - 파일 생성 : index.html

### html 작성

- 코드 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
    </head>
    <body>
        aaa
    </body>
</html>
```

- 저장 후 폴더에서  html파일 열기
- 다음과 같이 작서한 내용이 출력되어 있다.

![Untitled](/images/html_start/Untitled%201.png)

### 링크 첨부

- Naver 주소를 복사하여 다음과 같이 작성한다.

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
    </head>
    <body>
        <a href="https://www.naver.com/">NAVER</a>
        <br>
        <br>
        <div>Hello World</div>
    </body>
</html>
```

![Untitled](/images/html_start/Untitled%202.png)

### 이미지 추가

- project/step01_intro 경로에 폴더 생성 : img
- 아무 사진이나 다운받아서 폴더에 넣는다.
    - 사진을 다른 이름으로 저장 : temp
- 여기까지 설정하고 다음과 같이 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
    </head>
    <body>
        <a href="https://www.naver.com/">NAVER</a>
        <br>
        <br>
        <div>Hello World</div>
        <br>
        <img src="./img/temp.jpg" alt = "ball">
    </body>
</html>
```

![Untitled](/images/html_start/Untitled%203.png)

### 이미지 주소로 추가

- 이미지 우클릭 : 이미지 링크 복사
- 다음과 같이 링크를 붙여넣고 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
    </head>
    <body>
        <a href="https://www.naver.com/">NAVER</a>
        <br>
        <br>
        <div>Hello World</div>
        <br>
        <img src="./img/temp.jpg" alt = "ball">
        <img src="https://img.animalplanet.co.kr/news/2020/01/07/700/tbg4j63622z4545z51af.jpg" alt = "fox">
    </body>
</html>
```

![Untitled](/images/html_start/Untitled%204.png)

### 페이지 이동

- 링크로 페이지 이동하기
- 우선 step01_intro 아래에 폴더 생성 : about
    - about 아래에 파일 생성 : index.html
- about/index.html에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>About</title>
    </head>
    <body>
       <a href="../">Home</a>
       About 페이지입니다.
    </body>
</html>
```

- index.html에 about/index.html 경로 추가

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
    </head>
    <body>
        <! -- 키워드: 상대경로, 절대경로 -->
        <a href="https://www.naver.com/">NAVER</a>
        <a href="./about/index.html">About</a>
        
        <br>
        <br>
        <div>Hello World</div>
        <br>
        <img src="./img/temp.jpg" alt = "ball">
        <img src="https://img.animalplanet.co.kr/news/2020/01/07/700/tbg4j63622z4545z51af.jpg" alt = "fox">
    </body>
</html>
```

![Untitled](/images/html_start/Untitled%205.png)

### 팁

- 다음 설정으로 코드 가독성을 높일 수 있다.
    - VSCord → 메뉴바 → 보기 → 자동 줄 바꿈