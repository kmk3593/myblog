---
title: "Java Script 실습2"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-09'
---

 
### 사전작업

- 살행할 폴더 우클릭 : git bash here
- VSCord 작동 : `code .`

- 폴더, 파일 생성
- PROJECT 아래에 생성
    - 폴더 생성 : step05_js
    - 파일 생성 : ch01_index.html

### JavaScript 작성

- ch01_index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <center>
        <p>안녕하세요!</p>
        <button type="button" onclick="document.getElementById"
        ('demo').innerHTML = Date()">
            버튼을 클릭하세요!
        </button>
        <p id="demo"></p>
    </center>
</body>
</html>
```

- step05_js 폴더에서 ch01_index.html을 오픈
- 페이지가 출력된다.

![Untitled](/images/javaScript_practice_2/Untitled.png)

### 스크립트 불러오기 사전준비

- 파일 생성
- step05_js 폴더 아래에 생성
    - 파일 생성 : ch02_1_js.html
    
- ch02_1_js.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <center>
        <p>안녕하세요!</p>
        <p id="demo">adfadfa</p>

        <! -- 스크립트 불러오기 -- >
        <script>
            document.getElementById('demo').innerHTML="자바스크립트";
        </script>
    </center>
</body>
</html>
```

- step05_js 폴더에서 ch02_1_js.html을 오픈
- 페이지가 출력된다.

![Untitled](/images/javaScript_practice_2/Untitled%201.png)

### 스크립트 불러오기 사전준비

- 파일 생성
- step05_js 폴더 아래에 생성
    - 파일 생성 : ch02_2_js.html
    
- 폴더, 파일 생성
- step05_js 폴더 아래에 생성
    - 폴더 생성 : js
    - js 아래에 파일 생성 : myscript.js

- ch02_2_js.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <center>
        <p>안녕하세요!</p>
        <p id="demo">adfadfa</p>

        <! -- 스크립트 불러오기 -- >
        <script src = "js/myscript.js"></script>
    </center>
</body>
</html>
```

- myscript.js 에 다음 내용 작성

```jsx
document.getElementById('demo').innerHTML="자바스크립트";
```

- step05_js 폴더에서 ch02_2_js.html을 오픈
- 페이지가 출력된다.
- html에 작성하지 않은 스크립트의 출력에 성공했다.

![Untitled](/images/javaScript_practice_2/Untitled%202.png)

### 버튼

- ch02_2_js.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        document.getElementById('demo').innerHTML="자바스크립트";
    </script>
</head>
<body>
    <center>
        <p>안녕하세요!</p>
        <p id="demo">adfadfa</p>
        <button type="button" onclick="myFunction()">
            버튼을 클릭하세요!
        </button>
    </center>
</body>
</html>
```

- step05_js 폴더에서 ch02_2_js.html을 오픈
- 페이지가 출력된다.

![Untitled](/images/javaScript_practice_2/Untitled%203.png)