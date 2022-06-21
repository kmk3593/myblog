---
title: "Java Script 실습1"
tags:
  - setting
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-08'
---

### 사전작업

- 살행할 폴더 우클릭 : git bash here
- VSCord 작동 : `code .`

- 폴더, 파일 생성
- PROJECT 아래에 생성
    - 폴더 생성 : step04_js_dom
    - 파일 생성 : index.html
    - 파일 생성 : main.js

### JavaScript 형식

- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width">
    <title>Document</title>
    <script src="./main.js"></script>
</head>

<body>
    <h1>자바스크립트 연습</h1>
</body>

</html>
```

- main.js 에 다음 내용 작성

```jsx
console.log("new file!")
```

- step04_js_dom 폴더에서 index.html을 오픈
- 페이지가 출력된다.
- html 페이지에서 우클릭 → 검사
- 다음과 같이 시스템 로그가 출력되었다.

![Untitled](Ja/images/javaScript_practice_1/Untitled.png)

### Event

- 이벤트를 감지하고 출력하는 코드를 작성해본다.
- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script defer src="./main.js"></script>

</head>
<body>
    <div class = 'box'>1</div>
    <div class = 'box'>2</div>
    <div class = 'box'>3</div>
    <div class = 'box'>4</div>
</body>
</html>
```

- main.js 에 다음 내용 작성

```jsx
const boxEl = document.querySelector(".box");
console.log(boxEl);

boxEl.addEventListener('click', function() {
    console.log('Click!');
    boxEl.classList.add('active');

    /*
    const hasActive = boxEl.classList.contains('active');
    console.log(hasActive);
    */
   // let hasActive = boxEl.classList.contains('active');
   // console.log(hasActive);

   // boxEl.classList.remove('active');
   // hasActive = boxEl.classList.contains('active');
   // console.log(hasActive);
});
```

- 1을 마우스로 클릭하면 다음과 같이 출력된다.
- Click이라는 이벤트를 감지하고 표시한다.

![Untitled](Ja/images/javaScript_practice_1/Untitled%201.png)

### div class

- 파일 생성
- PROJECT 아래에 생성
    - 파일 생성 : main2.js
    
- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script defer src="./main2.js"></script>

</head>
<body>
    <div class = 'box'>1</div>
    <div class = 'box'>2</div>
    <div class = 'box'>3</div>
    <div class = 'box'>4</div>
</body>
</html>
```

- main2.js 에 다음 내용 작성

```jsx
const boxE1s = document.querySelectorAll('.box');
console.log(boxE1s);

boxE1s.forEach(function(boxE1, index){
    boxE1.classList.add('order-${index}');
    console.log(boxE1, index);
});
```

- 다음과 같이 시스템 로그가 출력되었다.

![Untitled](Ja/images/javaScript_practice_1/Untitled%202.png)

### JS 구조 파악

- 다음 코드와 실행 결과로 구조를 파악해보자.
- main2.js 에 다음 내용 작성

```jsx
const boxE1s = document.querySelectorAll('.box');
console.log(boxE1s);

boxE1s.forEach(function(boxE1, index){
    // div 클래스면을 box order-1
    boxE1.classList.add('order-${index}');
    console.log(boxE1, index);
    console.log(boxE1.textContent);
    boxE1.textContent = "안녕";
    console.log(boxE1.textContent);
});
```

- index.html 의 1 2 3 4를 건드리지 않았음에도 다음과 같이 출력되었다.
- 이를 통해 페이지에 최종적으로 영향을 미치는 것은 JS임을 알 수 있다.

![Untitled](Ja/images/javaScript_practice_1/Untitled%203.png)