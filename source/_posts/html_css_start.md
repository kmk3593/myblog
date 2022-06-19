---
title: "html & css"
tags:
  - setting
  - HTML
categories:
  - frontEnd 
  - html & css
author: "minkuen"
date: '2022-06-06'
---


### 사전작업

- 살행할 폴더 우클릭 : git bash here
- VSCord 작동 : `code .`

- 폴더, 파일 생성
- PROJECT 아래에 생성
    - 폴더 생성 : step02_hello
    - 파일 생성 : index.html
    - 파일 생성 : main.css

### CSS 작성

- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
        <link rel="stylesheet" href="./main.css" >
    </head>
    <body>
        <div>Hello World</div>
    </body>
</html>
```

- main.css 에 다음 내용 작성

```css
div {
    width: 400px;
    height: 200px;
    background-color: blue;
}
```

- step02_hello 폴더에서 index.html을 오픈
- 다음과 같이 페이지가 출력된다.

![Untitled](/images/html_css_start/Untitled.png)

### 이미지 업로드

- step02_hello 아래에 폴더 생성 : img
- 사진을 img폴더 경로에 다운로드 : rainday
- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
        <link rel="stylesheet" href="./main.css" >
    </head>
    <body>
        <div class = "weather_title">
            <h1>오늘의 날씨</h1>
            <p>오늘은 비가 많이 내릴 예정입니다. ~~</p>
            <img src="./img/rainday.webp" alt="rain">
        </div>
    </body>
</html>
```

- main.css 에 다음 내용 작성

```css
div {
    width: 200px;
    height: 200px;
    background-color: blue;
}

p{
    color: navy;
    text-indent : 30px;
    text-transform: uppercase;
}
```

- 지정한 이미지가 업로드되었다.

![Untitled](/images/html_css_start/Untitled%201.png)

### div 클래스

- div를 이용하여 글을 작성한다.
- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
        <link rel="stylesheet" href="./main.css" >
    </head>
    <body>
        <div class = "weather_title">
            <h1>오늘의 날씨</h1>
            <p>오늘은 비가 많이 내릴 예정입니다. ~~</p>
        </div>
        <div class = "fruits">
            <ul>
                <li>사과</li>
                <li>바나나</li>
                <li>수박</li>
                <li>오렌지</li>
            </ul>
        </div>
        <div id="song">
            <span>노래~~가사~~</span>
        </div>
    </body>
</html>
```

- main.css 에 다음 내용 작성

```css
div {
    width: 200px;
    height: 200px;
    background-color: blue;
}

div.fruits {
    width: 500px;
    height: 300px;
    background-color: orange;
}

#song {
    width: 500px;
    height: 300px;
    background-color: rgb(205, 235, 135);
}

p{
    color: navy;
    text-indent : 30px;
    text-transform: uppercase;

}
```

- 다음과 같이 차례로 출력된다.

![Untitled](/images/html_css_start/Untitled%202.png)

### Label, Table

- 라벨과 테이블을 사용해본다.
- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=devie-width, initial-scale=1.0">
        <title>돈까스집</title>
        <link rel="stylesheet" href="./main.css" >
    </head>
    <body>
        <div class = "weather_title">
            <h1>오늘의 날씨</h1>
            <p>오늘은 비가 많이 내릴 예정입니다. ~~</p>
        </div>
        <div class = "fruits">
            <ul>
                <li>사과</li>
                <li>바나나</li>
                <li>수박</li>
                <li>오렌지</li>
            </ul>
        </div>
        <div id="song">
            <span>노래~~가사~~</span>
        </div>

        <br>
        <input type = "text" value = "hello" />
        <input type = "text" placeholder = "이름을 입력하세요"/>

        <label>
            <input type="checkbox" />사과
            <input type="checkbox" checked/>바나나
        </label>

        <table>
            <tr>
                <th>항목명1</th>
                <td>내용이 들어갑니다.</td>
            </tr>
            <tr>
                <th>항목명2</th>
                <td>내용이 들어갑니다.</td>
            </tr>
            <tr>
                <th>항목명3</th>
                <td>내용이 들어갑니다.</td>
            </tr>
        </table>

    </body>
</html>
```

- main.css 에 다음 내용 작성

```css
div {
    width: 200px;
    height: 200px;
    background-color: blue;
}

div.fruits {
    width: 500px;
    height: 300px;
    background-color: orange;
}

#song {
    width: 500px;
    height: 300px;
    background-color: rgb(205, 235, 135);
}

p{
    color: navy;
    text-indent : 30px;
    text-transform: uppercase;

}

input:focus {
    background-color: blue;
}
```

![Untitled](/images/html_css_start/Untitled%203.png)

### 팁

Ctrl + A 후 전체정렬

전체 정렬 : Ctrl + Alt + L

### 추가 공부

[https://www.inflearn.com/course/html5](https://www.inflearn.com/course/html5)

- 해당 링크에서 필요한 강의를 찾아서 듣기
- 최종적으로 홈페이지가 제작되는 강의나 책을 선택해야 한다.

### 참고 자료

- **[[CSS] Flex를 사용하여 DIV 예쁘게 배치하기 (Container 편)](https://wooncloud.tistory.com/10)**
- 한 번에 끝내는 프론트엔트 개발_강의자료.pdf
- HTTP웹_기본지식_20201226.pdf